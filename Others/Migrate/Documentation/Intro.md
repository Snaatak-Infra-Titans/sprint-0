# Migrate Introduction Documentation
<p align="center">
  <a href="https://www.liquibase.com/documentation">
    <img src="https://img.shields.io/badge/Liquibase-Documentation-blue?style=for-the-badge" />
  </a>
  <a href="https://alembic.sqlalchemy.org/en/latest/">
    <img src="https://img.shields.io/badge/Alembic-Documentation-green?style=for-the-badge" />
  </a>
  <a href="https://flask-migrate.readthedocs.io/">
    <img src="https://img.shields.io/badge/Flask--Migrate-Docs-orange?style=for-the-badge" />
  </a>
  <a href="https://martinfowler.com/articles/evodb.html">
    <img src="https://img.shields.io/badge/DB--Migration-Concepts-purple?style=for-the-badge" />
  </a>
</p>

| Author       | Created on | Version | Last updated by | Last edited on | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
| ------------ | ---------- | ------- | --------------- | -------------- | ------------ | ----------- | ----------- | ----------- |
| Mukesh Kharb | 16/04/2026 | 1.0     | Mukesh Kharb    | 16/04/2026     | Team         | Mohit Kumar |Faisal Khan  | Mahesh Kumar| 

---

## Table of Contents

* [Introduction](#introduction)
* [What is Migrate](#what-is-migrate)
* [Why Migrate](#why-migrate)
* [Key Features](#key-features)
* [Workflow](#workflow)
* [Migration Commands (Common)](#migration-commands-common)
* [DB Schema Evolution Diagram](#db-schema-evolution-diagram)
* [Liquibase and Migration Concept](#liquibase-and-migration-concept)
* [Liquibase Example](#liquibase-example)
* [Summary](#summary)

---

<a id="introduction"></a>

## Introduction

> [!NOTE]
> This section explains why migration is needed and where it fits in real projects.

When working on applications, the database structure keeps changing as new features are added. Managing these changes manually can quickly become confusing and error-prone.

Migration tools help handle this in a structured way. Instead of making direct changes in the database, we define changes as scripts and apply them in a controlled manner.

This makes it easier to keep all environments (development, testing, production) in sync.

---

<a id="what-is-migrate"></a>

## What is Migrate

> [!IMPORTANT]
> Migrate is a way to manage database changes using version-controlled scripts.

* It allows us to define database changes as code.
* Each change is saved as a migration file.
* These changes can be applied step by step or rolled back when needed.

### Example

```bash
make run-migrations
```

This command applies pending changes to the database.

---

<a id="why-migrate"></a>

## Why Migrate

> [!TIP]
> Migration helps avoid manual mistakes and keeps databases consistent.

### Key Reasons

* **Consistency Across Environments**
  All environments follow the same database structure.

* **Version Control for Database**
  Database changes are tracked just like application code.

* **Safe Updates**
  Changes are applied in a controlled way instead of directly modifying tables.

* **Rollback Support**
  If something breaks, changes can be reverted.

* **Automation**
  Works well with CI/CD pipelines.

---

<a id="key-features"></a>

## Key Features

| Feature              | Description                                    |
| -------------------- | ---------------------------------------------- |
| Versioned Migrations | Tracks schema changes using version files      |
| Auto Generation      | Generates migration scripts from model changes |
| Rollback Support     | Allows reverting changes safely                |
| Environment Sync     | Keeps all environments aligned                 |
| CI/CD Integration    | Automates migrations during deployment         |

---

<a id="workflow"></a>

## Workflow

```text
Update Model / Schema
        ↓
Generate Migration File
        ↓
Review Migration Script
        ↓
Apply Migration (Upgrade)
        ↓
Database Updated
```

---

<a id="migration-commands-common"></a>

## Migration Commands (Common)

> [!IMPORTANT]
> These commands are commonly used with tools like Alembic or Flask-Migrate.

### Initialize Migration

```bash
flask db init
```

Creates the migration setup.

---

### Generate Migration

```bash
flask db migrate -m "add user table"
```

Creates a migration file based on changes.

---

### Apply Migration

```bash
flask db upgrade
```

Applies changes to the database.

---

### Rollback Migration

```bash
flask db downgrade
```

Reverts the last change.

---

<a id="db-schema-evolution-diagram"></a>

## DB Schema Evolution Diagram

> [!TIP]
> Shows how database changes progress over time.

```text
Version 1
        ↓
Add Change
        ↓
Migration File
        ↓
Apply Migration
        ↓
Version 2
        ↓
Further Changes
        ↓
Version 3
```

---

<a id="liquibase-and-migration-concept"></a>

## Liquibase and Migration Concept

> [!NOTE]
> Liquibase is a tool used to manage migrations.

* Migration is the process of handling database changes.
* Liquibase is a tool that helps automate and track those changes.

In simple terms:

* Migration = concept
* Liquibase = tool

---

<a id="liquibase-example"></a>

## Liquibase Example

> [!IMPORTANT]
> This is a simple example of how changes are defined using Liquibase.

```xml
<databaseChangeLog>

    <changeSet id="1" author="mukesh">
        <createTable tableName="users">
            <column name="id" type="INT" autoIncrement="true">
                <constraints primaryKey="true" nullable="false"/>
            </column>
            <column name="name" type="VARCHAR(100)"/>
        </createTable>
    </changeSet>

    <changeSet id="2" author="mukesh">
        <addColumn tableName="users">
            <column name="email" type="VARCHAR(150)"/>
        </addColumn>
    </changeSet>

</databaseChangeLog>
```

### Run Migration

```bash
liquibase update
```

---

<a id="summary"></a>

## Summary

* Migration helps manage database changes in a structured way
* It keeps all environments consistent
* Tools like Liquibase automate the process
* It is essential for real-world applications

---

## References

* Liquibase Official Documentation
  [https://www.liquibase.com/documentation](https://www.liquibase.com/documentation)

* Alembic Documentation
  [https://alembic.sqlalchemy.org/en/latest/](https://alembic.sqlalchemy.org/en/latest/)

* Flask-Migrate Documentation
  [https://flask-migrate.readthedocs.io/](https://flask-migrate.readthedocs.io/)

* Database Migration Concepts (General Guide)
  [https://martinfowler.com/articles/evodb.html](https://martinfowler.com/articles/evodb.html)

---
