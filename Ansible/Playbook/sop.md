# Standard Operating Procedure — Ansible Playbook Execution

| Field             | Details                                      |
|-------------------|----------------------------------------------|
| **Document ID**   | CS-ANS-PB-SOP-001                            |
| **Stack**         | Common Stack                                 |
| **Domain**        | Infrastructure Automation — Ansible          |
| **Version**       | 1.0.0                                        |
| **Status**        | Active                                       |
| **Last Reviewed** | 2025-01-01                                   |
| **Owner**         | Platform / Infrastructure Engineering Team  |

---

## Table of Contents

1. [Purpose](#1-purpose)
2. [Scope](#2-scope)
3. [Roles and Responsibilities](#3-roles-and-responsibilities)
4. [Prerequisites](#4-prerequisites)
5. [Required Inputs](#5-required-inputs)
6. [Playbook Structure Standard](#6-playbook-structure-standard)
7. [Execution Steps](#7-execution-steps)
8. [Validation Checks](#8-validation-checks)
9. [Rollback Procedure](#9-rollback-procedure)
10. [Error Handling and Escalation](#10-error-handling-and-escalation)
11. [Audit and Logging](#11-audit-and-logging)
12. [Change Control](#12-change-control)
13. [Glossary](#13-glossary)

---

## 1. Purpose

This Standard Operating Procedure (SOP) defines the mandatory process for **authoring, reviewing, executing, and validating** Ansible playbooks within the Common Stack infrastructure automation framework.

It exists to ensure:

- Playbook runs are **repeatable, predictable, and peer-reviewed** before reaching production.
- All automation changes follow a **documented, auditable workflow** consistent with change management policy.
- Engineers executing playbooks have a **clear, step-by-step process** with defined checkpoints, reducing the risk of configuration drift, outages, or data loss.
- Validation gates are consistently applied so that **failures are caught early** — in staging — rather than in production.

This SOP applies to all playbooks regardless of target scope (single host, host group, or full environment). Emergency (break-glass) procedures are noted where they diverge from the standard flow.

---

## 2. Scope

| In Scope                                                               | Out of Scope                                              |
|------------------------------------------------------------------------|-----------------------------------------------------------|
| All Ansible playbooks authored within the Common Stack repository      | Ad-hoc `ansible` commands run directly (no SOP required, but log them) |
| Playbook execution against staging, UAT, and production environments   | Molecule/unit tests run locally during development        |
| Automated playbook runs triggered via CI/CD pipelines                  | Terraform, Helm, or other IaC tooling                     |
| Role-level changes that alter play behaviour across multiple playbooks  | Reading-only inventory operations                         |

---

## 3. Roles and Responsibilities

| Role                     | Responsibility                                                                                   |
|--------------------------|--------------------------------------------------------------------------------------------------|
| **Playbook Author**      | Writes, lints, and unit-tests the playbook. Opens the PR. Fills in the Run Request form.        |
| **Peer Reviewer**        | Reviews playbook logic, idempotency, and variable hygiene. Approves or requests changes on PR.  |
| **Execution Operator**   | Runs the playbook after all approvals are obtained. Must not be the same person as the Author for production runs. |
| **Change Approver**      | Approves the Change Request ticket (CAB or designated approver). Required for production only.  |
| **Incident Responder**   | Owns rollback and escalation if execution fails. Usually the on-call engineer.                  |

> **Separation of duty:** For production environments, the Author and the Execution Operator **must** be different individuals.

---

## 4. Prerequisites

All of the following must be satisfied **before** beginning execution. Do not proceed if any item is unresolved.

### 4.1 System Prerequisites

- [ ] Ansible `>= 2.14` installed on the control node (`ansible --version`)
- [ ] Python `>= 3.9` available on the control node
- [ ] All required Ansible collections installed (`ansible-galaxy collection install -r requirements.yml`)
- [ ] SSH connectivity verified to all target hosts (`ansible all -m ping -i inventory/`)
- [ ] Sufficient disk space on the control node (`df -h` — minimum 500 MB free)

### 4.2 Access Prerequisites

- [ ] The executing user has SSH key-based access to target hosts (no password prompts)
- [ ] Vault password or Vault token available if the playbook references encrypted variables
- [ ] Sudo / privilege escalation (`become: true`) confirmed working on target hosts
- [ ] Read access to the Common Stack Git repository confirmed

### 4.3 Process Prerequisites

- [ ] Playbook has passed all linting checks (see §7.2)
- [ ] Playbook has been peer-reviewed and PR approved
- [ ] Playbook has been executed successfully in the staging environment
- [ ] A Change Request ticket has been raised and approved (production only)
- [ ] A maintenance window has been scheduled and communicated (if service-impacting)
- [ ] A rollback plan is documented (see §9)

---

## 5. Required Inputs

Every playbook execution requires the following inputs to be defined and verified before the run begins.

### 5.1 Inventory

The target inventory must be explicitly specified on the command line. Never rely on the default `/etc/ansible/hosts`.

| Input         | Description                                         | Example                              |
|---------------|-----------------------------------------------------|--------------------------------------|
| `inventory`   | Path to inventory file or directory                 | `-i inventory/production/`           |
| Target hosts  | Specific host or group to limit the run             | `--limit webservers` or `--limit app01.prod.example.com` |

```bash
# Always specify inventory explicitly
ansible-playbook site.yml -i inventory/production/
```

### 5.2 Variables

Variables may be sourced from the following locations. All must be reviewed before execution.

| Source                  | File / Flag                              | Priority (Highest → Lowest)  |
|-------------------------|------------------------------------------|------------------------------|
| Extra vars (CLI)        | `-e "key=value"` or `-e @vars_file.yml` | 1 (highest)                  |
| Playbook `vars:`        | Inline in play definition                | 2                            |
| Role `vars/main.yml`    | Internal role constants                  | 3                            |
| Host vars               | `inventory/host_vars/<hostname>.yml`     | 4                            |
| Group vars              | `inventory/group_vars/<group>.yml`       | 5                            |
| Role `defaults/main.yml`| Overridable defaults                     | 6 (lowest)                   |

**Mandatory variable review checklist:**

- [ ] Confirm environment-specific variables (`env`, `region`, `datacenter`) are correctly set for the target environment
- [ ] Confirm no production credentials are passed as plaintext — use Ansible Vault
- [ ] Confirm `ansible_user` and `ansible_become` are set appropriately for the target hosts
- [ ] If using `-e @extra_vars.yml`, review the file content before execution

### 5.3 Ansible Vault

If the playbook references Vault-encrypted variables:

```bash
# Option A — provide vault password file (recommended for CI/CD)
ansible-playbook site.yml -i inventory/production/ --vault-password-file ~/.vault_pass

# Option B — prompt interactively (recommended for human-run executions)
ansible-playbook site.yml -i inventory/production/ --ask-vault-pass
```

- [ ] Vault password file permissions confirmed at `600` (`chmod 600 ~/.vault_pass`)
- [ ] Vault password file is **not** committed to the repository

### 5.4 Tags

Use `--tags` to scope execution to specific parts of the playbook when performing targeted changes:

```bash
# Run only tasks tagged 'deploy'
ansible-playbook site.yml -i inventory/production/ --tags deploy

# Skip tasks tagged 'restart'
ansible-playbook site.yml -i inventory/production/ --skip-tags restart
```

> **Caution:** When using `--tags` in production, ensure that skipping unlisted tasks does not leave the system in an inconsistent state.

---

## 6. Playbook Structure Standard

All playbooks in the Common Stack must conform to the following structure before they are eligible for review and execution.

### 6.1 Required Header Block

Every playbook file must begin with a metadata comment block:

```yaml
---
# =============================================================================
# Playbook   : <descriptive name>
# Description: <one or two sentences explaining what this playbook does>
# Author     : <name or team>
# Version    : <semver, e.g., 1.2.0>
# Last Update: <YYYY-MM-DD>
# Ticket     : <JIRA/Linear/GitHub issue reference>
# Usage      :
#   ansible-playbook <playbook>.yml -i inventory/<env>/ [--limit <group>]
# =============================================================================
```

### 6.2 Required Play-Level Keys

```yaml
- name: "Deploy application — Common Stack"    # Human-readable, specific name
  hosts: "{{ target_hosts | default('app') }}" # Always parameterise the hosts value
  become: true                                  # Declare explicitly, even if false
  gather_facts: true                            # Declare explicitly
  any_errors_fatal: false                       # Set to true only when a partial run is worse than stopping
  vars_files:
    - vars/common.yml
  roles:
    - common
    - app
```

### 6.3 Task Naming Convention

Every task must have a `name` that is written in sentence case, specific enough to understand without reading the module arguments, and prefixed with the role or component name where ambiguity exists.

```yaml
# BAD
- name: Do thing
  ansible.builtin.copy:
    src: nginx.conf
    dest: /etc/nginx/nginx.conf

# GOOD
- name: "nginx | Deploy main configuration file"
  ansible.builtin.copy:
    src: nginx.conf
    dest: /etc/nginx/nginx.conf
    owner: root
    group: root
    mode: '0644'
```

### 6.4 Idempotency Requirement

All tasks **must be idempotent** — running the playbook twice must produce the same end state without unintended side effects. Tasks that are not naturally idempotent must use guards:

```yaml
- name: "ssl | Generate DH parameters (only if file absent)"
  ansible.builtin.command:
    cmd: openssl dhparam -out /etc/ssl/dhparams.pem 4096
    creates: /etc/ssl/dhparams.pem  # Guards idempotency — skips if file exists
```

---

## 7. Execution Steps

Follow these steps in sequence. Do not skip steps. Mark each checkbox as you proceed.

### Step 1 — Verify Prerequisites

```bash
# Confirm Ansible version
ansible --version

# Confirm collections are installed
ansible-galaxy collection list

# Confirm SSH connectivity to all target hosts
ansible all -m ping -i inventory/<env>/
```

- [ ] All prerequisites in §4 are satisfied
- [ ] All required inputs in §5 are defined and reviewed

---

### Step 2 — Lint and Static Analysis

Run linting checks before every execution. **Do not proceed if linting fails.**

```bash
# Install ansible-lint if not present
pip install ansible-lint

# Run lint against the playbook
ansible-lint <playbook>.yml

# Run YAML lint
yamllint <playbook>.yml
```

Expected output: `Passed: 0 failure(s), 0 warning(s)`

- [ ] `ansible-lint` passes with zero errors
- [ ] `yamllint` passes with zero errors

---

### Step 3 — Dry Run (Check Mode)

Execute a dry run against the target environment. Check mode simulates the playbook without making changes.

```bash
ansible-playbook <playbook>.yml \
  -i inventory/<env>/ \
  --check \
  --diff \
  [--limit <host_or_group>] \
  [--vault-password-file ~/.vault_pass]
```

Review the output carefully:

- [ ] No unexpected `changed` tasks — verify any change shown is intentional
- [ ] No `fatal` errors during check mode
- [ ] `--diff` output reviewed: confirm file changes are correct before proceeding
- [ ] Host count in `PLAY RECAP` matches expected target count

> **Note:** Check mode may report false positives for tasks that depend on state created earlier in the same run (e.g., a file created by task 3, referenced by task 5). This is expected behaviour — note these cases and verify manually post-run.

---

### Step 4 — Staging Execution (Mandatory)

Execute the playbook against the **staging environment** before any production run.

```bash
ansible-playbook <playbook>.yml \
  -i inventory/staging/ \
  --vault-password-file ~/.vault_pass \
  | tee logs/staging_$(date +%Y%m%d_%H%M%S).log
```

- [ ] Playbook completes with zero `failed` tasks in `PLAY RECAP`
- [ ] `changed` task count is as expected (document the expected count before running)
- [ ] Services or components targeted by the playbook are verified working in staging (see §8)
- [ ] Log file saved to `logs/` directory with timestamp

---

### Step 5 — Change Request Approval (Production Only)

For production runs, the following must be completed before proceeding:

- [ ] Change Request ticket is in **Approved** status
- [ ] Scheduled maintenance window is active or approved for the current time slot
- [ ] On-call engineer has been notified and is available
- [ ] Rollback procedure documented and reviewed (§9)
- [ ] Stakeholders notified of upcoming change

**Do not proceed to Step 6 without Change Request approval for production.**

---

### Step 6 — Production Execution

```bash
ansible-playbook <playbook>.yml \
  -i inventory/production/ \
  --vault-password-file ~/.vault_pass \
  [--limit <host_or_group>] \
  | tee logs/production_$(date +%Y%m%d_%H%M%S).log
```

**During execution:**

- Monitor output in real time. Do not leave an unattended production run.
- If any task reports `fatal`, assess immediately — do not wait until the end of the run.
- If `any_errors_fatal: true` is set, the playbook will stop automatically on the first failure.
- Keep the Change Request ticket updated with run status.

**Execution flags reference:**

| Flag                             | Purpose                                        |
|----------------------------------|------------------------------------------------|
| `-i inventory/<env>/`            | Target environment inventory                   |
| `--limit <host>`                 | Scope run to specific host or group            |
| `--tags <tag>`                   | Run only tagged tasks                          |
| `--skip-tags <tag>`              | Skip tagged tasks                              |
| `--check --diff`                 | Dry run with diff output                       |
| `--vault-password-file <path>`   | Non-interactive vault decryption               |
| `-v / -vv / -vvv`               | Increase verbosity (use `-vv` for debugging)   |
| `--start-at-task "<task name>"`  | Resume from a specific task (use with caution) |
| `--step`                         | Prompt before each task (interactive review)   |

---

### Step 7 — Post-Execution Review

After the playbook completes:

```bash
# Review PLAY RECAP
grep -A 10 "PLAY RECAP" logs/production_<timestamp>.log

# Check for any failed or unreachable hosts
grep -E "failed=[^0]|unreachable=[^0]" logs/production_<timestamp>.log
```

- [ ] `PLAY RECAP` shows `failed=0` and `unreachable=0` for all hosts
- [ ] `changed` count is within expected range
- [ ] Log file is stored in the `logs/` directory and linked to the Change Request ticket

---

## 8. Validation Checks

Validation must be performed after every successful execution. These checks confirm the intended end state was achieved and that no unintended side effects occurred.

### 8.1 Automated Validation (Built into Playbook)

Include post-task validation directly in the playbook using `assert` or `wait_for`:

```yaml
# Validate a service is running after handler fires
- name: "validate | Confirm nginx is active"
  ansible.builtin.service_facts:

- name: "validate | Assert nginx service is in running state"
  ansible.builtin.assert:
    that:
      - ansible_facts.services['nginx.service'].state == 'running'
    fail_msg: "nginx failed to start after configuration deployment"
    success_msg: "nginx is running as expected"

# Validate a port is listening
- name: "validate | Confirm nginx is listening on port 80"
  ansible.builtin.wait_for:
    host: "{{ inventory_hostname }}"
    port: 80
    timeout: 30
    state: started
```

### 8.2 Manual Validation Checklist

After every production run, the Execution Operator must manually verify the following:

**Service Health**
- [ ] Target services are in the expected state (`systemctl status <service>`)
- [ ] No unexpected errors in service logs (`journalctl -u <service> --since "10 minutes ago"`)

**Configuration Integrity**
- [ ] Configuration files deployed correctly (`cat /etc/<service>/main.conf`)
- [ ] File permissions and ownership correct (`ls -la /etc/<service>/`)
- [ ] No syntax errors in deployed configuration files (e.g., `nginx -t`, `apache2ctl configtest`)

**Connectivity**
- [ ] Application endpoints return expected responses (`curl -I https://<endpoint>`)
- [ ] Health check URLs return `200 OK`
- [ ] No increase in error rates in application monitoring (Grafana, Datadog, etc.)

**No Regression**
- [ ] Hosts not targeted by `--limit` are unaffected
- [ ] Previously working functionality continues to work (smoke test)

### 8.3 Idempotency Validation

After a successful production run, re-run the playbook immediately in check mode to confirm idempotency:

```bash
ansible-playbook <playbook>.yml \
  -i inventory/production/ \
  --check \
  --vault-password-file ~/.vault_pass
```

- [ ] Check mode re-run shows `changed=0` for all hosts
- [ ] Any `changed` output investigated and justified

> A non-zero `changed` count on the idempotency re-run indicates the playbook has idempotency issues that must be fixed before the next execution.

---

## 9. Rollback Procedure

Rollback steps must be identified and documented **before** every production execution, not after a failure.

### 9.1 Pre-Run Rollback Preparation

Before executing in production:

1. Identify whether a rollback playbook exists for this change. If not, document manual rollback steps.
2. Confirm the previous known-good state is either captured (e.g., config file backed up) or a rollback playbook is tested.
3. Record the git commit SHA of the last known-good playbook state.

```bash
# Record the current commit SHA before making changes
git rev-parse HEAD
```

### 9.2 Automated Rollback (Preferred)

If a rollback playbook exists:

```bash
ansible-playbook rollback_<component>.yml \
  -i inventory/production/ \
  --vault-password-file ~/.vault_pass \
  | tee logs/rollback_$(date +%Y%m%d_%H%M%S).log
```

### 9.3 Manual Rollback Steps

If no rollback playbook exists, the general procedure is:

1. **Stop the affected service** to prevent further errors from propagating.
2. **Restore the backed-up configuration** from the pre-run backup location.
3. **Restart the service** and validate it returns to the known-good state.
4. **Re-run validation checks** from §8.2.
5. **Update the Change Request ticket** with rollback status and root cause.

### 9.4 Rollback Decision Criteria

Initiate rollback immediately if any of the following are observed after execution:

| Condition                                        | Action                       |
|--------------------------------------------------|------------------------------|
| Any host shows `failed=1` or higher in PLAY RECAP | Investigate — rollback if service is impacted |
| Target service is not running post-execution     | Rollback immediately         |
| Error rate increases >5% in monitoring dashboards | Rollback immediately         |
| Health check returns non-200 response            | Rollback immediately         |
| Unexpected configuration drift detected          | Rollback after investigation |

---

## 10. Error Handling and Escalation

### 10.1 Common Errors and Resolution

| Error                                    | Likely Cause                                   | Resolution                                              |
|------------------------------------------|------------------------------------------------|---------------------------------------------------------|
| `UNREACHABLE! Failed to connect`         | SSH key not authorised, host down, firewall     | Verify SSH access manually. Check host status.          |
| `fatal: [host]: FAILED! => {"msg": "Missing sudo password"}` | `become` set but no sudo config | Add host to sudoers or configure `NOPASSWD`             |
| `AnsibleUndefinedVariable`              | Required variable not set in inventory or vars  | Check `defaults/`, `group_vars/`, `host_vars/` for missing key |
| `Vault was used on a file...`           | Vault-encrypted file but no vault password provided | Add `--vault-password-file` or `--ask-vault-pass`       |
| `ansible-lint` profile violation        | Code quality issue in playbook                  | Review lint output, fix flagged tasks before proceeding |
| `changed` count higher than expected    | Unintended configuration drift or non-idempotent task | Investigate diff output. Fix idempotency issue.        |

### 10.2 Escalation Path

If an issue cannot be resolved within **15 minutes** of discovery during a production execution:

1. **Stop the playbook run** if it is still in progress (`Ctrl+C`).
2. **Initiate rollback** per §9 if the system is in a degraded state.
3. **Page the on-call engineer** via the alerting platform (PagerDuty / OpsGenie).
4. **Open a P1 incident ticket** referencing the Change Request.
5. **Post in the `#incidents` Slack channel** with: environment, affected systems, playbook name, and timeline.

---

## 11. Audit and Logging

All playbook executions must produce a durable log for audit and post-incident review.

### 11.1 Log Naming Convention

```
logs/<env>_<playbook_name>_<YYYYMMDD_HHMMSS>.log
```

Examples:
```
logs/production_deploy_app_20250401_143022.log
logs/staging_configure_nginx_20250401_110500.log
logs/rollback_app_20250401_150812.log
```

### 11.2 Minimum Logging Configuration

Ensure `ansible.cfg` in the repository root contains:

```ini
[defaults]
log_path        = logs/ansible.log
display_skipped_hosts = false
stdout_callback = yaml
```

### 11.3 Audit Record Requirements

Each playbook execution must be traceable to:

- [ ] The Git commit SHA of the playbook that was run
- [ ] The user / service account that ran the playbook
- [ ] The timestamp of execution start and end
- [ ] The Change Request ticket number (production)
- [ ] The log file stored in the `logs/` directory

For CI/CD-triggered runs, the pipeline job ID serves as the execution record.

---

## 12. Change Control

### 12.1 Branching and Review

All playbook changes must follow the Git workflow:

```
main (protected)
  └── feature/CS-<ticket>-<short-description>
```

1. Create a feature branch from `main`.
2. Author the playbook changes.
3. Run lint and local tests.
4. Open a Pull Request against `main`.
5. At least **one peer reviewer** must approve.
6. Merge only after all CI checks pass.

### 12.2 Versioning

Playbooks follow **Semantic Versioning** (`MAJOR.MINOR.PATCH`) recorded in the header comment block:

| Change Type                                      | Version Bump  |
|--------------------------------------------------|---------------|
| New play or major restructuring                  | `MAJOR`       |
| New tasks, roles, or handlers added              | `MINOR`       |
| Bug fixes, variable updates, documentation only | `PATCH`       |

### 12.3 Environment Promotion

Changes must be promoted through environments in order:

```
Development → Staging → UAT (if applicable) → Production
```

**Never execute an unvalidated playbook directly in production.**

---

## 13. Glossary

| Term               | Definition                                                                                     |
|--------------------|-----------------------------------------------------------------------------------------------|
| **Playbook**       | A YAML file containing one or more plays that map hosts to roles and tasks                    |
| **Play**           | A single mapping of hosts to tasks within a playbook                                          |
| **Role**           | A reusable, self-contained unit of automation with a standardised directory structure          |
| **Handler**        | A task triggered by notification; runs once at the end of a play                              |
| **Idempotency**    | The property that running a playbook multiple times produces the same end state                |
| **Inventory**      | A file or directory defining the hosts and groups Ansible manages                              |
| **Ansible Vault**  | Ansible's built-in encryption tool for protecting sensitive variables and files                |
| **Check Mode**     | Ansible's dry-run mode — simulates changes without applying them (`--check`)                  |
| **PLAY RECAP**     | The summary table printed at the end of a playbook run showing ok/changed/failed/unreachable counts |
| **Control Node**   | The machine from which Ansible commands and playbooks are executed                             |
| **Managed Node**   | A target host that Ansible configures (also called a remote host)                             |
| **CAB**            | Change Advisory Board — the group that approves production changes                            |
| **SOP**            | Standard Operating Procedure — this document                                                  |

---

## Appendix A — Execution Checklist (Printable)

Use this checklist for every production playbook run.

```
PRE-EXECUTION
  [ ] Prerequisites verified (§4)
  [ ] Required inputs confirmed (§5)
  [ ] Linting passed — zero errors (§7.2)
  [ ] Dry run reviewed — diff output approved (§7.3)
  [ ] Staging execution successful (§7.4)
  [ ] Change Request approved (§7.5)
  [ ] Rollback plan documented (§9.1)
  [ ] On-call engineer notified

EXECUTION
  [ ] Log file path confirmed
  [ ] Run command verified (inventory, limit, vault)
  [ ] Execution monitored in real time
  [ ] PLAY RECAP: failed=0, unreachable=0

POST-EXECUTION
  [ ] Service health validated (§8.2)
  [ ] Idempotency re-run: changed=0 (§8.3)
  [ ] Log file linked to Change Request ticket
  [ ] Change Request closed
  [ ] Stakeholders notified of completion
```

---

## Appendix B — Quick Reference Commands

```bash
# Check Ansible version and config
ansible --version
ansible-config dump --only-changed

# Test connectivity to all hosts in inventory
ansible all -m ping -i inventory/<env>/

# Lint the playbook
ansible-lint <playbook>.yml && yamllint <playbook>.yml

# Dry run with diff
ansible-playbook <playbook>.yml -i inventory/<env>/ --check --diff

# Full execution with logging
ansible-playbook <playbook>.yml \
  -i inventory/<env>/ \
  --vault-password-file ~/.vault_pass \
  | tee logs/<env>_<playbook>_$(date +%Y%m%d_%H%M%S).log

# List all tasks without running them
ansible-playbook <playbook>.yml --list-tasks

# List all hosts that would be targeted
ansible-playbook <playbook>.yml -i inventory/<env>/ --list-hosts

# Idempotency validation re-run
ansible-playbook <playbook>.yml -i inventory/<env>/ --check --vault-password-file ~/.vault_pass
```

---

*This document is version-controlled in the Common Stack repository. Raise a PR against `docs/sop/` to propose changes. All modifications require peer review and Platform Engineering team approval.*
