# SOP Ansible Playbook





## Document Information

| Author          | Created On | Version | L0 Reviewer  | L1 Reviewer  | L2 Reviewer     |
| --------------- | ---------- | ------- | ------------ | ------------ | --------------- |
| Versha Tripathi | 13-04-2026 | v1.0    | Prince Batra | Nikita Joshi | Piyush Upadhyay |

---

## Table of Contents

* [Purpose](#1-purpose)
* [Scope](#2-scope)
* [Prerequisites](#3-prerequisites)
* [Required Inputs](#4-required-inputs)
* [Execution Steps](#5-execution-steps)
* [Validation Checks](#6-validation-checks)
* [Failure Handling, Rollback and Logging](#7-failure-handling-rollback-and-logging)
* [Change Control](#8-change-control)
* [Conclusion](#9-conclusion)
* [Contact Information](#contact-information)
* [References](#references)

---

## 1. Purpose

This SOP provides a structured and standardised approach for executing Ansible playbooks in a controlled and reliable manner. It ensures that every playbook run follows clearly defined steps, uses the correct inputs, and includes proper validation before and after execution. By following this process, teams can reduce deployment risks, maintain consistency across environments, and ensure that automation is predictable, auditable, and safe for production use.

---

## 2. Scope

| In Scope                                           | Out of Scope                        |
| :------------------------------------------------- | :---------------------------------- |
| Execution of Ansible playbooks in all environments | Ad-hoc `ansible` commands           |
| CI/CD-triggered playbook runs                      | Non-Ansible tools (Terraform, Helm) |
| Validation and rollback procedures                 | Local-only development testing      |

---

## 3. Prerequisites

| Requirement          | Command                                                 |
| :------------------- | :------------------------------------------------------ |
| Ansible installed    | `ansible --version`                                     |
| Python available     | `python3 --version`                                     |
| Inventory reachable  | `ansible all -m ping -i inventory/`                     |
| Required collections | `ansible-galaxy collection install -r requirements.yml` |

---

## 4. Required Inputs

Before executing any playbook, it is important to clearly define and verify all required inputs. Incorrect or missing inputs can lead to failed executions or unintended changes in the environment.

| Input        | Description                                       | Example                               |
| :----------- | :------------------------------------------------ | :------------------------------------ |
| Inventory    | Defines target systems where playbook will run    | `-i inventory/production/`            |
| Target Hosts | Limits execution to specific hosts/groups         | `--limit webservers`                  |
| Variables    | Provide dynamic configuration values at runtime   | `-e "env=prod"`                       |
| Vault Access | Required to decrypt sensitive data like passwords | `--vault-password-file ~/.vault_pass` |

**Key Notes:**

* Always verify the correct inventory (staging vs production)
* Ensure variables match the intended environment
* Validate vault access before execution

---

## 5. Execution Steps

### Step 1 — Verify Environment

```bash
ansible all -m ping -i inventory/<env>/
```

### Step 2 — Validate Playbook (Linting)

```bash
ansible-lint <playbook>.yml
yamllint <playbook>.yml
```

Expected: No errors

### Step 3 — Dry Run (Check Mode)

```bash
ansible-playbook <playbook>.yml -i inventory/<env>/ --check --diff
```

Purpose:

* Preview changes
* Identify risks

### Step 4 — Staging Execution

```bash
ansible-playbook <playbook>.yml -i inventory/staging/
```

Verify:

* No failures
* Expected changes only

### Step 5 — Production Execution

```bash
ansible-playbook <playbook>.yml -i inventory/production/
```

Important:

* Monitor execution
* Do not leave unattended



---

## 6. Validation Checks

After execution, verify system health:

| Check           | Command                      |
| :-------------- | :--------------------------- |
| Service status  | `systemctl status <service>` |
| Logs            | `journalctl -u <service>`    |
| Endpoint        | `curl -I <url>`              |
| Config validity | `nginx -t`                   |

### Idempotency Check

```bash
ansible-playbook <playbook>.yml -i inventory/production/ --check
```

Expected: `changed=0`

---

## 7. Failure Handling, Rollback and Logging

### 7.1 Rollback Procedure

| Step | Action                 |
| :--: | :--------------------- |
|   1  | Stop execution         |
|   2  | Run rollback playbook  |
|   3  | Restore configurations |
|   4  | Restart services       |
|   5  | Validate system        |

### 7.2 Error Handling and Escalation

| Error              | Cause            | Fix                |
| :----------------- | :--------------- | :----------------- |
| UNREACHABLE        | SSH issue        | Check connectivity |
| Missing sudo       | Permission issue | Fix sudo access    |
| Undefined variable | Missing input    | Validate variables |

Escalation Steps:

* Stop execution
* Notify on-call engineer
* Initiate rollback if required

### 7.3 Audit and Logging

Logs must include:

* Execution timestamp
* User details
* Playbook version
* Execution output

Example:

```
logs/prod_<date>.log
```

---

## 8. Change Control

Process:

1. Create feature branch
2. Submit PR
3. Get approval
4. Merge after checks

Environment flow:

```
Dev → Staging → Production
```

---

## 9. Conclusion

This SOP ensures that Ansible playbook execution is structured, predictable, and safe. By clearly defining inputs, following execution steps, and performing validation checks, teams can reduce risks and improve automation reliability.

Consistent adherence to this SOP helps maintain system stability and ensures smooth production deployments.

---

## Contact Information

| Name            | Email                                                                                   |
| :-------------- | :-------------------------------------------------------------------------------------- |
| Versha Tripathi | [versha.tripathi.snaatak@mygurukulam.co](mailto:versha.tripathi.snaatak@mygurukulam.co) |

---

## References

| Resource      | Link                                                                                                       |
| :------------ | :--------------------------------------------------------------------------------------------------------- |
| Ansible Docs  | [https://docs.ansible.com](https://docs.ansible.com)                                                       |
| Ansible Vault | [https://docs.ansible.com/ansible/latest/vault_guide](https://docs.ansible.com/ansible/latest/vault_guide) |
| ansible-lint  | [https://ansible.readthedocs.io/projects/lint/](https://ansible.readthedocs.io/projects/lint/)             |

---

<div align="center"></div>
