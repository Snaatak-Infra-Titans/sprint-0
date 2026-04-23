<p align="center">
  <img width="600" height="400" alt="image" src="https://github.com/user-attachments/assets/98f725e7-b98d-46aa-a3e4-1c344a7099d5" />
  <br/>
</p>


<h1 align="center">Common Stack | Others | Migrate | SOP for Migrate</h1>

<p align="center">
  Step by step installation guide
</p>

---

## Author Table

| Author      | Created on | Version | Last updated by | Last Edited On | L0 Reviewer | L1 Reviewer     | L2 Reviewer     |
| ----------- | ---------- | ------- | --------------- | -------------- | ----------- | --------------- | --------------- |
| Saransh Rai | 19-04-2026 | 1.1     | Saransh Rai     | 19-04-2026     | Anuj Jain   | Prashant Sharma | Piyush Upadhyay |

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [Purpose](#2-purpose)
3. [Prerequisites](#3-prerequisites)
4. [What is Migrate](#4-what-is-migrate)
5. [Why Migrate](#5-why-migrate)
6. [Key Features](#6-key-features)
7. [Workflow](#7-workflow)
8. [Installation Guide](#8-installation-guide)
9. [Migration Commands (Common)](#9-migration-commands-common)
10. [DB Schema Evolution Diagram](#10-db-schema-evolution-diagram)
11. [Migration Tool Comparison](#11-migration-tool-comparison)
12. [Example (Flask-Migrate)](#12-example-flask-migrate)
13. [Validation](#13-validation)
14. [Troubleshooting](#14-troubleshooting)
15. [Best Practices](#15-best-practices)
16. [Conclusion](#16-conclusion)
17. [Contact Information](#17-contact-information)
18. [References](#18-references)

---

## 1. Introduction

Database schema changes are frequent during application development. Managing these changes manually leads to inconsistency and errors.

Migration tools solve this by allowing schema changes to be written as version-controlled scripts and applied in a structured way.

---

## 2. Purpose

To standardize database schema changes using migration tools, ensuring consistency, traceability, and reliability.

---

## 3. Prerequisites

* Basic database knowledge
* Linux/Unix environment
* Terminal access
* Permission to install tools

---

## 4. What is Migrate

Migration is the process of managing database schema changes in a controlled and versioned way.

This can be implemented using different tools, such as:

* **Flask-Migrate** for Flask-based applications
* **golang-migrate** for CLI-based SQL migrations
* **Liquibase** for enterprise database change management

In this SOP, **Flask-Migrate** is used for demonstration because it is simple to understand and easy to integrate with a sample Flask project.

---

## 5. Why Migrate

* Consistency across environments
* Version control for DB
* Safe updates
* Rollback support
* CI/CD integration

---

## 6. Key Features

| Feature    | Description       |
| ---------- | ----------------- |
| Versioning | Tracks DB changes |
| Rollback   | Revert changes    |
| Automation | CI/CD compatible  |

---

## 7. Workflow

Code Change → Create Migration → Review → Apply → DB Updated

---

## 8. Installation Guide

### Step 1: Install Required Packages

```bash
pip install flask flask-sqlalchemy flask-migrate
```

### Step 2: Verify Installation

```bash
python -c "import flask, flask_sqlalchemy, flask_migrate; print('Installation successful')"
```

---

## 9. Migration Commands (Common)

### Initialize Migration Repository

```bash
flask db init
```

### Generate Migration

```bash
flask db migrate -m "create user table"
```

### Apply Migration

```bash
flask db upgrade
```

### Rollback Migration

```bash
flask db downgrade
```

> Note: Other migration tools such as **golang-migrate** and **Liquibase** also exist. This SOP demonstrates migration using **Flask-Migrate** for simplicity.

---

## 10. DB Schema Evolution Diagram

Version 1 → Version 2 → Version 3

---

## 11. Migration Tool Comparison

Migration is a concept, and multiple tools can implement it.

| Tool           | Type                                | Best Use Case                          |
| -------------- | ----------------------------------- | -------------------------------------- |
| Flask-Migrate  | Framework-integrated migration tool | Flask applications                     |
| golang-migrate | CLI migration tool                  | SQL-based migrations and microservices |
| Liquibase      | Enterprise migration tool           | Complex multi-environment systems      |

---

## 12. Example (Flask-Migrate)

This SOP demonstrates migration using Flask-Migrate.

Typical workflow:

```bash
flask db init
flask db migrate -m "create user table"
flask db upgrade
flask db downgrade
```

---

## 13. Validation

* Tables created correctly
* No errors in logs
* DB structure matches expected output

---

## 14. Troubleshooting

| Issue           | Solution               |
| --------------- | ---------------------- |
| Migration fails | Check DB path          |
| Syntax error    | Fix SQL                |
| Rollback fails  | Ensure down.sql exists |

---

## 15. Best Practices

| Practice                     | Description                                    |
| ---------------------------- | ---------------------------------------------- |
| Review Before Execution      | Always review migration scripts before running |
| Use Descriptive Names        | Clearly describe the purpose of migration      |
| Avoid Editing Old Migrations | Never modify already applied migrations        |
| Backup Before Deployment     | Take database backup before production changes |
| Test in Lower Environments   | Validate in dev/staging before production      |
| Keep Migrations Small        | Prefer small, incremental changes              |
| Maintain Rollback Scripts    | Ensure rollback is always possible             |

---

## 16. Conclusion

Database migration ensures controlled and reliable schema updates. While multiple tools exist, this SOP demonstrates the concept using Flask-Migrate for simplicity and ease of understanding.

---

## 17. Contact Information

| Name        | Email                                                                           |
| ----------- | ------------------------------------------------------------------------------- |
| Saransh Rai | [saransh.rai.snaatak@mygurukulam.co](mailto:saransh.rai.snaatak@mygurukulam.co) |

---

## 18. References

| Resource                     | Link                                                                                   |
| ---------------------------- | -------------------------------------------------------------------------------------- |
| Flask-Migrate Documentation  | [https://flask-migrate.readthedocs.io/](https://flask-migrate.readthedocs.io/)         |
| Alembic Documentation        | [https://alembic.sqlalchemy.org/](https://alembic.sqlalchemy.org/)                     |
| golang-migrate Documentation | [https://github.com/golang-migrate/migrate](https://github.com/golang-migrate/migrate) |
| Liquibase Documentation      | [https://www.liquibase.com/documentation](https://www.liquibase.com/documentation)     |



