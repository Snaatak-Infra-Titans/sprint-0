# Ansible Role Introduction

<img width="940" height="400" src="https://github.com/user-attachments/assets/59588ad0-c256-4392-b490-3ea0433d2478" />

<br>

| Author           | Created on | Version | Last updated by | Last edited on | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer      |
|------------------|------------|---------|-----------------|----------------|--------------|-------------|-------------|------------------|
| Shivam Uniyal    | 16-04-2026 | v1.0    | Shivam Uniyal   | 22-04-2026     | Team         | Anuj Jain   | Prashant    | Piyush Upadhyay  |

---

## Table of Contents

1. [Introduction](#1-introduction)  
2. [What is an Ansible Role?](#2-what-is-an-ansible-role)  
3. [Why Use Ansible Roles?](#3-why-use-ansible-roles)  
4. [Key Features of Ansible Roles](#4-key-features-of-ansible-roles)  
5. [Structure of an Ansible Role](#5-structure-of-an-ansible-role)  
6. [Conclusion](#6-conclusion)  
7. [Contact Information](#7-contact-information)  
8. [References](#8-references)

---

## 1. Introduction

Ansible is an automation tool used for configuration management and deployment.  
Roles help organize large playbooks into reusable and structured components.

---

## 2. What is an Ansible Role?

An Ansible Role is a structured way to organize tasks, variables, files, and templates into reusable units.

Common directories include:

- `tasks/` – Main execution steps  
- `handlers/` – Triggered actions  
- `files/` – Static files  
- `templates/` – Dynamic configurations  
- `vars/` – Variables  
- `defaults/` – Default values  

---

## 3. Why Use Ansible Roles?

- Improves modularity  
- Enables code reuse  
- Simplifies maintenance  
- Enhances scalability  
- Supports team collaboration  

---

## 4. Key Features of Ansible Roles

| Feature | Description |
|--------|------------|
| Standardized Structure | Predefined directory layout |
| Reusability | Can be reused across projects |
| Separation of Concerns | Each role handles a specific function |
| Easy Integration | Can be easily used in playbooks |
| Variable Management | Supports flexible variable handling |
| Idempotency | Ensures safe repeated execution |

---

## 5. Structure of an Ansible Role

```bash
my-role/
├── tasks/
├── handlers/
├── files/
├── templates/
├── vars/
├── defaults/
├── meta/
```

---

## 6. Conclusion

Ansible Roles provide a structured and reusable approach to automation, making configurations easier to manage and scale in DevOps environments.

---

## 7. Contact Information

| Name           | Email ID |
|----------------|----------|
| Shivam Uniyal  | shivam.uniyal.snaatak@mygurukulam.co |

---

## 8. References

| Link | Description |
|------|------------|
| https://docs.ansible.com | Official Ansible documentation |
| https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_roles.html | Ansible roles guide |
