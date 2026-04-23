# Common Stack | Others | Migrate | SOP for Migrate

Step by step installation guide

---

## Author Table

| Author      | Created on | Version | Last updated by | Last Edited On | L0 Reviewer | L1 Reviewer     | L2 Reviewer     |
| ----------- | ---------- | ------- | --------------- | -------------- | ----------- | --------------- | --------------- |
| Saransh Rai | 19-04-2026 | 1.1     | Saransh Rai     | 19-04-2026     | Anuj Jain   | Prashant Sharma | Piyush Upadhyay |


---

## Table of Contents

1. [Introduction](#1-introduction)  
2. [What is Migrate](#2-what-is-migrate)  
3. [Why Migrate](#3-why-migrate)  
4. [Key Features](#4-key-features)  
5. [Workflow](#5-workflow)  
6. [Installation Guide](#6-installation-guide)  
7. [Migration Commands (Common)](#7-migration-commands-common)  
8. [DB Schema Evolution Diagram](#8-db-schema-evolution-diagram)  
9. [Liquibase and Migration Concept](#9-liquibase-and-migration-concept)  
10. [Liquibase Example](#10-liquibase-example)  
11. [Validation](#11-validation)  
12. [Troubleshooting](#12-troubleshooting)  
13. [Best Practices](#13-best-practices)  
14. [Conclusion](#14-conclusion)  
15. [Contact Information](#15-contact-information)  
16. [References](#16-references)  

---

## 1. Introduction

When working on applications, the database structure keeps changing as new features are added. Managing these changes manually can quickly become confusing and error-prone.

Migration tools help handle this in a structured way. Instead of making direct changes in the database, we define changes as scripts and apply them in a controlled manner.

This ensures all environments (development, testing, production) remain consistent.

---

## 2. What is Migrate

Migrate is a way to manage database changes using version-controlled scripts.

* Database changes are written as code
* Each change is stored as a migration file
* Changes can be applied or rolled back safely

Example:

```bash
make run-migrations
```

---

## 3. Why Migrate

Migration helps avoid manual mistakes and keeps databases consistent.

### Key Reasons

* **Consistency Across Environments** → Same schema everywhere
* **Version Control** → DB changes tracked like code
* **Safe Updates** → Controlled execution
* **Rollback Support** → Easy revert
* **Automation** → Works with CI/CD

---

## 4. Key Features

| Feature              | Description                |
| -------------------- | -------------------------- |
| Versioned Migrations | Tracks schema changes      |
| Rollback Support     | Safe revert capability     |
| Environment Sync     | Keeps environments aligned |
| CI/CD Integration    | Automates deployment       |

---

## 5. Workflow

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

## 6. Installation Guide

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

## 7. Migration Commands (Common)

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

## 8. DB Schema Evolution Diagram

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

## 9. Liquibase and Migration Concept

* **Migration = Concept** (process of managing DB changes)
* **Liquibase = Tool** (implements migration)

### Comparison

| Tool      | Type            | Usage                |
| --------- | --------------- | -------------------- |
| Migrate   | CLI Tool        | Simple microservices |
| Liquibase | Enterprise Tool | Complex systems      |

---

## 10. Liquibase Example

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

## 11. Validation

After applying migrations, validate:

* Tables/columns are created as expected
* No errors in migration logs
* Application works with updated schema

---

## 12. Troubleshooting

| Issue                | Solution                      |
| -------------------- | ----------------------------- |
| Migration fails      | Check syntax & DB connection  |
| Version mismatch     | Sync migration history        |
| Rollback not working | Ensure rollback scripts exist |

---

## 13. Best Practices

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

## 14. Conclusion

Database migration ensures controlled and reliable schema changes. Using tools like Migrate or Liquibase improves consistency, reduces manual errors, and supports automated deployments.

---

## 15. Contact Information

| Name        | Email                                                                           |
| ----------- | ------------------------------------------------------------------------------- |
| Saransh Rai | [saransh.rai.snaatak@mygurukulam.co](mailto:saransh.rai.snaatak@mygurukulam.co) |

---

## 16. References

| Resource                | Link                                                                               |
| ----------------------- | ---------------------------------------------------------------------------------- |
| Liquibase Documentation | [https://www.liquibase.com/documentation](https://www.liquibase.com/documentation) |
| Flask-Migrate Docs      | [https://flask-migrate.readthedocs.io/](https://flask-migrate.readthedocs.io/)     |
| Alembic Docs            | [https://alembic.sqlalchemy.org/](https://alembic.sqlalchemy.org/)                 |



