# Ansible Role — CI Workflow Documentation


## Document Details

| Author  | Created On     | Version | Last Updated By | Last Edited On | L0 Reviewer  | L1 Reviewer  | L2 Reviewer   |
|---------|----------------|---------|------------------|----------------|--------------|--------------|---------------|
| Deepak  | 14 April 2026  | v1.1    | Deepak           | 22 April 2026  | Mohit Kumar  | Faisal Khan  | Mahesh Kumar  |


## Table of Contents

1. [Introduction](#1-introduction)  
2. [What is Continuous Integration (CI)?](#2-what-is-continuous-integration-ci)  
3. [What is an Ansible Role?](#3-what-is-an-ansible-role)  
4. [CI for Ansible Roles](#4-ci-for-ansible-roles)  
5. [CI Workflow](#5-ci-workflow)  
6. [Dry Run (Most Important)](#6-dry-run-most-important)  
7. [Required Structure](#7-required-structure)  
8. [Best Practices](#8-best-practices)  
9. [FAQs](#9-faqs)  
10. [Conclusion](#10-conclusion)  
11. [Contact Information](#11-contact-information)  
12. [References](#12-references)  


## 1. Introduction

This document explains how Continuous Integration (CI) works for Ansible roles in a simple and practical way.

It covers:
- CI basics  
- Ansible roles  
- Workflow and validation  
- Best practices  

Goal: Ensure every Ansible role works correctly before deployment.



## 2. What is Continuous Integration (CI)?

Continuous Integration is a development practice where code is automatically tested and validated after every change.

| Component | Meaning |
|-----------|--------|
| Code Push | Developer submits changes |
| Pipeline | Automated process starts |
| Validation | Code is checked and tested |
| Result | Pass or fail feedback |


## 3. What is an Ansible Role?

An Ansible role is a structured way to organize automation code.

It groups tasks, variables, templates, and handlers into a reusable unit.

| Part | Meaning |
|------|--------|
| tasks | Main automation steps |
| handlers | Actions triggered by tasks |
| vars/defaults | Variables used in role |
| templates | Config files using Jinja2 |



## 4. CI for Ansible Roles

CI ensures that the role is correct and safe to use.

| Area | Validation |
|------|-----------|
| YAML | Syntax correctness |
| Structure | Proper role layout |
| Variables | Defined and usable |
| Templates | Render correctly |
| Dry Run | Executes without changes |
| Idempotency | No repeated changes |



## 5. CI Workflow

```Code Push → Lint → Syntax Check → Dry Run → Result```

| Step   | Tool/Action        | Purpose              |
|--------|-------------------|----------------------|
| Push   | Git               | Trigger pipeline     |
| Lint   | ansible-lint      | Check best practices |
| Syntax | ansible-playbook  | Validate YAML        |
| Dry Run| ansible-playbook  | Simulate execution   |
| Result | CI System         | Show pass/fail       |




## 6. Dry Run (Most Important)

Command:

```ansible-playbook tests/test.yml -i tests/inventory --check --diff```



| Parameter | Meaning |
|----------|--------|
| --check  | Run without making changes |
| --diff   | Show expected differences |

Dry run helps detect issues early without affecting systems.



## 7. Required Structure

```
role/
├── tasks/
├── handlers/
├── defaults/
├── vars/
├── templates/
├── meta/
├── tests/
│   ├── test.yml
│   └── inventory
├── .ansible-lint

```
| Component | Purpose |
|-----------|--------|
| tasks | Main execution logic |
| handlers | Triggered actions |
| defaults | Default variables |
| vars | Role-specific variables |
| templates | Configuration templates |
| tests | Validation setup |


## 8. Best Practices

| Practice | Reason |
|----------|-------|
| Idempotency | Prevent repeated changes |
| Dry Run | Catch issues early |
| Use modules | More reliable than shell/command |
| Local testing | Reduce CI failures |


## 9. FAQs

- Why use --check mode?  
  To simulate execution without making changes.

- What is idempotency?  
  Running the role multiple times should not cause changes.

- Is linting required?  
  Yes, it helps maintain best practices.

- Why are some tasks skipped?  
  Some modules do not support check mode.



## 10. Conclusion

CI ensures your Ansible roles are validated, safe, and reliable before deployment.

Always test and validate before merging changes.



## 11. Contact Information

| Name   | Contact |
|--------|---------|
| Deepak | deepak.nagar.snaatak@mygurukulam.co |


## 12. References

| Resource | Link |
|----------|------|
| Ansible Documentation | https://docs.ansible.com |
| Ansible Lint | https://ansible.readthedocs.io/projects/lint/ |
| Jenkins Pipeline | https://www.jenkins.io/doc/book/pipeline/ |
