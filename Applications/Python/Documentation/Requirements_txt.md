# Documentation: requirements.txt (Python)

---

## Document Control

| Author       | Created on | Version | Last updated by | Last Edited On | Level           | Reviewer |
| ------------ | ---------- | ------- | --------------- | -------------- | --------------- | -------- |
| Mukesh Kharb | 2026-04-14 | 1.0     | Mukesh Kharb    | 2026-04-14     | Internal Review | Team     |

---

## Table of Contents

* [Introduction](#introduction)
* [Why requirements.txt (Problem Statement)](#why-requirementstxt-problem-statement)
* [Use Cases](#use-cases)
* [What is requirements.txt](#what-is-requirementstxt)
* [Dependency Versioning (Core Concept)](#dependency-versioning-core-concept)
* [Versioning Strategies (Best Practices)](#versioning-strategies-best-practices)
* [File Structure & Syntax](#file-structure--syntax)
* [Installation Workflow](#installation-workflow)
* [Best Practices (Instructor Criteria Focus)](#best-practices-instructor-criteria-focus)
* [Common Commands](#common-commands)
* [Troubleshooting](#troubleshooting)
* [Contact Information](#contact-information)
* [References](#references)

---

<a id="introduction"></a>

## Introduction

> [!NOTE]
> This section explains the purpose and importance of dependency management in Python projects.

In Python projects, applications depend on multiple external libraries. Managing these dependencies without a structured approach leads to inconsistent environments, deployment failures, and version conflicts.

The `requirements.txt` file provides a standardized and reproducible way to define and manage these dependencies.

---

<a id="why-requirementstxt-problem-statement"></a>

## Why requirements.txt (Problem Statement)

> [!WARNING]
> Lack of dependency control can lead to inconsistent environments and deployment failures.

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

<a id="use-cases"></a>

## Use Cases

> [!TIP]
> This section highlights practical scenarios where requirements.txt is used.

### 1. Developer Onboarding

```
pip install -r requirements.txt
```

### 2. CI/CD Pipelines

Automated builds use the file to install exact dependencies.

### 3. Production Deployment

Servers install controlled and tested versions of packages.

### 4. Microservices Architecture

Each service maintains its own dependency file for isolation.

---

<a id="what-is-requirementstxt"></a>

## What is requirements.txt

`requirements.txt` is a dependency declaration file containing a list of Python packages with optional version constraints.

Example:

```
flask==2.3.2
requests>=2.28.0
psycopg2-binary==2.9.9
```

Each entry defines:

* Package name
* Version rule

---

<a id="dependency-versioning-core-concept"></a>

## Dependency Versioning (Core Concept)

> [!IMPORTANT]
> Incorrect versioning can break applications or introduce security risks.

Dependency versioning controls which version of a package is installed.

It is critical because:

* Libraries evolve
* APIs change
* Backward compatibility is not guaranteed

Improper versioning leads to:

* Runtime errors
* Breaking changes
* Security vulnerabilities

---

<a id="versioning-strategies-best-practices"></a>

## Versioning Strategies (Best Practices)

> [!TIP]
> Follow these strategies to ensure stability and maintainability.

### 1. Exact Version (==) → Recommended for Production

```
flask==2.3.2
```

Ensures reproducibility and prevents unexpected updates.

---

### 2. Minimum Version (>=) → Flexible but Risky

```
flask>=2.0
```

Use case: Development
Risk: Breaking changes

---

### 3. Version Range → Balanced Approach

```
flask>=2.0,<3.0
```

Allows updates within a safe boundary and prevents major version breaks.

---

### 4. No Version → Not Recommended

```
flask
```

Installs latest version and is non-deterministic.

---

<a id="file-structure--syntax"></a>

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

```
# Core dependencies
flask==2.3.2
```

---

<a id="installation-workflow"></a>

## Installation Workflow

> [!NOTE]
> Follow these steps sequentially to install dependencies correctly.

### Step 1: Activate virtual environment (optional)

```
source venv/bin/activate
```

### Step 2: Install dependencies

```
pip install -r requirements.txt
```

### Step 3: Verify installation

```
pip list
```

---

<a id="best-practices-instructor-criteria-focus"></a>

## Best Practices (Instructor Criteria Focus)

> [!IMPORTANT]
> These guidelines align with production-grade DevOps standards.

### Why-focused Practices

* Always define versions
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

<a id="common-commands"></a>

## Common Commands

| Command                         | Description             |
| ------------------------------- | ----------------------- |
| pip install -r requirements.txt | Install dependencies    |
| pip freeze                      | Generate file           |
| pip list                        | View installed packages |
| pip uninstall package           | Remove package          |

---

<a id="troubleshooting"></a>

## Troubleshooting

> [!NOTE]
> Use this section to identify and resolve common issues.

| Issue                       | Cause                 | Solution                       |
| --------------------------- | --------------------- | ------------------------------ |
| Module not found            | Missing dependency    | Install using requirements.txt |
| Version conflict            | Incompatible versions | Adjust constraints             |
| Works locally not in server | Version mismatch      | Use exact versions             |

---

<a id="contact-information"></a>

## Contact Information

| Name         | Email                                                                             |
| ------------ | --------------------------------------------------------------------------------- |
| Mukesh Kharb | [mukesh.Kharb.snaatak@mygurukulam.co](mailto:mukesh.Kharb.snaatak@mygurukulam.co) |

---

<a id="references"></a>

## References

* [https://docs.python.org/3/](https://docs.python.org/3/)
* [https://pip.pypa.io/en/stable/](https://pip.pypa.io/en/stable/)

---

## Notes

This document strictly focuses on `requirements.txt` aligned with instructor evaluation criteria: Why, Use Case, and Dependency Versioning Best Practices.
