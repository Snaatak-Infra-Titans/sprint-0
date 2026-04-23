# Ansible Playbook CD Workflow

| Author           | Created on | Version | Last updated by | Last edited on | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer      |
|------------------|------------|---------|-----------------|----------------|--------------|-------------|-------------|------------------|
| Shivam Uniyal    | 17-04-2026 | v1.0    | Shivam Uniyal   | 22-04-2026     | Team         | Anuj Jain   | Prashant    | Piyush Upadhyay  |

---

## Table of Contents

1. [Introduction](#1-introduction)  
2. [What is Ansible Playbook?](#2-what-is-ansible-playbook)  
3. [What is Continuous Delivery (CD)?](#3-what-is-continuous-delivery-cd)  
4. [Ansible Playbook CD Workflow](#4-ansible-playbook-cd-workflow)  
5. [Workflow Explanation](#5-workflow-explanation)  
6. [Conclusion](#6-conclusion)  
7. [Contact Information](#7-contact-information)  
8. [References](#8-references)  

---

## 1. Introduction

Ansible Playbooks are used to automate configuration and deployment. In Continuous Delivery (CD), they help in automating application deployment across environments.

---

## 2. What is Ansible Playbook?

An Ansible Playbook is a YAML file that defines tasks to be executed on target servers.

It is used to:
- Deploy applications  
- Configure systems  
- Automate infrastructure  

---

## 3. What is Continuous Delivery (CD)?

Continuous Delivery (CD) is a DevOps practice where code changes are automatically built, tested, and prepared for deployment. It ensures that applications are always in a deployable state and can be released quickly with minimal manual effort.

---

## 4. Ansible Playbook CD Workflow

### Workflow Diagram

<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/52043ea4-c30e-4cde-ab15-e547aa206eb1" />

<br>

---

## 5. Workflow Explanation

1. Developer pushes code to Git repository  
2. CI/CD pipeline is triggered (Jenkins/GitLab)  
3. Ansible playbook is executed by pipeline  
4. Playbook targets defined inventory hosts  
5. Playbook invokes the Ansible Role  
6. Role executes tasks on target servers  
7. Application/configuration is deployed  
8. Deployment is verified   

---

## 6. Conclusion

Ansible Playbooks enable automated and consistent deployments in CD pipelines, improving reliability and reducing manual effort.

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
| https://www.jenkins.io/doc | Jenkins documentation |
