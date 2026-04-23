# Common Stack | Ansible | Playbook | CI Workflow Documentation

## Author Table

| Author      | Created on | Version | Last updated by | Last Edited On | L0 Reviewer | L1 Reviewer     | L2 Reviewer     |
| ----------- | ---------- | ------- | --------------- | -------------- | ----------- | --------------- | --------------- |
| Saransh Rai | 19-04-2026 | 1.1     | Saransh Rai     | 19-04-2026     | Anuj Jain   | Prashant Sharma | Piyush Upadhyay |

---

## 1. Introduction

This document explains the workflow of using Ansible Playbooks within a CI (Continuous Integration) pipeline. It covers how automation is achieved for configuration management, deployment, and orchestration.

---

## 2. Why Ansible in CI?

* Automates infrastructure and deployment tasks
* Reduces manual errors
* Ensures consistent environments
* Integrates easily with CI/CD tools
* Agentless (uses SSH, no agents required)

---

## 3. What is Ansible & Playbook?

### Ansible

* Open-source automation tool
* Used for configuration management, deployment, and orchestration

### Playbook

* YAML file defining automation tasks
* Contains roles, tasks, and configurations

Example:

```yaml
- hosts: servers
  tasks:
    - name: Install nginx
      apt:
        name: nginx
        state: present
```

---

## 4. Key Features

### 1. Agentless Architecture

* No need to install agents on target machines

### 2. Idempotency

* Running playbook multiple times gives same result

### 3. YAML-based Configuration

* Easy to read and write

### 4. Reusability

* Roles and modules can be reused

### 5. Integration with CI/CD

* Works with Jenkins, GitHub Actions, GitLab CI

---

## 5. Workflow (CI + Ansible Playbook)

1. Developer pushes code to repository
2. CI tool triggers pipeline (e.g., Jenkins)
3. Pipeline installs required dependencies
4. Ansible Playbook is executed
5. Playbook connects to target servers via SSH
6. Tasks are executed (install, configure, deploy)
7. Deployment result is validated
8. Pipeline reports success/failure

---

## 6. Basic Workflow Diagram (Text)

Code Push → CI Trigger → Setup Environment → Run Ansible Playbook → Configure/Deploy → Validate → Result

---

## 7. Common Commands

| Command                       | Description           |
| ----------------------------- | --------------------- |
| ansible --version             | Check Ansible version |
| ansible-playbook playbook.yml | Run playbook          |
| ansible all -m ping           | Test connectivity     |
| ansible-inventory --list      | View inventory        |

---

## 8. Use Case

* Automating server setup (install packages like nginx, docker)
* Deploying applications across multiple servers
* Managing configurations consistently

---

## 9. Conclusion

Using Ansible Playbooks in CI pipelines enables automated, consistent, and scalable deployments, improving efficiency and reducing manual intervention.
