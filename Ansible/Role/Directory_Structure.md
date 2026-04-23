<div align="center">

# Ansible Role Directory Structure

### *A reference guide for every directory and file in a standard Ansible role*

</div>

---

## Document Information

| Author          | Created On | Version | L0 Reviewer  | L1 Reviewer  | L2 Reviewer     |
| --------------- | ---------- | ------- | ------------ | ------------ | --------------- |
| Versha Tripathi | 13-04-2026 | v1.0    | Prince Batra | Nikita Joshi | Piyush Upadhyay |

---

## Table of Contents

- [Overview](#overview)
- [Directory Tree](#directory-tree)
- [Directory Reference](#directory-reference)
- [Variable Precedence](#variable-precedence)
- [How Ansible Loads a Role](#how-ansible-loads-a-role)
- [Quick Reference](#quick-reference)
- [Contact Information](#contact-information)
- [References](#references)

---

## Overview

An **Ansible Role** is a self-contained, reusable unit of automation that groups related tasks, variables, templates, files, and handlers into a well-defined directory structure. Roles allow you to break large playbooks into manageable, portable components that can be shared across projects and teams.

The standard role skeleton is generated via:

```bash
ansible-galaxy role init <role_name>
```

---

## Directory Tree

```
roles/
└── <role_name>/
    ├── defaults/
    │   └── main.yml
    ├── files/
    ├── handlers/
    │   └── main.yml
    ├── meta/
    │   └── main.yml
    ├── tasks/
    │   └── main.yml
    ├── templates/
    ├── tests/
    │   ├── inventory
    │   └── test.yml
    └── vars/
        └── main.yml
```

---

## Directory Reference

| Directory | Purpose | Key File | Module Used |
|:---|:---|:---:|:---:|
| `tasks/` | Main automation logic — what the role *does* | `main.yml` | Any |
| `defaults/` | Default variables, lowest precedence, overridable by callers | `main.yml` | — |
| `vars/` | Internal role constants, high precedence, not for override | `main.yml` | — |
| `handlers/` | Triggered tasks (e.g. service restarts), run once at play end when notified | `main.yml` | `service`, `command` |
| `templates/` | Jinja2 `.j2` files rendered with variables at runtime | `*.j2` | `template` |
| `files/` | Static files copied to target hosts without modification | any | `copy` |
| `meta/` | Role metadata, Galaxy info, and dependency declarations | `main.yml` | — |
| `tests/` | Minimal test inventory and playbook for local role testing | `test.yml` | — |

### Key Rules

| Rule | Detail |
|:---|:---|
| File needs variable substitution? | Use `templates/` with `.j2` extension |
| File is static, copied as-is? | Use `files/` |
| Variable should be overridden by users? | Define in `defaults/` |
| Variable is an internal constant? | Define in `vars/` |
| Task runs only after a change? | Define in `handlers/` using `notify` |
| Handler name must match | Exactly match the string used in the `notify` directive |
| Dependencies always run first | Declared in `meta/main.yml` under `dependencies` |
| `tests/` is never auto-loaded | Must be invoked manually or via Molecule |

---

## Variable Precedence

| Directory | Precedence | Intended Author | Overridable by Users? |
|:---|:---:|:---|:---:|
| `defaults/` | Lowest | Role author (defaults) | Yes — intentionally |
| `vars/` | High | Role author (constants) | No — internal only |

---

## How Ansible Loads a Role

| Order | Source | What Happens |
|:---:|:---|:---|
| 1 | `meta/main.yml` | Resolves and runs role dependencies |
| 2 | `defaults/main.yml` | Loads default variables |
| 3 | `vars/main.yml` | Loads role variables (overrides defaults) |
| 4 | `tasks/main.yml` | Executes role tasks |
| 5 | `handlers/main.yml` | Registers handlers (run at play end when notified) |
| 6 | `templates/` & `files/` | Made available for `template` and `copy` modules |
| 7 | `tests/` | Never auto-loaded — manually invoked for testing |

---

## Quick Reference

| Task | Directory | Command / Module |
|:---|:---:|:---|
| Install, configure, start a service | `tasks/` | Any Ansible module |
| Deploy a config file with variables | `templates/` | `ansible.builtin.template` |
| Copy a static file or certificate | `files/` | `ansible.builtin.copy` |
| Restart a service after config change | `handlers/` | `ansible.builtin.service` |
| Set a user-overridable default | `defaults/` | — |
| Set an internal constant | `vars/` | — |
| Declare a role dependency | `meta/` | — |
| Test the role locally | `tests/` | `ansible-playbook` or Molecule |

---

## Contact Information

| Name | Email |
|:---|:---|
| Versha Tripathi | [versha.tripathi.snaatak@mygurukulam.co](mailto:versha.tripathi.snaatak@mygurukulam.co) |

---

## References

| # | Resource | Link |
|:---:|:---|:---|
| 1 | Ansible Roles Documentation | [docs.ansible.com — Roles](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_roles.html) |
| 2 | Ansible Galaxy — Publishing Roles | [galaxy.ansible.com — Contributing](https://galaxy.ansible.com/docs/contributing/creating_role.html) |
| 3 | Molecule — Role Testing Framework | [molecule.readthedocs.io](https://molecule.readthedocs.io/en/latest/) |
| 4 | Variable Precedence Reference | [docs.ansible.com — Variable Precedence](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_variables.html#understanding-variable-precedence) |

---

<div align="center">



</div>
