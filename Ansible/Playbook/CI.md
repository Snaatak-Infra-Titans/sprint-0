<p align="center">
  <img width="200" height="200" alt="image" src="https://github.com/user-attachments/assets/da23836f-f029-4ae9-95a4-953bc80b6d24" />
  <br/>
</p>


<h1 align="center">Common Stack | Ansible | Playbook | CI Workflow Documentation</h1>

<p align="center">

---

## Author Table

| **Author**  | **Created on** | **Version** | **Last updated by** | **Last Edited On** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ----------- | -------------- | ----------- | ------------------- | ------------------ | --------------- | --------------- | --------------- |
| Saransh Rai | 19-04-2026     | 1.1         | Saransh Rai         | 19-04-2026         |  Anuj Jain      | Prashant Sharma | Piyush Upadhyay |

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [Purpose](#2-purpose)
3. [What is Ansible & Playbook](#3-what-is-ansible--playbook)
4. [Why Ansible in CI](#4-why-ansible-in-ci)
5. [Key Features](#5-key-features)
6. [Workflow (CI + Ansible)](#6-workflow-ci--ansible)
7. [Workflow Diagram](#7-workflow-diagram)
8. [Commands](#8-commands)
9. [Use Cases](#9-use-cases)
10. [Conclusion](#10-conclusion)
11. [References](#11-references)

---

## 1. Introduction

This document explains the workflow of using **Ansible Playbooks** within a **CI (Continuous Integration) pipeline**. It highlights how automation is achieved for configuration management, deployment, and orchestration in modern DevOps environments.

---

## 2. Purpose

The purpose of this document is to:

* Explain the role of Ansible in CI pipelines
* Provide understanding of Playbooks and automation workflows
* Demonstrate how CI tools integrate with Ansible
* Help teams implement consistent and automated deployments

---

## 3. What is Ansible & Playbook

### Ansible

* Open-source automation tool
* Used for configuration management, deployment, and orchestration

### Playbook

* YAML file defining automation tasks
* Contains roles, tasks, and configurations

### Example Playbook

```yaml
- hosts: servers
  tasks:
    - name: Install nginx
      apt:
        name: nginx
        state: present
```

---

## 4. Why Ansible in CI

Ansible is widely used in CI pipelines because:

* Automates infrastructure and deployment tasks
* Reduces manual errors
* Ensures consistent environments
* Easily integrates with CI/CD tools
* Agentless architecture (uses SSH, no agents required)

---

## 5. Key Features

### 1. Agentless Architecture

* No need to install agents on target machines

### 2. Idempotency

* Running playbook multiple times gives the same result

### 3. YAML-based Configuration

* Easy to read and write

### 4. Reusability

* Roles and modules can be reused

### 5. CI/CD Integration

* Works with Jenkins, GitHub Actions, GitLab CI

---

## 6. Workflow (CI + Ansible)

### Step-by-Step Workflow

1. Developer pushes code to repository
2. CI tool triggers pipeline (e.g., Jenkins)
3. Environment setup and dependencies installation
4. Ansible Playbook execution
5. Playbook connects to target servers via SSH
6. Tasks are executed (install, configure, deploy)
7. Deployment result is validated
8. Pipeline reports success/failure

---

## 7. Workflow Diagram

```
Code Push → CI Trigger → Setup Environment → Run Ansible Playbook → Configure/Deploy → Validate → Result
```

<img src="https://github.com/user-attachments/assets/61723365-2a1b-4bc0-bc74-7160790730f6" width="100%" />


---

## 8. Commands

| **Command**                   | **Description**       |
| ----------------------------- | --------------------- |
| ansible --version             | Check Ansible version |
| ansible-playbook playbook.yml | Run playbook          |
| ansible all -m ping           | Test connectivity     |
| ansible-inventory --list      | View inventory        |

---

## 9. Use Cases

| **Use Case**                | **Description**                                                                 |
| --------------------------- | ------------------------------------------------------------------------------- |
| Server Setup Automation     | Automating installation of packages like nginx, docker, and system dependencies |
| Application Deployment      | Deploying applications across multiple servers efficiently                      |
| Configuration Management    | Ensuring consistent configurations across environments                          |
| Infrastructure Provisioning | Automating infrastructure setup and orchestration                               |

---

## 10. Conclusion

Using Ansible Playbooks in CI pipelines enables organizations to automate deployments, maintain consistent infrastructure, and scale operations efficiently while minimizing manual intervention. By integrating Ansible with CI/CD tools, teams can achieve faster, more reliable, and repeatable delivery processes. This approach enhances overall productivity, reduces the risk of human error, and supports modern DevOps practices by ensuring seamless and standardized application deployment across environments.

---

## 11. References

| **Topic**                      | **Link**                                                                            |
| ------------------------------ | ----------------------------------------------------------------------------------- |
| Ansible Official Documentation | [Ansible Docs](https://docs.ansible.com/)                                           |
| Ansible Playbooks Guide        | [Playbook Guide](https://docs.ansible.com/ansible/latest/playbook_guide/index.html) |
| GitHub Actions Documentation   | [GitHub Actions Docs](https://docs.github.com/en/actions)                           |
| GitLab CI/CD Documentation     | [GitLab CI/CD Docs](https://docs.gitlab.com/ee/ci/)                                 |
| Jenkins Documentation          | [Jenkins Docs](https://www.jenkins.io/doc/)                                         |
