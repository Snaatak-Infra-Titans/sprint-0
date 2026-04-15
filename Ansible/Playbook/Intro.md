# Ansible Playbook SOP

---

| Author       | Created on | Version | Last updated by | Last edited on | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
| ------------ | ---------- | ------- | --------------- | -------------- | ------------ | ----------- | ----------- | ----------- |
| Mukesh Kharb | 2026-04-15 | 1.0     | Mukesh Kharb    | 2026-04-15     | Team         |             |             |             |

---

## Table of Contents

* [Introduction](#introduction)
* [What is Ansible Playbook](#what-is-ansible-playbook)
* [Why Use Playbooks](#why-use-playbooks)
* [How Playbooks Work](#how-playbooks-work)
* [Core Concepts](#core-concepts)
* [Difference: Task vs Play vs Playbook](#difference-task-vs-play-vs-playbook)
* [Example Playbook](#example-playbook)
* [Execution Workflow](#execution-workflow)
* [Common Playbook Commands](#common-playbook-commands)
* [Best Practices](#best-practices)
* [Troubleshooting](#troubleshooting)
* [Summary](#summary)
* [References](#references)

---

<a id="introduction"></a>

## Introduction

> [!NOTE]
> This section explains what playbooks are and why they are important.

While working with infrastructure, performing tasks manually (like installing packages or configuring services) can be repetitive and error-prone.

Ansible Playbooks allow us to define these steps as code so they can be executed consistently across multiple systems.

---

<a id="what-is-ansible-playbook"></a>

## What is Ansible Playbook

> [!IMPORTANT]
> An Ansible Playbook is a YAML-based automation file used to define and execute a series of tasks on managed systems in a predictable and repeatable way.

Ansible Playbooks act as the **core automation engine** in Ansible. Instead of manually configuring systems, you describe the desired state of infrastructure in a playbook, and Ansible ensures that state is achieved.

A playbook contains:

* **Plays** → define which hosts to target
* **Tasks** → define what actions to perform
* **Modules** → actual units that execute tasks

Unlike scripts, playbooks are **declarative**, meaning you describe *what the system should look like*, not how to achieve it step by step.

This makes playbooks:

* Easier to understand
* Safer to run multiple times
* Ideal for automation at scale

---

<a id="why-use-playbooks"></a>

## Why Use Playbooks

> [!TIP]
> Playbooks are used to bring consistency, automation, and control to infrastructure management.

In real-world environments, managing multiple servers manually is not practical. Even small differences in configuration can lead to failures, downtime, or inconsistent behavior.

Playbooks solve this problem by providing a **single source of truth** for system configuration.

### Key Reasons

* **Automation at Scale**
  - Execute the same configuration across hundreds of servers with a single command.

* **Consistency and Standardization**
  - Ensures all systems follow the same configuration, reducing environment drift.

* **Idempotency (Safe Re-runs)**
  - Playbooks only make changes when required, avoiding unnecessary modifications.

* **Version Control Friendly**
  - Playbooks can be stored in Git, allowing tracking, auditing, and rollback of changes.

* **Faster Deployment and Recovery**
  - Entire environments can be recreated quickly using playbooks.

* **Reduced Human Error**
  - Eliminates manual mistakes in repetitive operations.

---

<a id="how-playbooks-work"></a>

## How Playbooks Work

> [!IMPORTANT]
> Ansible executes playbooks in a structured and sequential manner to achieve the desired system state.

When you run a playbook, Ansible performs the following steps:

1. **Reads the Playbook File**
   - Parses the YAML file and identifies plays, hosts, and tasks.

2. **Connects to Target Hosts**
   - Uses SSH (or other protocols) to connect to systems defined in the inventory.

3. **Gathers System Facts (Optional)**
   - Collects information about the system (OS, IP, memory, etc.) for conditional logic.

4. **Executes Tasks Sequentially**
   - Tasks run in the exact order they are defined in the play.

5. **Uses Modules for Execution**
   - Each task calls a module (like apt, service, copy) to perform the action.

6. **Ensures Idempotency**
   - Before making changes, Ansible checks current state and applies changes only if needed.

7. **Reports Results**
   - Provides output showing which tasks changed, failed, or were skipped.

---

<a id="core-concepts"></a>

## Core Concepts

* **Inventory** → List of hosts
* **Module** → Unit of work
* **Task** → Single action
* **Play** → Group of tasks
* **Playbook** → Collection of plays

---

<a id="difference-task-vs-play-vs-playbook"></a>

## Difference: Task vs Play vs Playbook

| Component | Description         | Example          |
| --------- | ------------------- | ---------------- |
| Task      | Single action       | Install nginx    |
| Play      | Group of tasks      | Configure server |
| Playbook  | Collection of plays | Full deployment  |

---

<a id="example-playbook"></a>

## Example Playbook

```yaml
- name: Setup Web Server
  hosts: all
  become: yes

  tasks:
    - name: Update packages
      apt:
        update_cache: yes

    - name: Install nginx
      apt:
        name: nginx
        state: present

    - name: Ensure nginx is running
      service:
        name: nginx
        state: started
```

### Explanation

* Runs on all hosts
* Uses sudo privileges
* Updates packages, installs nginx, and starts service

---

<a id="execution-workflow"></a>

## Execution Workflow

```text
Write Playbook
        ↓
Run ansible-playbook
        ↓
Connect to Hosts
        ↓
Execute Tasks
        ↓
System Configured
```

---

<a id="common-playbook-commands"></a>

## Common Playbook Commands

```bash
ansible-playbook playbook.yml
```

Runs playbook on target hosts.

```bash
ansible-playbook -i inventory.ini playbook.yml
```

Uses custom inventory file.

```bash
ansible-playbook playbook.yml --check
```

Performs dry run.

```bash
ansible-playbook playbook.yml --syntax-check
```

Checks YAML syntax.

```bash
ansible-playbook playbook.yml --limit web
```

Runs only on specific hosts.

```bash
ansible-playbook playbook.yml -vvv
```

Shows detailed logs.

---

<a id="best-practices"></a>

## Best Practices

* Use roles for large setups
* Avoid hardcoding values
* Test before production
* Keep playbooks modular

---

<a id="troubleshooting"></a>

## Troubleshooting

| Issue             | Cause        | Solution         |
| ----------------- | ------------ | ---------------- |
| Host unreachable  | SSH issue    | Check connection |
| Permission denied | No sudo      | Use become       |
| YAML error        | Wrong format | Fix indentation  |

---

<a id="summary"></a>

## Summary

* Playbooks automate infrastructure tasks
* Ensure consistency across environments
* Easy to manage and reuse
* Core DevOps automation tool

---

<a id="references"></a>

## References

* [https://docs.ansible.com/ansible/latest/playbook_guide/index.html](https://docs.ansible.com/ansible/latest/playbook_guide/index.html)
* [https://docs.ansible.com/ansible/latest/user_guide/playbooks_intro.html](https://docs.ansible.com/ansible/latest/user_guide/playbooks_intro.html)
* [https://www.geeksforgeeks.org/ansible-playbooks/](https://www.geeksforgeeks.org/ansible-playbooks/)
* [https://www.redhat.com/en/topics/automation/what-is-an-ansible-playbook](https://www.redhat.com/en/topics/automation/what-is-an-ansible-playbook)

---
