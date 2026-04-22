# Ansible Inventory — Dynamic Inventory Documentation


## Document Details

| Author  | Created On     | Version | Last Updated By | Last Edited On | L0 Reviewer  | L1 Reviewer  | L2 Reviewer   |
|---------|----------------|---------|------------------|----------------|--------------|--------------|---------------|
| Deepak  | 14 April 2026  | v1.1    | Deepak           | 22 April 2026  | Mohit Kumar  | Faisal Khan  | Mahesh Kumar  |



## Table of Contents

1. [Introduction](#1-introduction)  
2. [What is Ansible Inventory?](#2-what-is-ansible-inventory)  
3. [Static vs Dynamic Inventory](#3-static-vs-dynamic-inventory)  
4. [How Dynamic Inventory Works](#4-how-dynamic-inventory-works)  
5. [AWS EC2 Dynamic Inventory](#5-aws-ec2-dynamic-inventory)  
6. [Dynamic Inventory Configuration](#6-dynamic-inventory-configuration)  
7. [Testing Inventory](#7-testing-inventory)  
8. [Best Practices](#8-best-practices)  
9. [FAQs](#9-faqs)  
10. [Conclusion](#10-conclusion)  
11. [References](#11-references)  



## 1. Introduction

This document explains how Ansible inventory works, focusing on dynamic inventory.

It covers:
- Inventory basics  
- Static vs dynamic approach  
- AWS-based inventory  
- Testing and best practices  

Goal: Automatically manage servers without manual updates.



## 2. What is Ansible Inventory?

An Ansible inventory is a list of machines that Ansible manages.

| Part | Meaning |
|------|--------|
| Host | Server IP or hostname |
| Group | Logical grouping (e.g., api, db) |
| Variables | Connection details (user, key) |

Ansible uses inventory before running any playbook.



## 3. Static vs Dynamic Inventory

| Feature | Static | Dynamic |
|--------|--------|---------|
| Definition | Manual file | Auto-generated |
| Updates | Manual | Automatic |
| Cloud Support | Poor | Excellent |
| Scaling | Hard | Easy |
| Best Use | Small setups | Cloud / large infra |

Dynamic inventory is preferred for modern systems.



## 4. How Dynamic Inventory Works

Steps:

1. Ansible calls inventory plugin  
2. Plugin queries AWS API  
3. AWS returns host details  
4. Ansible runs playbook on hosts  

Flow:

Developer → Run Playbook → Plugin → AWS → Hosts → Execution


## 5. AWS EC2 Dynamic Inventory

Uses `amazon.aws.aws_ec2` plugin.

Instances are grouped using tags.

| Tag | Purpose |
|-----|--------|
| Service | Application name |
| Environment | dev / staging / prod |




## 6. Dynamic Inventory Configuration

File: inventories/aws_ec2.yml

```yaml
plugin: amazon.aws.aws_ec2

regions:
  - ap-south-1

filters:
  instance-state-name: running

keyed_groups:
  - key: tags.Service
    prefix: service
  - key: tags.Environment
    prefix: env

compose:
  ansible_host: private_ip_address
  ansible_user: ubuntu
```

| Field | Meaning |
|-------|--------|
| plugin | AWS EC2 plugin |
| regions | AWS region |
| filters | Only running instances |
| keyed_groups | Group by tags |
| compose | Set connection details |



## 7. Testing Inventory

| Command | Purpose |
|---------|--------|
| ansible-inventory --list | Show all hosts |
| ansible-inventory --graph | Show groups |
| ansible -m ping | Test connectivity |

Always verify inventory before running playbooks.



## 8. Best Practices

| Practice | Reason |
|----------|-------|
| Use tags | Enables grouping |
| Avoid hardcoding credentials | Improves security |
| Test with --list | Prevent errors |
| Use private IPs | Reliable connectivity |
| Keep naming consistent | Easy management |



## 9. FAQs

- What is dynamic inventory?  
  Auto-generated host list from AWS.

- When should I use it?  
  When infrastructure changes frequently.

- Can I use multiple inventories?  
  Yes.

- Do I need static inventory?  
  Only for small setups.



## 10. Conclusion

Dynamic inventory makes Ansible scalable and reliable.

- No manual updates  
- Always accurate  
- Works well with cloud  


## 11. References

| Description | Link |
|-------------|------|
| Official guide for managing Ansible inventory | [Ansible Inventory Guide](https://docs.ansible.com/ansible/latest/inventory_guide/) |
| AWS EC2 dynamic inventory plugin documentation | [AWS EC2 Plugin](https://docs.ansible.com/ansible/latest/collections/amazon/aws/aws_ec2_inventory.html) |


---

## Author

| Name   | Role              | Contact                                  |
|--------|-------------------|------------------------------------------|
| Deepak | DevOps Engineer   | deepak.nagar.snaatak@mygurukulam.co      |
