# Ansible Role — CI Workflow Documentation

**OT-Microservices | DevOps Engineering — Sprint 0**

> Author: Deepak | April 2026

---

| Author | Created On | Version | Last Updated By | Last Edited On | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|--------|------------|---------|-----------------|----------------|--------------|-------------|-------------|-------------|
| Deepak | April 2026 | v1.0 | Deepak | April 2026 | | | | |

---

## Table of Contents

1. [What Is Continuous Integration (CI)?](#1-what-is-continuous-integration-ci)
2. [CI in the Context of Ansible Roles](#2-ci-in-the-context-of-ansible-roles)
3. [CI Workflow: Step-by-Step](#3-ci-workflow-step-by-step)
4. [Complete Jenkinsfile](#4-complete-jenkinsfile)
5. [Required File and Directory Structure](#5-required-file-and-directory-structure)
6. [Sample Dry Run Configuration](#6-sample-dry-run-configuration)
7. [CI Best Practices for Ansible Roles](#7-ci-best-practices-for-ansible-roles)
8. [Common CI Failures and How to Fix Them](#8-common-ci-failures-and-how-to-fix-them)
9. [Conclusion](#9-conclusion)
10. [References](#10-references)

---

## 1. What Is Continuous Integration (CI)?

Continuous Integration (CI) is a software development practice where developers frequently merge their code changes into a shared repository — usually multiple times per day. Each merge triggers an automated pipeline that builds the code, runs tests, and validates quality before the change is accepted.

The core idea behind CI is simple: **the sooner you find a bug, the cheaper it is to fix.** By integrating code continuously rather than at the end of a sprint, teams catch integration conflicts, failed tests, and broken deployments almost immediately.

### 1.1 Why Does CI Matter?

| Without CI | With CI |
|---|---|
| Code merged once at end of sprint | Code merged multiple times per day |
| Integration bugs discovered late | Bugs caught within minutes of commit |
| Manual testing by developers | Automated tests run on every push |
| "Works on my machine" syndrome | Consistent, validated role execution |
| Long, painful release cycles | Faster, confident deployments |
| One person manually runs tests | Pipeline runs in parallel across all PRs |

---

## 2. CI in the Context of Ansible Roles

An Ansible role encapsulates reusable automation logic — directory structure, tasks, handlers, variables, templates, and defaults. When multiple engineers contribute to the same role, a CI pipeline ensures that every change meets quality standards before it lands in the main branch.

For the OT-Microservices project, Ansible roles are used to automate the deployment of all four services (Employee API, Salary API, Attendance API, and Frontend) along with their dependencies (ScyllaDB, PostgreSQL, Redis, Nginx). The CI pipeline for these roles validates:

- YAML syntax and Ansible linting rules
- Role directory structure compliance
- Variable and defaults file correctness
- Jinja2 template rendering without errors
- Idempotency: running the role twice produces the same result
- **Dry run (`--check` mode):** validates the full role execution path without making any changes on target hosts

---

## 3. CI Workflow: Step-by-Step

### 3.1 Workflow Overview

The CI workflow for an Ansible role follows this sequence every time a developer pushes code or opens a Pull Request:

| Stage | Tool | What It Does | Fails If... |
|---|---|---|---|
| 1. Trigger | Jenkins | Developer pushes to a branch or opens PR | — |
| 2. Checkout | Git SCM | Clones the repo into the Jenkins workspace | Repo unreachable |
| 3. Lint | ansible-lint | Checks Ansible tasks against best-practice rules | Any rule violation found |
| 4. Syntax Check | ansible-playbook --syntax-check | Parses YAML, validates module usage | Invalid YAML or unknown module |
| 5. Dry Run | ansible-playbook --check | Executes role logic without applying changes; validates task flow and variables | Task would fail or produce unexpected changes |
| 6. Notify | Slack / Email | Reports pipeline result to the team | — |

### 3.2 Detailed Stage Breakdown

#### Stage 1 — Code Push / Pull Request Trigger

The pipeline starts automatically when:

- A developer pushes commits to any branch
- A Pull Request (PR) is opened targeting the `main` or `develop` branch
- A PR is updated with new commits

> **Best Practice:** Require CI to pass before merging any PR. Enforce this via Jenkins branch protection rules or protected branches in your SCM.

#### Stage 2 — Repository Checkout

The Jenkins pipeline checks out the full repository. For Ansible roles hosted in a monorepo (like OT-Microservices), the SCM checkout fetches the entire repo so all role files are available.

```groovy
checkout scm
```

#### Stage 3 — Linting with ansible-lint

`ansible-lint` scans all task files, handlers, and playbooks for rule violations. It catches common mistakes such as:

- Using `command:` or `shell:` instead of idiomatic Ansible modules
- Missing `name:` fields on tasks
- Using deprecated module syntax
- YAML indentation errors
- Hardcoded credentials in variables

```bash
ansible-lint roles/
```

> **Configuration:** Place a `.ansible-lint` file in the repo root to configure which rules to enforce or skip. For new teams, start with the `production` profile.

#### Stage 4 — Syntax Check

The syntax check runs `ansible-playbook --syntax-check` against a test playbook that includes the role. This catches YAML parsing errors, references to undefined variables, and unknown Ansible modules that `ansible-lint` might miss.

```bash
ansible-playbook tests/test.yml --syntax-check -i tests/inventory
```

#### Stage 5 — Dry Run (`--check` Mode)

The dry run stage uses Ansible's built-in `--check` flag to simulate the full role execution against real or mock inventory without making any actual changes on target hosts. This is the most comprehensive pre-deployment validation step.

**What `--check` mode does:**
- Evaluates all tasks and their conditions (`when:`, loops, etc.)
- Resolves all variables and template expressions
- Reports what *would* change — without changing anything
- Detects tasks that would fail due to missing files, wrong module args, or unresolvable variables

```bash
ansible-playbook tests/test.yml -i tests/inventory --check
```

**With a diff for visibility:**

```bash
ansible-playbook tests/test.yml -i tests/inventory --check --diff
```

> **Idempotency Validation:** Run the dry run twice in sequence. If the second run reports zero changes (`changed=0`), the role is idempotent. If it still reports changes, investigate tasks that always report `changed` regardless of actual state.

**Check mode with extra variables (for dynamic roles):**

```bash
ansible-playbook tests/test.yml -i tests/inventory --check \
  -e "app_version=1.0.0 env=staging"
```

> **Note:** Some tasks (e.g., those using `command:` or `shell:`) may not fully support `--check` mode and will be skipped. Mark such tasks explicitly with `check_mode: false` or add a `changed_when:` condition to handle them correctly.

#### Stage 6 — Notification

At the end of the pipeline, the result (pass or fail) is sent to the team via Slack or email. This ensures engineers are immediately aware of broken builds without checking the Jenkins dashboard manually.

---

## 4. Complete Jenkinsfile

Save this file at the root of your repository as `Jenkinsfile`.

```groovy
pipeline {
    agent any


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

        stage('Idempotency Check') {
            steps {
                sh '''
                    echo "=== First dry run ==="
                    ansible-playbook tests/test.yml -i tests/inventory --check --diff

                    echo "=== Second dry run (must show changed=0) ==="
                    ansible-playbook tests/test.yml -i tests/inventory --check --diff \
                        | tee /tmp/idempotency_output.txt

                    grep -q "changed=0" /tmp/idempotency_output.txt \
                        || (echo "IDEMPOTENCY CHECK FAILED" && exit 1)
                '''
            }
        }
    }

    post {
        success {
            echo 'CI pipeline passed. Role is lint-clean, syntax-valid, and dry-run verified.'
            // slackSend channel: '#devops-alerts', message: "✅ Ansible CI passed: ${env.JOB_NAME} #${env.BUILD_NUMBER}"
        }
        failure {
            echo 'CI pipeline failed. Check the logs above for details.'
            // slackSend channel: '#devops-alerts', message: "❌ Ansible CI failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}"
        }
        always {
            cleanWs()
        }
    }
}
```

> **Slack notifications:** Uncomment the `slackSend` lines and install the [Jenkins Slack plugin](https://plugins.jenkins.io/slack/) to enable team alerts.

---

## 5. Required File and Directory Structure

For the CI pipeline to work, the Ansible role and test files must follow this structure:

```
ansible-role-employee-api/
├── tasks/
│   └── main.yml                  # Main tasks
├── handlers/
│   └── main.yml                  # Service restart handlers
├── defaults/
│   └── main.yml                  # Default variable values
├── vars/
│   └── main.yml                  # Role-specific variables
├── templates/
│   └── config.yaml.j2            # Jinja2 config templates
├── meta/
│   └── main.yml                  # Role metadata (galaxy info)
├── tests/
│   ├── test.yml                  # Minimal playbook for syntax check & dry run
│   └── inventory                 # Test inventory (localhost or staging host)
├── .ansible-lint                 # ansible-lint configuration
└── Jenkinsfile                   # Jenkins pipeline definition
```

### tests/test.yml

```yaml
---
- name: Test playbook for CI dry run
  hosts: all
  become: true
  roles:
    - role: ansible-role-employee-api
```

### tests/inventory

```ini
[test]
localhost ansible_connection=local

# For dry run against a remote staging host:
# [staging]
# 192.168.1.10 ansible_user=ubuntu ansible_ssh_private_key_file=~/.ssh/id_rsa
```

---

## 6. Sample Dry Run Configuration

### 6.1 .ansible-lint

```yaml
---
profile: production

exclude_paths:
  - .cache/
  - .github/

warn_list:
  - experimental

skip_list: []
```

### 6.2 Running Dry Run Locally (Before Pushing)

Before pushing to Jenkins, developers should validate their changes locally:

```bash
# Lint check
ansible-lint roles/

# Syntax check
ansible-playbook tests/test.yml --syntax-check -i tests/inventory

# Full dry run with diff
ansible-playbook tests/test.yml -i tests/inventory --check --diff

# Dry run with extra vars
ansible-playbook tests/test.yml -i tests/inventory --check --diff \
  -e "app_version=1.2.0 deploy_env=staging"
```

### 6.3 Handling Tasks That Don't Support Check Mode

Some tasks (e.g., `command:`, `shell:`, file downloads) may be skipped during `--check` mode. Handle them explicitly:

```yaml
# Option 1: Mark as always-run in check mode
- name: Run migration script
  ansible.builtin.command: /opt/app/migrate.sh
  check_mode: false

# Option 2: Suppress false "changed" reports
- name: Check app health
  ansible.builtin.command: curl -sf http://localhost:8080/health
  changed_when: false
  check_mode: false
```

---

## 7. CI Best Practices for Ansible Roles

| Practice | Why It Matters |
|---|---|
| Pin dependency versions in `requirements.txt` | Prevents surprise failures when upstream packages update |
| Cache pip packages between Jenkins builds | Reduces CI execution time significantly |
| Test dry run against multiple environments (staging, UAT) | Ensures role works across your actual infrastructure |
| Enforce idempotency check in dry run (two consecutive runs) | Catches tasks that make unnecessary changes on re-runs |
| Use `--diff` flag alongside `--check` | Shows exactly what would change, making review easier |
| Keep lint warnings as errors in production profiles | Higher code quality, fewer runtime surprises |
| Mark `check_mode: false` for tasks that must always run | Prevents silent task skips masking real failures |
| Store secrets in Jenkins Credentials Store | Never put passwords or tokens in `Jenkinsfile` or inventory |
| Run dry run against a realistic staging inventory | Localhost-only dry runs may miss network/host-specific issues |

---

## 8. Common CI Failures and How to Fix Them

| Error | Cause | Fix |
|---|---|---|
| `ansible-lint: E301 Commands should not change things if nothing needs doing` | Task uses `command:` or `shell:` instead of an Ansible module | Replace with the appropriate Ansible module (e.g., `ansible.builtin.package` instead of `shell: apt install`) |
| `Syntax Error: could not find expected ':'` | YAML indentation error in task file | Run `yamllint` locally; check spacing around colons |
| `Skipping task in check mode` | Task does not support `--check` and has no `check_mode` directive | Add `check_mode: false` or ensure the task uses a module with check mode support |
| `Idempotence check failed: N change(s) on second run` | A task always reports `changed` even when nothing changed | Add `changed_when: false` or use an Ansible module instead of `command:`/`shell:` |
| `fatal: FAILED! => msg: 'The conditional check failed'` | A `when:` condition references a variable not defined in test inventory | Define the variable in `defaults/main.yml` or pass it via `-e` in the dry run command |
| `ModuleNotFoundError: No module named 'ansible'` | Ansible not installed in the Jenkins agent Python environment | Add `pip install ansible ansible-lint` to the Install Dependencies stage |

---

## 9. Conclusion

CI for Ansible roles is not just about running tests — it is about **maintaining trust in your automation.** When every change to a role is validated automatically through linting, syntax checking, and dry runs, your team can deploy with confidence knowing that:

- The YAML syntax is valid
- Ansible best practices are followed
- The role's task logic is sound and will not cause unexpected changes
- Re-running the role produces no unintended side effects

For the OT-Microservices project, implementing CI on Ansible roles means that infrastructure deployments are as reliable as application deployments. A broken role is caught in the Jenkins pipeline within minutes, not discovered hours later on a production server.

---

## 10. References

- [Ansible Documentation](https://docs.ansible.com)
- [ansible-lint Documentation](https://ansible.readthedocs.io/projects/lint/)
- [Ansible Check Mode (Dry Run)](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_checkmode.html)
- [Jenkins Pipeline Documentation](https://www.jenkins.io/doc/book/pipeline/)
- [Jenkins Slack Plugin](https://plugins.jenkins.io/slack/)
- [OT-Microservices Repository](https://github.com/OT-MICROSERVICES)

---

> **Document Owner:** Deepak
| **Last Updated:** April 2026
