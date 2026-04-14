# Documentation: Requirements.txt (Python)

---

| **Author**   | **Created on** | **Version** | **Last updated by** | **Last Edited On** | **Level**       | **Reviewer** |
| ------------ | -------------- | ----------- | ------------------- | ------------------ | --------------- | ------------ |
| Mukesh Kharb | 2026-04-14     | 3.0         | Mukesh Kharb        | 2026-04-14         | Internal Review | Team         |

---

## Table of Contents

* Introduction
* Why requirements.txt (Problem Statement)
* Use Cases
* What is requirements.txt
* Dependency Versioning (Core Concept)
* Versioning Strategies (Best Practices)
* File Structure & Syntax
* Installation Workflow
* Best Practices
* Common Commands
* Troubleshooting
* Contact Information
* References

---

## Introduction

In Python projects, applications depend on multiple external libraries. Managing these dependencies without a structured approach leads to **inconsistent environments**, **deployment failures**, and **version conflicts**.

The `requirements.txt` file provides a **standardized and reproducible way** to define and manage these dependencies.

---

## Why requirements.txt (Problem Statement)

Without `requirements.txt`:

* Different developers install different versions of packages
* Code works on one system but fails on another
* Production deployments become unpredictable
* Debugging dependency issues becomes complex

### Example Problem

Developer A:

```
Flask 2.3
```

Developer B:

```
Flask 3.0
```

Application may break due to API changes.

### Solution

`requirements.txt` ensures:

* Same versions across all environments
* Deterministic builds
* Reliable deployments

---

## Use Cases

### 1. Developer Onboarding

New developer can install all dependencies using:

```bash
pip install -r requirements.txt
```

### 2. CI/CD Pipelines

Automated builds use the file to install exact dependencies.

### 3. Production Deployment

Servers install controlled and tested versions of packages.

### 4. Microservices Architecture

Each service maintains its own dependency file for isolation.

---

## What is requirements.txt

`requirements.txt` is a **dependency declaration file** containing a list of Python packages with optional version constraints.

Example:

```txt
flask==2.3.2
requests>=2.28.0
psycopg2-binary==2.9.9
```

Each entry defines:

* Package name
* Version rule

---

## Dependency Versioning (Core Concept)

Dependency versioning controls **which version of a package is installed**.

It is critical because:

* Libraries evolve
* APIs change
* Backward compatibility is not guaranteed

Improper versioning leads to:

* Runtime errors
* Breaking changes
* Security vulnerabilities

---

## Versioning Strategies (Best Practices)

### 1. Exact Version (==) → **Recommended for Production**

```txt
flask==2.3.2
```

**Why:**

* Ensures reproducibility
* Prevents unexpected updates

---

### 2. Minimum Version (>=) → **Flexible but Risky**

```txt
flask>=2.0
```

**Use Case:** Development environments

**Risk:** New versions may introduce breaking changes

---

### 3. Version Range → **Balanced Approach**

```txt
flask>=2.0,<3.0
```

**Why:**

* Allows updates within safe boundary
* Prevents major version breaks

---

### 4. No Version → **Not Recommended**

```txt
flask
```

**Problem:**

* Installs latest version
* Completely non-deterministic

---

## File Structure & Syntax

### Basic Format

```
package==version
```

### Supported Syntax

| Syntax          | Meaning         |
| --------------- | --------------- |
| flask==2.3.2    | Fixed version   |
| requests>=2.0   | Minimum version |
| numpy<=1.25     | Maximum version |
| pandas!=1.5.0   | Exclude version |
| flask>=2.0,<3.0 | Version range   |

### Comments

```txt
# Core dependencies
flask==2.3.2
```

---

## Installation Workflow

### Step 1: (Optional but Recommended) Activate virtual environment

```bash
source venv/bin/activate
```

### Step 2: Install dependencies

```bash
pip install -r requirements.txt
```

### Step 3: Verify installation

```bash
pip list
```

---

## Best Practices (Instructor Criteria Focus)

### Why-focused Practices

* Always define versions to avoid ambiguity
* Avoid floating dependencies

### Use Case-driven Practices

* Use exact versions in production
* Use ranges in development

### Dependency Versioning Practices

* Prefer `==` for stability
* Use `<` to prevent major upgrades
* Regularly review and update versions

### Additional Practices

* Keep file minimal
* Remove unused dependencies
* Maintain separate files for dev if needed

---

## Common Commands

| Command                         | Description             |
| ------------------------------- | ----------------------- |
| pip install -r requirements.txt | Install dependencies    |
| pip freeze                      | Generate file           |
| pip list                        | View installed packages |
| pip uninstall package           | Remove package          |

---

## Troubleshooting

| Issue                       | Cause                 | Solution                       |
| --------------------------- | --------------------- | ------------------------------ |
| Module not found            | Missing dependency    | Install using requirements.txt |
| Version conflict            | Incompatible versions | Adjust constraints             |
| Works locally not in server | Version mismatch      | Use exact versions             |

---

## Contact Information

| Name         | Email                                                                             |
| ------------ | --------------------------------------------------------------------------------- |
| Mukesh Kharb | [mukesh.Kharb.snaatak@mygurukulam.co](mailto:mukesh.Kharb.snaatak@mygurukulam.co) |

---

## References

* Python Official Documentation
* pip Documentation

---

## Notes

This document strictly focuses on `requirements.txt` aligned with instructor evaluation criteria: **Why, Use Case, and Dependency Versioning Best Practices**.
