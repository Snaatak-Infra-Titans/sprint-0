# Common Stack | Others | Migrate | SOP for Migrate

## Description

Step by step installation guide

---

## Author Table

| Author      | Created on | Version | Last updated by | Last Edited On | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
| ----------- | ---------- | ------- | --------------- | -------------- | ------------ | ----------- | ----------- | ----------- |
| Saransh Rai | 19-04-2026 | 1.1     | Saransh Rai     | 19-04-2026     | -            | -           | -           | -           |

---

## Table of Contents

* Introduction
* What is Migrate
* Why Migrate
* Key Features
* Workflow
* Installation Guide
* Migration Commands (Common)
* DB Schema Evolution Diagram
* Liquibase and Migration Concept
* Liquibase Example
* Summary

---

## Introduction

When working on applications, the database structure keeps changing as new features are added. Managing these changes manually can quickly become confusing and error-prone.

Migration tools help handle this in a structured way. Instead of making direct changes in the database, we define changes as scripts and apply them in a controlled manner.

This ensures all environments (development, testing, production) remain consistent.

---

## What is Migrate

Migrate is a way to manage database changes using version-controlled scripts.

* Database changes are written as code
* Each change is stored as a migration file
* Changes can be applied or rolled back safely

Example:

```bash
make run-migrations
```

---

## Why Migrate

Migration helps avoid manual mistakes and keeps databases consistent.

### Key Reasons

* **Consistency Across Environments** → Same schema everywhere
* **Version Control** → DB changes tracked like code
* **Safe Updates** → Controlled execution
* **Rollback Support** → Easy revert
* **Automation** → Works with CI/CD

---

## Key Features

| Feature              | Description                |
| -------------------- | -------------------------- |
| Versioned Migrations | Tracks schema changes      |
| Rollback Support     | Safe revert capability     |
| Environment Sync     | Keeps environments aligned |
| CI/CD Integration    | Automates deployment       |

---

## Workflow

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

## Installation Guide

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

## Migration Commands (Common)

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

## DB Schema Evolution Diagram

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

## Liquibase and Migration Concept

* **Migration = Concept** (process of managing DB changes)
* **Liquibase = Tool** (implements migration)

### Comparison

| Tool      | Type            | Usage                |
| --------- | --------------- | -------------------- |
| Migrate   | CLI Tool        | Simple microservices |
| Liquibase | Enterprise Tool | Complex systems      |

---

## Liquibase Example

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

## Summary

* Migration manages database changes in structured way
* Keeps environments consistent
* Supports rollback and automation
* Tools like Liquibase and Migrate implement it

---

## References

* Liquibase Docs: [https://www.liquibase.com/documentation](https://www.liquibase.com/documentation)
* Flask-Migrate Docs: [https://flask-migrate.readthedocs.io/](https://flask-migrate.readthedocs.io/)
* Alembic Docs: [https://alembic.sqlalchemy.org/](https://alembic.sqlalchemy.org/)
