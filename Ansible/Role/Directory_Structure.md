

# Ansible Role Directory Structure


---

## Document Information

| Author          | Created On | Version | L0 Reviewer  | L1 Reviewer  | L2 Reviewer     |
| --------------- | ---------- | ------- | ------------ | ------------ | --------------- |
| Versha Tripathi | 13-04-2026 | v1.0    | Prince Batra | Nikita Joshi | Piyush Upadhyay |

---

## Table of Contents

* [Overview](#overview)
* [Directory Tree](#directory-tree)
* [Directory Reference](#directory-reference)
* [Variable Precedence](#variable-precedence)
* [How Ansible Loads a Role](#how-ansible-loads-a-role)
* [Quick Reference](#quick-reference)
* [Conclusion](#conclusion)
* [Contact Information](#contact-information)
* [References](#references)

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

| Directory    | Purpose                                                       | When to Use                                      |  Key File  |      Module Used     |
| :----------- | :------------------------------------------------------------ | :----------------------------------------------- | :--------: | :------------------: |
| `tasks/`     | Contains the main automation logic (step-by-step execution)   | When defining what the role actually does        | `main.yml` |      Any module      |
| `defaults/`  | Stores default values for variables (lowest priority)         | When values should be easily overridden by users | `main.yml` |           —          |
| `vars/`      | Stores fixed/internal variables (high priority)               | When values should NOT be overridden             | `main.yml` |           —          |
| `handlers/`  | Defines tasks triggered by changes (like restarting services) | When an action should run only after a change    | `main.yml` | `service`, `command` |
| `templates/` | Stores dynamic files with variables using Jinja2              | When config files need runtime customization     |   `*.j2`   |      `template`      |
| `files/`     | Stores static files copied as-is                              | When no variable substitution is needed          |     any    |        `copy`        |
| `meta/`      | Contains role metadata and dependencies                       | When defining role dependencies or Galaxy info   | `main.yml` |           —          |
| `tests/`     | Used for testing roles locally                                | When validating role behavior before production  | `test.yml` |           —          |

### Key Rules

| Rule                                    | Detail                                    |
| :-------------------------------------- | :---------------------------------------- |
| File needs variable substitution?       | Use `templates/` with `.j2`               |
| File is static, copied as-is?           | Use `files/`                              |
| Variable should be overridden by users? | Define in `defaults/`                     |
| Variable is an internal constant?       | Define in `vars/`                         |
| Task runs only after a change?          | Define in `handlers/` using `notify`      |
| Handler name must match                 | Exactly match the string used in `notify` |
| Dependencies always run first           | Defined in `meta/main.yml`                |
| `tests/` is never auto-loaded           | Must be run manually                      |

---

## Variable Precedence

| Directory   | Precedence | Intended Author | Overridable by Users? |
| :---------- | :--------: | :-------------- | :-------------------: |
| `defaults/` |   Lowest   | Role author     |          Yes          |
| `vars/`     |    High    | Role author     |           No          |

---

## How Ansible Loads a Role

### Flow Diagram

<div align="center">

```
Start
  ↓
Load meta/main.yml (dependencies)
  ↓
Load defaults/main.yml (default variables)
  ↓
Load vars/main.yml (override defaults)
  ↓
Execute tasks/main.yml
  ↓
Register handlers/main.yml
  ↓
Use templates/ and files/ when required
  ↓
Run handlers (if notified)
  ↓
End
```

</div>

---

## Quick Reference

| Task                                  |   Directory  | Command / Module               |
| :------------------------------------ | :----------: | :----------------------------- |
| Install, configure, start a service   |   `tasks/`   | Any Ansible module             |
| Deploy a config file with variables   | `templates/` | `ansible.builtin.template`     |
| Copy a static file or certificate     |   `files/`   | `ansible.builtin.copy`         |
| Restart a service after config change |  `handlers/` | `ansible.builtin.service`      |
| Set a user-overridable default        |  `defaults/` | —                              |
| Set an internal constant              |    `vars/`   | —                              |
| Declare a role dependency             |    `meta/`   | —                              |
| Test the role locally                 |   `tests/`   | `ansible-playbook` or Molecule |

---

## Conclusion

Ansible roles provide a clean and standardized way to organize automation code. By understanding each directory and its purpose, you can build roles that are **modular, reusable, and easy to maintain**.

For beginners, focusing on `tasks/`, `templates/`, and `handlers/` is a great starting point. As you grow, mastering variable precedence and role dependencies will help you design more scalable and production-ready automation.

> A well-structured role not only simplifies automation but also improves collaboration across teams.

---

## Contact Information

| Name            | Email                                                                                   |
| :-------------- | :-------------------------------------------------------------------------------------- |
| Versha Tripathi | [versha.tripathi.snaatak@mygurukulam.co](mailto:versha.tripathi.snaatak@mygurukulam.co) |

---

## References

|  #  | Resource                          | Link                                                                                                                                                                                                                                   |
| :-: | :-------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|  1  | Ansible Roles Documentation       | [https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_roles.html](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_roles.html)                                                                 |
|  2  | Ansible Galaxy — Publishing Roles | [https://galaxy.ansible.com/docs/contributing/creating_role.html](https://galaxy.ansible.com/docs/contributing/creating_role.html)                                                                                                     |
|  3  | Molecule — Role Testing Framework | [https://molecule.readthedocs.io/en/latest/](https://molecule.readthedocs.io/en/latest/)                                                                                                                                               |
|  4  | Variable Precedence Reference     | [https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_variables.html#understanding-variable-precedence](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_variables.html#understanding-variable-precedence) |

---

<div align="center"></div>
