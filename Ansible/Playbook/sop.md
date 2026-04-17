<div align="center">

# Standard Operating Procedure — Ansible Playbook Execution

### *Common Stack · Infrastructure Automation · Ansible*

</div>

---

## Document Information

| Author | Created On | Version | Last Updated By | Last Edited On | PRE Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|:---|:---|:---:|:---|:---|:---:|:---:|:---:|:---:|
| Versha Tripathi | 13-04-2026 | v1.0 | Versha Tripathi | 13-04-2026 | Team | — | — | — |

---

## Table of Contents

- [Purpose](#1-purpose)
- [Scope](#2-scope)
- [Roles and Responsibilities](#3-roles-and-responsibilities)
- [Prerequisites](#4-prerequisites)
- [Required Inputs](#5-required-inputs)
- [Playbook Structure Standard](#6-playbook-structure-standard)
- [Execution Steps](#7-execution-steps)
- [Validation Checks](#8-validation-checks)
- [Rollback Procedure](#9-rollback-procedure)
- [Error Handling and Escalation](#10-error-handling-and-escalation)
- [Audit and Logging](#11-audit-and-logging)
- [Change Control](#12-change-control)
- [Glossary](#13-glossary)
- [Contact Information](#contact-information)
- [References](#references)

---

## 1. Purpose

This SOP defines the mandatory process for **authoring, reviewing, executing, and validating** Ansible playbooks within the Common Stack infrastructure automation framework, ensuring runs are repeatable, peer-reviewed, auditable, and validated before reaching production.

---

## 2. Scope

| In Scope | Out of Scope |
|:---|:---|
| All Ansible playbooks in the Common Stack repository | Ad-hoc `ansible` commands (log them, no SOP required) |
| Playbook execution against staging, UAT, and production | Molecule / unit tests run locally during development |
| Automated playbook runs via CI/CD pipelines | Terraform, Helm, or other IaC tooling |
| Role-level changes affecting multiple playbooks | Read-only inventory operations |

---

## 3. Roles and Responsibilities

| Role | Responsibility |
|:---|:---|
| **Playbook Author** | Writes, lints, and unit-tests the playbook. Opens the PR. Fills in the Run Request form. |
| **Peer Reviewer** | Reviews logic, idempotency, and variable hygiene. Approves or requests changes on PR. |
| **Execution Operator** | Runs the playbook after all approvals. Must not be the Author for production runs. |
| **Change Approver** | Approves the Change Request ticket (CAB or designated approver). Required for production only. |
| **Incident Responder** | Owns rollback and escalation if execution fails. Usually the on-call engineer. |

> **Separation of duty:** For production environments, the Author and Execution Operator **must** be different individuals.

---

## 4. Prerequisites

### 4.1 System Prerequisites

| Requirement | Check Command |
|:---|:---|
| Ansible `>= 2.14` installed | `ansible --version` |
| Python `>= 3.9` available | `python3 --version` |
| Required collections installed | `ansible-galaxy collection install -r requirements.yml` |
| SSH connectivity to all target hosts | `ansible all -m ping -i inventory/` |
| Minimum 500 MB free disk on control node | `df -h` |

### 4.2 Access Prerequisites

| Requirement | Notes |
|:---|:---|
| SSH key-based access to target hosts | No password prompts |
| Vault password or token available | Required if playbook references encrypted variables |
| Sudo / `become: true` confirmed working | Test manually before execution |
| Read access to Common Stack Git repository | Confirm clone and pull work |

### 4.3 Process Prerequisites

| Requirement | Notes |
|:---|:---|
| Playbook passed all linting checks | See §7 Step 2 |
| Playbook peer-reviewed and PR approved | — |
| Playbook executed successfully in staging | Mandatory before production |
| Change Request raised and approved | Production only |
| Maintenance window scheduled and communicated | If service-impacting |
| Rollback plan documented | See §9 |

---

## 5. Required Inputs

### 5.1 Inventory

Always specify inventory explicitly — never rely on `/etc/ansible/hosts`.

| Input | Description | Example |
|:---|:---|:---|
| `inventory` | Path to inventory file or directory | `-i inventory/production/` |
| Target hosts | Specific host or group to limit the run | `--limit webservers` |

### 5.2 Variable Sources

| Source | File / Flag | Priority |
|:---|:---|:---:|
| Extra vars (CLI) | `-e "key=value"` or `-e @vars_file.yml` | 1 (highest) |
| Playbook `vars:` | Inline in play definition | 2 |
| Role `vars/main.yml` | Internal role constants | 3 |
| Host vars | `inventory/host_vars/<hostname>.yml` | 4 |
| Group vars | `inventory/group_vars/<group>.yml` | 5 |
| Role `defaults/main.yml` | Overridable defaults | 6 (lowest) |

### 5.3 Vault

| Method | Command | Recommended For |
|:---|:---|:---|
| Vault password file | `--vault-password-file ~/.vault_pass` | CI/CD pipelines |
| Interactive prompt | `--ask-vault-pass` | Human-run executions |

> Vault password file permissions must be `600`. Never commit it to the repository.

### 5.4 Execution Flags Reference

| Flag | Purpose |
|:---|:---|
| `-i inventory/<env>/` | Target environment inventory |
| `--limit <host>` | Scope run to specific host or group |
| `--tags <tag>` | Run only tagged tasks |
| `--skip-tags <tag>` | Skip tagged tasks |
| `--check --diff` | Dry run with diff output |
| `--vault-password-file <path>` | Non-interactive vault decryption |
| `-v / -vv / -vvv` | Increase verbosity (`-vv` for debugging) |
| `--start-at-task "<name>"` | Resume from a specific task (use with caution) |
| `--step` | Prompt before each task (interactive review) |

---

## 6. Playbook Structure Standard

### 6.1 Required Header Block

Every playbook must begin with:

```yaml
---
# =============================================================================
# Playbook   : <descriptive name>
# Description: <one or two sentences>
# Author     : <name or team>
# Version    : <semver>
# Last Update: <YYYY-MM-DD>
# Ticket     : <JIRA / GitHub issue reference>
# Usage      : ansible-playbook <playbook>.yml -i inventory/<env>/
# =============================================================================
```

### 6.2 Standards Summary

| Standard | Requirement |
|:---|:---|
| Play `name` | Human-readable, specific |
| `hosts` value | Always parameterise — `"{{ target_hosts \| default('app') }}"` |
| `become` | Declare explicitly, even if `false` |
| `gather_facts` | Declare explicitly |
| Task naming | Sentence case, prefixed with component — `"nginx \| Deploy config"` |
| Idempotency | All tasks must be idempotent; use `creates:`, `when:`, or `assert` guards |

---

## 7. Execution Steps

### Step 1 — Verify Prerequisites

```bash
ansible --version
ansible-galaxy collection list
ansible all -m ping -i inventory/<env>/
```

### Step 2 — Lint and Static Analysis

```bash
ansible-lint <playbook>.yml
yamllint <playbook>.yml
```

Expected: `0 failure(s), 0 warning(s)` — **do not proceed if linting fails.**

### Step 3 — Dry Run (Check Mode)

```bash
ansible-playbook <playbook>.yml -i inventory/<env>/ --check --diff \
  [--limit <host>] [--vault-password-file ~/.vault_pass]
```

| Check | Expected |
|:---|:---|
| `changed` tasks | Only intentional changes shown |
| `fatal` errors | None |
| `--diff` output | All file changes reviewed and approved |
| Host count in PLAY RECAP | Matches expected target count |

### Step 4 — Staging Execution (Mandatory)

```bash
ansible-playbook <playbook>.yml -i inventory/staging/ \
  --vault-password-file ~/.vault_pass \
  | tee logs/staging_$(date +%Y%m%d_%H%M%S).log
```

| Check | Expected |
|:---|:---|
| `failed` tasks | 0 |
| `changed` count | Within expected range |
| Services / components | Verified working in staging |

### Step 5 — Change Request Approval (Production Only)

| Requirement | Status |
|:---|:---|
| Change Request in **Approved** status | — |
| Maintenance window active | — |
| On-call engineer notified and available | — |
| Rollback procedure reviewed | See §9 |

**Do not proceed to Step 6 without Change Request approval.**

### Step 6 — Production Execution

```bash
ansible-playbook <playbook>.yml -i inventory/production/ \
  --vault-password-file ~/.vault_pass \
  [--limit <host>] \
  | tee logs/production_$(date +%Y%m%d_%H%M%S).log
```

> Monitor output in real time. Do not leave an unattended production run.

### Step 7 — Post-Execution Review

```bash
grep -A 10 "PLAY RECAP" logs/production_<timestamp>.log
grep -E "failed=[^0]|unreachable=[^0]" logs/production_<timestamp>.log
```

| Check | Expected |
|:---|:---|
| `failed` | 0 for all hosts |
| `unreachable` | 0 for all hosts |
| Log file | Saved and linked to Change Request |

---

## 8. Validation Checks

### 8.1 Service Health

| Check | Command |
|:---|:---|
| Service state | `systemctl status <service>` |
| Service logs | `journalctl -u <service> --since "10 minutes ago"` |
| Config syntax | `nginx -t` / `apache2ctl configtest` |
| File permissions | `ls -la /etc/<service>/` |
| Endpoint response | `curl -I https://<endpoint>` |

### 8.2 Idempotency Validation

Re-run immediately in check mode after a successful production run:

```bash
ansible-playbook <playbook>.yml -i inventory/production/ --check \
  --vault-password-file ~/.vault_pass
```

Expected: `changed=0` for all hosts. Any non-zero count must be investigated.

---

## 9. Rollback Procedure

### 9.1 Rollback Decision Criteria

| Condition | Action |
|:---|:---|
| Any host shows `failed=1` or higher | Investigate — rollback if service is impacted |
| Target service not running post-execution | Rollback immediately |
| Error rate increases >5% in monitoring | Rollback immediately |
| Health check returns non-200 response | Rollback immediately |
| Unexpected configuration drift detected | Rollback after investigation |

### 9.2 Automated Rollback (Preferred)

```bash
ansible-playbook rollback_<component>.yml -i inventory/production/ \
  --vault-password-file ~/.vault_pass \
  | tee logs/rollback_$(date +%Y%m%d_%H%M%S).log
```

### 9.3 Manual Rollback Steps

| Step | Action |
|:---:|:---|
| 1 | Stop the affected service |
| 2 | Restore backed-up configuration from pre-run location |
| 3 | Restart the service and validate known-good state |
| 4 | Re-run validation checks from §8 |
| 5 | Update the Change Request ticket with rollback status and root cause |

---

## 10. Error Handling and Escalation

### 10.1 Common Errors

| Error | Likely Cause | Resolution |
|:---|:---|:---|
| `UNREACHABLE! Failed to connect` | SSH not authorised, host down, firewall | Verify SSH access manually; check host status |
| `Missing sudo password` | `become` set but no sudoers config | Add host to sudoers or configure `NOPASSWD` |
| `AnsibleUndefinedVariable` | Required variable not set | Check `defaults/`, `group_vars/`, `host_vars/` for missing key |
| `Vault was used on a file...` | No vault password provided | Add `--vault-password-file` or `--ask-vault-pass` |
| `ansible-lint` profile violation | Code quality issue | Review lint output and fix before proceeding |
| `changed` count higher than expected | Configuration drift or non-idempotent task | Investigate diff output; fix idempotency issue |

### 10.2 Escalation Path

If an issue cannot be resolved within **15 minutes** during a production execution:

| Step | Action |
|:---:|:---|
| 1 | Stop the playbook run (`Ctrl+C`) |
| 2 | Initiate rollback per §9 if system is degraded |
| 3 | Page the on-call engineer via PagerDuty / OpsGenie |
| 4 | Open a P1 incident ticket referencing the Change Request |
| 5 | Post in `#incidents` Slack: environment, affected systems, playbook name, timeline |

---

## 11. Audit and Logging

### 11.1 Log Naming Convention

```
logs/<env>_<playbook_name>_<YYYYMMDD_HHMMSS>.log
```

### 11.2 Minimum `ansible.cfg` Configuration

```ini
[defaults]
log_path              = logs/ansible.log
display_skipped_hosts = false
stdout_callback       = yaml
```

### 11.3 Audit Requirements

| Required Record | Source |
|:---|:---|
| Git commit SHA of playbook executed | `git rev-parse HEAD` |
| User / service account that ran the playbook | Shell history / CI job |
| Execution start and end timestamp | Log file |
| Change Request ticket number | Production runs only |
| Log file location | `logs/` directory |

---

## 12. Change Control

### 12.1 Branching and Review

| Step | Action |
|:---:|:---|
| 1 | Create feature branch from `main` — `feature/CS-<ticket>-<description>` |
| 2 | Author playbook changes |
| 3 | Run lint and local tests |
| 4 | Open Pull Request against `main` |
| 5 | At least one peer reviewer must approve |
| 6 | Merge only after all CI checks pass |

### 12.2 Versioning

| Change Type | Version Bump |
|:---|:---:|
| New play or major restructuring | `MAJOR` |
| New tasks, roles, or handlers added | `MINOR` |
| Bug fixes, variable updates, documentation only | `PATCH` |

### 12.3 Environment Promotion

```
Development → Staging → UAT (if applicable) → Production
```

**Never execute an unvalidated playbook directly in production.**

---

## 13. Glossary

| Term | Definition |
|:---|:---|
| **Playbook** | A YAML file containing one or more plays that map hosts to roles and tasks |
| **Play** | A single mapping of hosts to tasks within a playbook |
| **Role** | A reusable, self-contained unit of automation with a standardised directory structure |
| **Handler** | A task triggered by notification; runs once at the end of a play |
| **Idempotency** | The property that running a playbook multiple times produces the same end state |
| **Inventory** | A file or directory defining the hosts and groups Ansible manages |
| **Ansible Vault** | Ansible's built-in encryption tool for protecting sensitive variables and files |
| **Check Mode** | Ansible's dry-run mode — simulates changes without applying them (`--check`) |
| **PLAY RECAP** | Summary table at the end of a run showing ok / changed / failed / unreachable counts |
| **Control Node** | The machine from which Ansible commands and playbooks are executed |
| **Managed Node** | A target host that Ansible configures |
| **CAB** | Change Advisory Board — the group that approves production changes |
| **SOP** | Standard Operating Procedure — this document |

---

## Contact Information

| Name | Email |
|:---|:---|
| Versha Tripathi | [versha.tripathi.snaatak@mygurukulam.co](mailto:versha.tripathi.snaatak@mygurukulam.co) |

---

## References

| # | Resource | Link |
|:---:|:---|:---|
| 1 | Ansible Playbooks Documentation | [docs.ansible.com — Playbooks](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks.html) |
| 2 | Ansible Vault Documentation | [docs.ansible.com — Vault](https://docs.ansible.com/ansible/latest/vault_guide/index.html) |
| 3 | ansible-lint Documentation | [ansible.readthedocs.io — ansible-lint](https://ansible.readthedocs.io/projects/lint/) |
| 4 | Molecule — Role Testing Framework | [molecule.readthedocs.io](https://molecule.readthedocs.io/en/latest/) |
| 5 | Variable Precedence Reference | [docs.ansible.com — Variable Precedence](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_variables.html#understanding-variable-precedence) |
| 6 | Ansible Check Mode | [docs.ansible.com — Check Mode](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_checkmode.html) |

---

<div align="center">



</div>
