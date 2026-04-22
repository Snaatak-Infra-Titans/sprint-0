# Ansible Role — CD Workflow Documentation

**OT-Microservices | DevOps Engineering — Sprint 0**

> Author: Gourav | April 2026

---

| Author | Created On | Version | Last Updated By | Last Edited On | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|--------|------------|---------|-----------------|----------------|--------------|-------------|-------------|-------------|
| Gourav | April 2026 | v1.0 | Gouravk | April 2026 | | | | |

---


---

## Table of Contents

1. [What Is Continuous Deployment (CD)?](#1-what-is-continuous-deployment-cd)
2. [CD in the Context of Ansible Roles](#2-cd-in-the-context-of-ansible-roles)
3. [CD Workflow: Step-by-Step](#3-cd-workflow-step-by-step)
4. [Complete Jenkinsfile for CD](#4-complete-jenkinsfile-for-cd)
5. [Deployment Environments and Strategies](#5-deployment-environments-and-strategies)
6. [Pre-Deployment Checklist](#6-pre-deployment-checklist)
7. [Rollback Procedures](#7-rollback-procedures)
8. [CD Best Practices for Ansible Roles](#8-cd-best-practices-for-ansible-roles)
9. [Common CD Failures and How to Fix Them](#9-common-cd-failures-and-how-to-fix-them)
10. [Conclusion](#10-conclusion)

---

## 1. What Is Continuous Deployment (CD)?

Continuous Deployment (CD) is the practice of automatically releasing validated code changes to production (or staging/UAT) environments without manual intervention. Unlike Continuous Delivery, which makes code *ready* for release, Continuous Deployment actually *executes the release* automatically.

In the context of Ansible roles, CD means that the moment a Pull Request is approved and merged into the main branch, the automated pipeline **immediately deploys** the role changes to target infrastructure — databases, services, load balancers, and application servers.

### 1.1 CI → CD Pipeline

The CD pipeline assumes that the preceding CI pipeline (lint, syntax check, dry run) has already **passed**. CD adds the deployment stages:

| Stage | CI (Before Merge) | CD (After Merge) | Benefit |
|---|---|---|---|
| Validation | Lint, syntax, dry-run | Full deployment test | All changes pre-validated |
| Deployment | Not executed | Automatic to staging/prod | Zero manual steps |
| Testing | Static analysis only | Live smoke tests | Confirms actual impact |
| Approval | Code review only | Approval gate (optional) | Safety control |

---

## 2. CD in the Context of Ansible Roles

For the OT-Microservices project, Ansible roles automate the deployment of four services plus their dependencies. A robust CD pipeline ensures that infrastructure changes land smoothly across staging, UAT, and production environments.

### 2.1 Why CD for Ansible Roles?

| Without CD | With CD |
|---|---|
| Manual deployment steps | Automated end-to-end |
| Deployments only on schedule | Deploy multiple times per day |
| Deployment failures caught hours later | Failures caught in minutes |
| Long mean-time-to-recovery (MTTR) | Fast rollback via git tags |
| Manual approval gates | Jenkins approval gates |

---

## 3. CD Workflow: Step-by-Step

The CD workflow extends the CI pipeline with deployment and validation stages, triggering automatically after a PR merge:

| Stage | Tool | Action | Triggers On | Fails If... |
|---|---|---|---|---|
| 1. Merge | GitHub | PR merged to main | CI passed & approved | — |
| 2. Deploy | Ansible | Run role on staging | Deploy stage triggers | Task fails or vars undefined |
| 3. Smoke | Bash/Python | Health checks | Deployment completes | Service down or unreachable |
| 4. Approval | Jenkins | Wait for human OK | Staging smoke pass | Approval timeout |
| 5. Prod Deploy | Ansible | Run role on production | Approval granted | Task fails |

### 3.1 Detailed Stage Breakdown

#### Stage 1 — PR Approval and Merge

The CD pipeline triggers only after:

- CI pipeline has passed (lint, syntax check, dry run)
- PR is approved by at least one code reviewer
- Changes are merged to the main branch

#### Stage 2 — Deploy to Staging

The validated role is deployed to a staging environment (mirror of production) for smoke testing and validation.

**Command:**
```bash
ansible-playbook deploy.yml -i inventory/staging
```

The deployment uses tags to control which parts of the role execute:

```bash
ansible-playbook deploy.yml -i inventory/staging --tags='app-config,restart-services' --skip-tags='skip-in-staging'
```

#### Stage 3 — Smoke Tests

After deployment to staging, automated tests validate that the role executed correctly and services are healthy:

- HTTP health checks (curl, wget)
- Service availability checks (port listening)
- Database connectivity tests
- Log inspection for errors

```bash
bash tests/smoke_tests.sh staging
```

#### Stage 4 — Manual Approval (Optional)

For production deployments, require explicit human approval before proceeding. This is a safety gate to prevent accidental production changes.

#### Stage 5 — Deploy to Production

Only after staging validation passes (and manual approval if configured), the role is deployed to production:

```bash
ansible-playbook deploy.yml -i inventory/production --extra-vars 'deploy_version=1.2.3'
```

#### Stage 6 — Post-Deployment Validation

Run the same smoke tests against production to confirm deployment success and service health.

---

## 4. Complete Jenkinsfile for CD

Save this file at the root of your repository as **Jenkinsfile**.

```groovy
pipeline {
    agent any

    options {
        timeout(time: 1, unit: 'HOURS')
        timestamps()
        buildDiscarder(logRotator(numToKeepStr: '20'))
    }

    environment {
        SLACK_CHANNEL = '#devops-alerts'
        ANSIBLE_VAULT_PASSWORD_FILE = credentials('ansible-vault-password')
        DEPLOY_VERSION = "${BUILD_NUMBER}"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                    pip install --upgrade pip
                    pip install ansible ansible-lint
                '''
            }
        }

        stage('Lint') {
            steps {
                sh 'ansible-lint roles/'
            }
        }

        stage('Syntax Check') {
            steps {
                sh 'ansible-playbook tests/test.yml --syntax-check -i tests/inventory'
            }
        }

        stage('Dry Run') {
            steps {
                sh '''
                    ansible-playbook tests/test.yml \
                        -i tests/inventory \
                        --check \
                        --diff
                '''
            }
        }

        stage('Deploy to Staging') {
            when {
                branch 'main'
            }
            steps {
                sh '''
                    echo "=== Deploying to Staging ==="
                    ansible-playbook deploy.yml \
                        -i inventory/staging \
                        -e "deploy_version=${BUILD_NUMBER}" \
                        --vault-password-file=${ANSIBLE_VAULT_PASSWORD_FILE}
                '''
            }
        }

        stage('Smoke Tests - Staging') {
            when {
                branch 'main'
            }
            steps {
                sh '''
                    echo "=== Running Smoke Tests on Staging ==="
                    bash tests/smoke_tests.sh staging
                '''
            }
        }

        stage('Approval for Production') {
            when {
                branch 'main'
            }
            steps {
                input message: 'Deploy to Production?', ok: 'Deploy', submitter: 'devops-team'
            }
        }

        stage('Deploy to Production') {
            when {
                branch 'main'
            }
            steps {
                sh '''
                    echo "=== Deploying to Production ==="
                    ansible-playbook deploy.yml \
                        -i inventory/production \
                        -e "deploy_version=${BUILD_NUMBER}" \
                        --vault-password-file=${ANSIBLE_VAULT_PASSWORD_FILE}
                '''
            }
        }

        stage('Smoke Tests - Production') {
            when {
                branch 'main'
            }
            steps {
                sh '''
                    echo "=== Running Smoke Tests on Production ==="
                    bash tests/smoke_tests.sh production
                '''
            }
        }

    }

    post {
        success {
            echo 'CD pipeline completed successfully.'
            // slackSend channel: "${SLACK_CHANNEL}", 
            //     message: " Ansible CD passed: ${JOB_NAME} #${BUILD_NUMBER} deployed to production"
        }
        failure {
            echo 'CD pipeline failed. Check logs above.'
            // slackSend channel: "${SLACK_CHANNEL}", 
            //     message: " Ansible CD failed: ${JOB_NAME} #${BUILD_NUMBER}. Check logs at ${BUILD_URL}"
        }
        always {
            cleanWs()
        }
    }
}
```

**Configure Jenkins credentials for vault password:**

- Jenkins Dashboard → Manage Credentials → System → Global credentials
- Create a Secret file credential named **ansible-vault-password**

---

## 5. Deployment Environments and Strategies

### 5.1 Environment Inventory Files

Maintain separate inventory files for each environment:

```
inventory/
├── staging
│   └── hosts.ini          # Staging infrastructure
├── uat
│   └── hosts.ini          # User acceptance testing
└── production
    └── hosts.ini          # Production infrastructure
```

**Example staging inventory (inventory/staging/hosts.ini):**

```ini
[app_servers]
staging-app-01 ansible_host=10.0.1.10 ansible_user=ubuntu
staging-app-02 ansible_host=10.0.1.11 ansible_user=ubuntu

[databases]
staging-db-01 ansible_host=10.0.2.20 ansible_user=ubuntu

[nginx]
staging-lb-01 ansible_host=10.0.0.5 ansible_user=ubuntu

[all:vars]
ansible_ssh_private_key_file=~/.ssh/id_rsa
environment_name=staging
app_version=latest
```

### 5.2 Deployment Strategies

| Strategy | How It Works | Best For | Risk |
|---|---|---|---|
| **All-at-once** | Deploy to all servers simultaneously | Testing, dev environments | High (full downtime if fails) |
| **Rolling** | Deploy batch-by-batch (e.g., 2 servers at a time) | Production, high availability | Low (partial service maintains) |
| **Canary** | Deploy to 1 server, monitor, then rest | Critical services, high-risk changes | Very low (early detection) |
| **Blue-Green** | Deploy to inactive cluster, switch via load balancer | Zero-downtime deployments | Low (full rollback instant) |

---

## 6. Pre-Deployment Checklist

Before running CD, verify:

- ✓ Ansible vault file is encrypted and accessible to Jenkins
- ✓ Inventory files are up-to-date with correct hostnames/IPs
- ✓ SSH keys deployed on all target hosts
- ✓ Firewall rules allow Ansible connectivity on port 22
- ✓ All role dependencies (handlers, vars) are available
- ✓ Smoke test script is executable and tested locally
- ✓ Approval group (LDAP/Active Directory) is configured in Jenkins

---

## 7. Rollback Procedures

If a deployment fails, use these rollback steps:

### 7.1 Immediate Rollback (Last Known Good Version)

Redeploy the previous stable version of the role:

```bash
# Identify the last successful build number
LAST_SUCCESSFUL_BUILD=42

# Deploy from git tag corresponding to that build
git checkout tags/v1.2.1

# Run deployment with previous version
ansible-playbook deploy.yml \
    -i inventory/production \
    -e "deploy_version=v1.2.1" \
    --vault-password-file=${VAULT_FILE}
```

### 7.2 Git Tag-Based Deployment

Create a Jenkins pipeline that allows manual selection of a release tag:

```groovy
// In Jenkinsfile post-production stage
parameters {
    choice(
        name: 'RELEASE_TAG',
        choices: ['v1.3.0', 'v1.2.1', 'v1.2.0'],
        description: 'Select the role version to deploy'
    )
}

stage('Deploy Selected Release') {
    steps {
        sh '''
            git checkout tags/${RELEASE_TAG}
            ansible-playbook deploy.yml \
                -i inventory/production \
                -e "deploy_version=${RELEASE_TAG}"
        '''
    }
}
```

### 7.3 Canary Rollback

If only some servers deployed successfully, revert just those:

```bash
# Rollback specific hosts
ansible-playbook deploy.yml \
    -i inventory/production \
    --limit production-app-01,production-app-02 \
    -e "deploy_version=v1.2.1 rollback_mode=true"
```

---

## 8. CD Best Practices for Ansible Roles

| Practice | Why It Matters | Implementation |
|---|---|---|
| **Tag every release** | Fast rollbacks, clear version history | `git tag -a v1.2.3 && git push origin v1.2.3` |
| **Encrypt all secrets** | Prevents credential exposure in logs | Use ansible-vault, Jenkins Credentials Store |
| **Staging mirrors production** | Catch environment-specific issues | Same OS, same packages, same firewall rules |
| **Limit deployment windows** | Reduces impact on users | Schedule deployments for off-peak hours |
| **Monitor post-deploy** | Catch failures before users notice | CloudWatch, Prometheus, ELK logs |
| **Document runbooks** | Enable oncall escalation | Wiki page per service with common issues |

---

## 9. Common CD Failures and How to Fix Them

| Error | Cause | Fix | Prevention |
|---|---|---|---|
| **Connection refused on port 22** | SSH unreachable | Check firewall rules, verify IP in inventory | Test connectivity in staging first |
| **fatal: Timeout waiting for ansible** | Task takes too long | Add timeout_seconds or async | Profile long tasks, add explicit timeouts |
| **Vault password incorrect** | Jenkins credentials not configured | Verify vault file in Credentials Store | Test vault decrypt locally first |
| **Smoke test fails after deploy** | Service crashed or misconfigured | Check service logs, restart manually if needed | Trigger automatic rollback on smoke test failure |
| **'undefined variable' error** | Variable not in inventory | Add to defaults/main.yml or inventory file | Run dry run with all required vars first |

---

## 10. Conclusion

CD for Ansible roles transforms infrastructure management from a manual, error-prone process into an automated, reliable, and auditable pipeline. When every change follows a validated path through staging, testing, and production, teams can deploy infrastructure updates with the same confidence as application releases.

### For the OT-Microservices project:

- ✓ Infrastructure changes are validated before production
- ✓ Rollbacks are fast and reliable (git-based versioning)
- ✓ Deployments are auditable (Jenkins logs, git history)
- ✓ Team velocity increases (less manual intervention)

Combine this CD pipeline with the CI pipeline documented in the companion **Ansible Role — CI Workflow Documentation**, and your team will have a modern, enterprise-grade infrastructure-as-code practice.

---

## Document Metadata

| Field | Value |
|---|---|
| Author | Gourav |
| Created On | April 2026 |
| Version | v1.0 |
| Last Updated | April 2026 |
| Document Type | DevOps Documentation |

---

## References

- [Ansible Documentation](https://docs.ansible.com)
- [Jenkins Pipeline Documentation](https://www.jenkins.io/doc/book/pipeline/)
- [Jenkins Slack Plugin](https://plugins.jenkins.io/slack/)
- [OT-Microservices Repository](https://github.com/OT-MICROSERVICES)

---

## Contact Information

| Name   | Email                                                                             |
| ------ | --------------------------------------------------------------------------------- |
| gourav sharma | [gourav.sharma.snaatak@mygurukulam.co](mailto:gourav.sharma.snaatak@mygurukulam.co) |
---
