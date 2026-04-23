# Ansible Role Introduction

<img width="940" height="400" alt="image" src="https://github.com/user-attachments/assets/59588ad0-c256-4392-b490-3ea0433d2478" />

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
6. [Use Cases](#6-use-cases)  
7. [CD Workflow using Ansible Role](#7-cd-workflow-using-ansible-playbook-and-role)  
8. [Demo (Playbook Execution)](#8-demo-playbook-execution)  
9. [Conclusion](#9-conclusion)  
10. [FAQs](#10-faqs)  
11. [Contact Information](#11-contact-information)  
12. [References](#12-references)

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
- `templates/` – Dynamic configs  
- `vars/` – Variables  
- `defaults/` – Default values  

---

## 3. Why Use Ansible Roles?

- Modularity  
- Reusability  
- Maintainability  
- Scalability  
- Better collaboration  

---

## 4. Key Features of Ansible Roles

| Feature | Description |
|--------|------------|
| Standardized Structure | Predefined directory layout |
| Reusability | Can be reused across projects |
| Separation of Concerns | Each role handles one task |
| Easy Integration | Simple to include in playbooks |
| Variable Management | Supports flexible variables |
| Idempotency | Safe repeated execution |

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

## 6. Use Cases

- Web server setup  
- Database configuration  
- Application deployment  
- Infrastructure provisioning  
- CI/CD automation  

---

## 7. CD Workflow using Ansible Playbook and Role

<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/d9ccb64a-2a0d-40c4-8067-e56ff37ddba0" />

<br>

1. Developer pushes code to Git repository  
2. CI/CD pipeline is triggered (Jenkins/GitLab)  
3. Ansible playbook is executed by pipeline  
4. Playbook targets defined inventory hosts  
5. Playbook invokes the Ansible Role  
6. Role executes tasks on target servers  
7. Application/configuration is deployed  
8. Deployment is verified  

---

## 8. Demo (Playbook Execution)

### Example Playbook

```yaml
- hosts: web
  become: yes
  roles:
    - nginx-role
```

### Run Command

```bash
ansible-playbook -i inventory.ini playbook.yml
```

---

## 9. Conclusion

Ansible Roles simplify automation by making code modular, reusable, and scalable. They are essential for managing complex DevOps workflows.

---

## 10. FAQs

**Q1. What is an Ansible Role?**  
A structured way to organize automation tasks.

**Q2. Why use roles?**  
For better reusability and maintainability.

**Q3. Can roles be reused?**  
Yes, across multiple projects.

---

## 11. Contact Information

| Name           | Email ID |
|----------------|----------|
| Shivam Uniyal  | shivam.uniyal.snaatak@mygurukulam.co |

---

## 12. References

| Link | Description |
|------|------------|
| https://docs.ansible.com | Official Ansible documentation |
| https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_roles.html | Ansible roles guide |
