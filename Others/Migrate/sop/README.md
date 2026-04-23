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
2. [Purpose](#2-Purpose)
3. [Prerequisites](#3-Prerequisites)
4. [What is Migrate](#4-what-is-migrate)  
5. [Why Migrate](#5-why-migrate)  
6. [Key Features](#6-key-features)  
7. [Workflow](#7-workflow)  
8. [Installation Guide](#8-installation-guide)  
9. [Migration Commands (Common)](#9-migration-commands-common)  
10. [DB Schema Evolution Diagram](#10-db-schema-evolution-diagram)  
11. [Liquibase and Migration Concept](#11-liquibase-and-migration-concept)  
12. [Liquibase Example](#12-liquibase-example)  
13. [Validation](#13-validation)  
14. [Troubleshooting](#14-troubleshooting)  
15. [Best Practices](#15-best-practices)  
16. [Conclusion](#16-conclusion)  
17. [Contact Information](#17-contact-information)  
18. [References](#18-references)  

---

## 1. Introduction

When working on applications, the database structure keeps changing as new features are added. Managing these changes manually can quickly become confusing and error-prone.

Migration tools help handle this in a structured way. Instead of making direct changes in the database, we define changes as scripts and apply them in a controlled manner.

This ensures all environments (development, testing, production) remain consistent.

---

## 2. Purpose

The purpose of this SOP is to define a standardized approach for managing database schema changes using migration tools. It ensures consistency, traceability, and reliability across all environments.

---

## 3. Prerequisites

Before starting, ensure the following:

* Basic understanding of databases
* Access to database
* Linux/Unix environment (or compatible)
* Required permissions to install and run commands

---

## 4. What is Migrate

Migrate is a way to manage database changes using version-controlled scripts.

* Database changes are written as code
* Each change is stored as a migration file
* Changes can be applied or rolled back safely

Example:

```bash
make run-migrations
```

---

## 5. Why Migrate

Migration helps avoid manual mistakes and keeps databases consistent.

### Key Reasons

* **Consistency Across Environments** → Same schema everywhere
* **Version Control** → DB changes tracked like code
* **Safe Updates** → Controlled execution
* **Rollback Support** → Easy revert
* **Automation** → Works with CI/CD

---

## 6. Key Features

| Feature              | Description                |
| -------------------- | -------------------------- |
| Versioned Migrations | Tracks schema changes      |
| Rollback Support     | Safe revert capability     |
| Environment Sync     | Keeps environments aligned |
| CI/CD Integration    | Automates deployment       |

---

## 7. Workflow

```
Update Schema
      ↓
Generate Migration
      ↓
Review Script
      ↓
Apply Migration
      ↓
Database Updated
```

---

## 8. Installation Guide

### Step 1: Download Migrate

```bash
wget https://github.com/golang-migrate/migrate/releases/latest/download/migrate.linux-amd64.tar.gz
```

### Step 2: Extract

```bash
tar -xvf migrate.linux-amd64.tar.gz
```

### Step 3: Move Binary

```bash
sudo mv migrate /usr/local/bin/
```

### Step 4: Verify

```bash
migrate -version
```

---

## 9. Migration Commands (Common)

### Initialize (Flask Example)

```bash
flask db init
```

### Generate Migration

```bash
flask db migrate -m "add user table"
```

### Apply Migration

```bash
flask db upgrade
```

### Rollback

```bash
flask db downgrade
```

---

## 10. DB Schema Evolution Diagram

```
Version 1
   ↓
Migration
   ↓
Version 2
   ↓
Migration
   ↓
Version 3
```

---

## 11. Liquibase and Migration Concept

* **Migration = Concept** (process of managing DB changes)
* **Liquibase = Tool** (implements migration)

### Comparison

| Tool      | Type            | Usage                |
| --------- | --------------- | -------------------- |
| Migrate   | CLI Tool        | Simple microservices |
| Liquibase | Enterprise Tool | Complex systems      |

---

## 12. Liquibase Example

```xml
<databaseChangeLog>

    <changeSet id="1" author="user">
        <createTable tableName="users">
            <column name="id" type="INT" autoIncrement="true">
                <constraints primaryKey="true" nullable="false"/>
            </column>
            <column name="name" type="VARCHAR(100)"/>
        </createTable>
    </changeSet>

    <changeSet id="2" author="user">
        <addColumn tableName="users">
            <column name="email" type="VARCHAR(150)"/>
        </addColumn>
    </changeSet>

</databaseChangeLog>
```

Run:

```bash
liquibase update
```

---

## 13. Validation

After applying migrations, validate:

* Tables/columns are created as expected
* No errors in migration logs
* Application works with updated schema

---

## 14. Troubleshooting

| Issue                | Solution                      |
| -------------------- | ----------------------------- |
| Migration fails      | Check syntax & DB connection  |
| Version mismatch     | Sync migration history        |
| Rollback not working | Ensure rollback scripts exist |

---

## 15. Best Practices

| Practice                     | Description                                    |
| ---------------------------- | ---------------------------------------------- |
| Review Before Execution      | Always review migration scripts before running |
| Use Descriptive Names        | Clearly describe purpose of migration          |
| Avoid Editing Old Migrations | Never modify already applied migrations        |
| Backup Before Deployment     | Take DB backup before production changes       |
| Test in Lower Environments   | Validate in dev/staging before production      |
| Keep Migrations Small        | Prefer small, incremental changes              |
| Maintain Rollback Scripts    | Ensure rollback is always possible             |

---

## 16. Conclusion

Database migration ensures controlled and reliable schema changes. Using tools like Migrate or Liquibase improves consistency, reduces manual errors, and supports automated deployments.

---

## 17. Contact Information

| Name        | Email                                                                           |
| ----------- | ------------------------------------------------------------------------------- |
| Saransh Rai | [saransh.rai.snaatak@mygurukulam.co](mailto:saransh.rai.snaatak@mygurukulam.co) |

---

## 18. References

| Resource                | Link                                                                               |
| ----------------------- | ---------------------------------------------------------------------------------- |
| Liquibase Documentation | [https://www.liquibase.com/documentation](https://www.liquibase.com/documentation) |
| Flask-Migrate Docs      | [https://flask-migrate.readthedocs.io/](https://flask-migrate.readthedocs.io/)     |
| Alembic Docs            | [https://alembic.sqlalchemy.org/](https://alembic.sqlalchemy.org/)                 |


