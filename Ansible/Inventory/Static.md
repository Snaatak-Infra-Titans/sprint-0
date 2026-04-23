# Common Stack | Ansible | Role | Jinja Templating

---

## Author Table

| **Author** | **Created on** | **Version** | **Last updated by** | **Last Edited On** | **Pre Reviewer** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ---------- | -------------- | ----------- | ------------------- | ------------------ | ---------------- | --------------- | --------------- | --------------- |
| Ankita     | 17-04-2026     | v1.0        | Ankita              | 23-04-2026         | Team             | Komal Jaiswal   | Akshit Kapil    | Mahesh Kumar    |

---

## Table of Contents

* Introduction
* Purpose
* Prerequisites
* What is Static Inventory
* Inventory File Structure
* Step-by-Step Implementation
* Verification
* Best Practices
* Troubleshooting
* Contact Information
* References

---

## Introduction

Ansible uses an inventory file to define the list of hosts it manages. A static inventory is a manually maintained file where all target systems are explicitly defined.

It is commonly used in small environments, testing setups, or stable infrastructures.

---

## Purpose

This SOP helps you:

* Understand static inventory in Ansible
* Create and configure inventory files
* Define hosts and groups
* Execute Ansible commands using static inventory

---

## Prerequisites

* Ubuntu 20.04 / 22.04
* Ansible installed
* SSH access to target machines
* Basic Linux knowledge
* Network connectivity between control node and targets

---

## What is Static Inventory

A static inventory is a file (INI or YAML) that contains:

* Hostnames or IP addresses
* Group definitions
* Variables (host/group level)

Unlike dynamic inventory, it does not automatically fetch hosts.

---

## Inventory File Structure

### INI Format

```ini
[web]
192.168.1.10
192.168.1.11

[db]
192.168.1.20

[all:vars]
ansible_user=ubuntu
ansible_ssh_private_key_file=~/.ssh/id_rsa
```

### YAML Format

```yaml
all:
  children:
    web:
      hosts:
        192.168.1.10:
        192.168.1.11:
    db:
      hosts:
        192.168.1.20:
  vars:
    ansible_user: ubuntu
```

---

## Step-by-Step Implementation

### Step 1: Install Ansible

```bash
sudo apt update
sudo apt install ansible -y
```

### Step 2: Create Inventory File

```bash
mkdir ansible-project
cd ansible-project
nano inventory.ini
```

### Step 3: Define Hosts and Groups

```ini
[web]
web1 ansible_host=192.168.1.10
web2 ansible_host=192.168.1.11

[db]
db1 ansible_host=192.168.1.20

[all:vars]
ansible_user=ubuntu
ansible_ssh_private_key_file=~/.ssh/id_rsa
```

### Step 4: Test Connectivity

```bash
ansible all -i inventory.ini -m ping
```

### Step 5: Run Ad-hoc Command

```bash
ansible web -i inventory.ini -m shell -a "uptime"
```

### Step 6: Run Playbook

```bash
ansible-playbook -i inventory.ini playbook.yml
```

---

## Verification

```bash
ansible-inventory -i inventory.ini --list
```

---

## Best Practices

* Use meaningful group names (web, db, app)
* Avoid hardcoding credentials
* Use SSH keys instead of passwords
* Keep inventory modular
* Store in Git repository

---

## Troubleshooting

| Issue                  | Cause                | Solution               |
| ---------------------- | -------------------- | ---------------------- |
| Host unreachable       | Wrong IP / SSH issue | Verify connectivity    |
| Permission denied      | Wrong key/user       | Check SSH key and user |
| Inventory not detected | Wrong path           | Use -i option          |
| Ping fails             | Firewall issue       | Allow port 22          |

---

## Contact Information

| Name   | Email                                                                             |
| ------ | --------------------------------------------------------------------------------- |
| Ankita | [ankita.singh.snaatak@mygurukulam.co](mailto:ankita.singh.snaatak@mygurukulam.co) |

---

## References

* [https://docs.ansible.com/ansible/latest/inventory_guide/intro_inventory.html](https://docs.ansible.com/ansible/latest/inventory_guide/intro_inventory.html)
* [https://docs.ansible.com/](https://docs.ansible.com/)
