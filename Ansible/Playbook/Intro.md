# Ansible Playbook SOP

<p align="center">
  <img src="https://upload.wikimedia.org/wikipedia/commons/2/24/Ansible_logo.svg" alt="Ansible Logo" width="100"/>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/automation-ansible-red" />
  <img src="https://img.shields.io/badge/configuration-management-blue" />
  <img src="https://img.shields.io/badge/type-infrastructure--as--code-green" />
  <img src="https://img.shields.io/badge/platform-linux-lightgrey" />
  <img src="https://img.shields.io/badge/status-production--ready-brightgreen" />
</p>

| Author       | Created on | Version | Last updated by | Last edited on | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
| ------------ | ---------- | ------- | --------------- | -------------- | ------------ | ----------- | ----------- | ----------- |
| Mukesh Kharb | 17/04/2026 | 1.0     | Mukesh Kharb    | 17/04/2026     | Team         | Mohit Kumar |Faisal Khan  | Mahesh Kumar| 

---

## Table of Contents

* [Introduction](#introduction)
* [What is Ansible Playbook](#what-is-ansible-playbook)
* [Why Use Playbooks](#why-use-playbooks)
* [Core Concepts](#core-concepts)
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

In modern infrastructure management, manual execution of repetitive tasks such as package installation, service configuration, and system setup increases the risk of human error and inconsistency.

Ansible Playbooks provide a structured and automated approach to define these operations as code. By describing the desired state of systems, playbooks enable consistent, repeatable, and scalable execution across multiple environments.

This approach ensures reliability, reduces operational overhead, and aligns with Infrastructure as Code (IaC) practices used in DevOps workflows.

---

<a id="what-is-ansible-playbook"></a>

## What is Ansible Playbook

> An Ansible Playbook is a YAML-based automation file used to define and execute a series of tasks on managed systems in a predictable and repeatable way.

| Aspect              | Description                                                                |
|--------------------|-----------------------------------------------------------------------------|
| Approach           | Declarative (defines desired state, not step-by-step execution)             |
| Purpose            | Automates system configuration and infrastructure management                |

---

## Key Characteristics

| Feature              | Benefit                                      |
|---------------------|----------------------------------------------|
| Idempotency         | Safe to run multiple times                   |
| Readability         | Easier to understand and maintain            |
| Scalability         | Suitable for large-scale automation          |
---

<a id="why-use-playbooks"></a>

## Why Use Playbooks

### Key Reasons

| Feature                     | Reason                                                                 |
|----------------------------|-------------------------------------------------------------------------|
| Idempotency                | Safe to run multiple times without unintended changes                  |
| Readability                | Easy to understand and maintain                                        |
| Scalability                | Suitable for large-scale automation across multiple systems            |
| Automation at Scale        | Configure hundreds of servers with a single command                    |
| Consistency                | Ensures standardized configuration across environments                 |
| Version Control Friendly   | Supports tracking, auditing, and rollback using Git                    |
| Faster Deployment          | Quickly recreate environments and recover systems                      |
| Reduced Human Error        | Minimizes manual mistakes in repetitive operations                     |

---

<a id="core-concepts"></a>

## Core Concepts

| Concept    | Description                      |
|------------|----------------------------------|
| Inventory  | List of hosts                    |
| Module     | Unit of work                     |
| Task       | Single action                    |
| Play       | Group of tasks                   |
| Playbook   | Collection of plays              |

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
ansible-playbook -i inventory.ini playbook.yml
```
Uses custom inventory file.
><img width="1407" height="676" alt="image" src="https://github.com/user-attachments/assets/38f22f6a-5189-4f03-9e73-6aa3e9a8c42b" />

```bash
ansible-playbook playbook.yml --check
```
Performs dry run.
><img width="1400" height="525" alt="image" src="https://github.com/user-attachments/assets/535e0417-af3f-4dee-9aff-ba3ced2684a4" />

```bash
ansible-playbook -i inventory.ini playbook.yml --syntax-check
```
Checks YAML syntax.
><img width="1335" height="213" alt="image" src="https://github.com/user-attachments/assets/d63f216e-ea62-4947-b720-19322ae3f300" />

```bash
ansible-playbook -i inventory.ini playbook.yml -vv
```
Shows detailed logs.
><img width="1371" height="874" alt="image" src="https://github.com/user-attachments/assets/297e5972-8bce-4519-9a9f-2ddfa5d32cdb" />

---

<a id="best-practices"></a>

## Best Practices

| Practice                | Description                                      |
|------------------------|--------------------------------------------------|
| Use Roles              | Organize large setups into reusable components    |
| Avoid Hardcoding       | Use variables instead of fixed values             |
| Test Before Production | Validate playbooks in staging environments        |
| Keep Modular           | Break playbooks into smaller, manageable parts    |

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

| Resource            | Link                                                                 |
|---------------------|----------------------------------------------------------------------|
| Ansible Docs        | https://docs.ansible.com/ansible/latest/playbook_guide/index.html     |
| Playbook Intro      | https://docs.ansible.com/ansible/latest/user_guide/playbooks_intro.html |
| GeeksforGeeks       | https://www.geeksforgeeks.org/ansible-playbooks/                      |
| Red Hat             | https://www.redhat.com/en/topics/automation/what-is-an-ansible-playbook |

---

## Contact Information

| Name          | Email                                      |
|--------------|--------------------------------------------|
| Mukesh Kharb | mukesh.Kharb.snaatak@mygurukulam.co        |

---
