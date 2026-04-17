# Common Stack | Ansible | Role | Jinja Templating

---

## Author Table

| **Author** | **Created on** | **Version** | **Last updated by** | **Last Edited On** | **Pre Reviewer** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ---------- | -------------- | ----------- | ------------------- | ------------------ | ---------------- | --------------- | --------------- | --------------- |
| Ankita     | 17-04-2026     | v1.0        | Ankita              | 17-04-2026         | Team             |                 |                 |                 |

---

## Table of Contents

1. [Introduction](#introduction)
2. [Purpose](#purpose)
3. [What is Jinja Templating?](#what-is-jinja-templating)
4. [Why Jinja in Ansible Roles](#why-jinja-in-ansible-roles)
5. [Key Concepts](#key-concepts)
6. [Jinja Syntax Basics](#jinja-syntax-basics)
7. [Using Jinja in Ansible Roles](#using-jinja-in-ansible-roles)
8. [Common Use Cases](#common-use-cases)
9. [Best Practices](#best-practices)
10. [Troubleshooting](#troubleshooting)
11. [Contact Information](#contact-information)
12. [References](#references)

---

## Introduction

Jinja (Jinja2) is a powerful templating engine used in Ansible to dynamically generate configuration files and scripts.

In Ansible roles, Jinja templating enables reusable and flexible automation by allowing variables, conditions, and loops to be embedded into templates.

---

## Purpose

This document provides a conceptual understanding of Jinja templating in Ansible roles, including syntax, usage, and best practices for real-world automation.

---

## What is Jinja Templating?

Jinja is a template engine for Python that allows dynamic content generation.

In Ansible, it is primarily used with `.j2` files to render configurations using variables.

---

## Why Jinja in Ansible Roles

Jinja templating is used because:

* Enables dynamic configuration generation
* Improves reusability of roles
* Supports conditional logic and loops
* Reduces duplication in configuration files

---

## Key Concepts

### 1. Variables

Variables are used to replace values dynamically.

Example:

```jinja
{{ app_port }}
```

---

### 2. Expressions

Perform operations inside templates.

```jinja
{{ 10 + 5 }}
```

---

### 3. Filters

Used to modify variables.

```jinja
{{ name | upper }}
```

---

### 4. Conditions

```jinja
{% if env == "prod" %}
Production Mode
{% endif %}
```

---

### 5. Loops

```jinja
{% for user in users %}
User: {{ user }}
{% endfor %}
```

---

## Jinja Syntax Basics

| Syntax  | Purpose            |
| ------- | ------------------ |
| `{{ }}` | Output variables   |
| `{% %}` | Control structures |
| `{# #}` | Comments           |

---

## Using Jinja in Ansible Roles

### Template File

Create template file:

```
templates/config.j2
```

Example:

```jinja
server {
    listen {{ port }};
    server_name {{ domain }};
}
```

---

### Playbook Usage

```yaml
- name: Deploy config
  hosts: all
  tasks:
    - name: Copy template
      template:
        src: config.j2
        dest: /etc/nginx/sites-enabled/default
```

---

## Common Use Cases

* Dynamic Nginx configuration
* Environment-based configuration files
* Generating application config files
* Loop-based user or service creation

---

## Best Practices

* Keep templates simple and readable
* Avoid complex logic in templates
* Use variables from group_vars and host_vars
* Validate templates before deployment

---

## Troubleshooting

| Issue                  | Cause                | Solution             |
| ---------------------- | -------------------- | -------------------- |
| Template not rendering | Wrong variable       | Check variable names |
| Syntax error           | Invalid Jinja syntax | Validate template    |
| File not updated       | Cache issue          | Re-run playbook      |

---

## Contact Information

| Name   | Email                                                                             |
| ------ | --------------------------------------------------------------------------------- |
| Ankita | [ankita.singh.snaatak@mygurukulam.co](mailto:ankita.singh.snaatak@mygurukulam.co) |

---

## References

| Topic                   | Link                                                                                                                                                                                 |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Jinja Docs              | [https://jinja.palletsprojects.com/](https://jinja.palletsprojects.com/)                                                                                                             |
| Ansible Template Module | [https://docs.ansible.com/ansible/latest/collections/ansible/builtin/template_module.html](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/template_module.html) |
