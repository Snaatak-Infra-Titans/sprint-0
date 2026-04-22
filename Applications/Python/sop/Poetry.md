# SOP: Common Stack | Applications | Python | Poetry

---

## Author Table

| **Author** | **Created on** | **Version** | **Last updated by** | **Last Edited On** | **Pre Reviewer** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ---------- | -------------- | ----------- | ------------------- | ------------------ | ---------------- | --------------- | --------------- | --------------- |
| Ankita     | 17-04-2026     | v1.1        | Ankita              | 21-04-2026         |    Team          |  Komal Jaiswal  |  Akshit Kapil   |   Mahesh Kumar  |

---

## Table of Contents

1. [Overview](#overview)
2. [Purpose](#purpose)
3. [Prerequisites](#prerequisites)
4. [Step-by-Step Implementation](#step-by-step-implementation)

   * Step 0: Verify System Setup
   * Step 1: Install Poetry
   * Step 2: Configure Environment
   * Step 3: Create New Project
   * Step 4: Add Dependencies
   * Step 5: Install Dependencies
   * Step 6: Activate Environment
   * Step 7: Run Application
   * Step 8: Validation
5. [Architecture & Workflow](#architecture--workflow)
6. [Common Commands](#common-commands)
7. [Troubleshooting](#troubleshooting)
8. [Best Practices](#best-practices)
9. [Contact Information](#contact-information)
10. [References](#references)

---

## Overview

Poetry is a dependency management and packaging tool for Python that simplifies project setup, dependency handling, and virtual environment management.

It is widely used in modern Python development and DevOps workflows to ensure reproducibility and clean project structure.

---

## Purpose

This SOP provides a step-by-step procedure to install and use Poetry for Python projects, including dependency management, environment setup, and execution.

---

## Prerequisites

* Ubuntu 20.04 / 22.04 / 24.04
* Python 3.8+
* Internet access
* sudo privileges

Verify Python:

```bash
python3 --version
```

---

## Step-by-Step Implementation

### Step 0: Verify System Setup

Ensure Python and curl are installed:

```bash
python3 --version
curl --version
```

<img width="866" height="692" alt="image" src="https://github.com/user-attachments/assets/83367a67-9b9a-4410-b2d6-131a6991d518" />

---

### Step 1: Install Poetry

```bash
curl -sSL https://install.python-poetry.org | python3 -
```

<img width="866" height="651" alt="image" src="https://github.com/user-attachments/assets/4e221e7b-b7d6-4ff7-9200-dc84ea678813" />

---

### Step 2: Configure Environment

Add Poetry to PATH:

```bash
export PATH="$HOME/.local/bin:$PATH"
```

Reload shell:

```bash
source ~/.bashrc
```

Verify installation:

```bash
poetry --version
```
<img width="866" height="629" alt="image" src="https://github.com/user-attachments/assets/0f82fa0c-d3ff-4cdb-b553-32dc1cd24e85" />

---

### Step 3: Create New Project

```bash
poetry new my-project
```

Navigate to project:

```bash
cd my-project
```

---

### Step 4: Add Dependencies

```bash
poetry add requests
```
<img width="866" height="541" alt="image" src="https://github.com/user-attachments/assets/14825ccb-1639-409d-bc27-da5ba279bc16" />

Add dev dependency:

```bash
poetry add pytest --group dev
```
<img width="866" height="453" alt="image" src="https://github.com/user-attachments/assets/8b89d526-c700-4207-8cb3-a97f2bf540f1" />

---

### Step 5: Install Dependencies

```bash
poetry install
```
<img width="866" height="255" alt="image" src="https://github.com/user-attachments/assets/731877b1-aeaa-4b86-8661-2ca4fc085950" />

---

### Step 6: Activate Environment

```bash
poetry env activate
```
<img width="866" height="189" alt="image" src="https://github.com/user-attachments/assets/fba524ab-5d40-499c-936f-e73a24a80554" />

---

### Step 7: Run Application

```bash
poetry run python src/my_project/app.py
```
<img width="866" height="299" alt="image" src="https://github.com/user-attachments/assets/eb290f43-c2ac-4d33-88a2-56f89b73201c" />

---

### Step 8: Validation

Check installed packages:

```bash
poetry show
```
<img width="866" height="365" alt="image" src="https://github.com/user-attachments/assets/148de32e-aad2-4a8d-b1c2-ea7a32821f9a" />

Check virtual environment:

```bash
poetry env info
```
<img width="866" height="497" alt="image" src="https://github.com/user-attachments/assets/3b998e3b-2436-4327-b0a1-261a8dc1e505" />

Expected Output:

* Poetry version displayed
* Virtual environment path available
* Dependencies listed successfully

---

## Architecture & Workflow

```
Developer → Poetry → Virtual Environment → Dependencies → Python Application
```

Workflow:

1. Developer creates project using Poetry
2. Dependencies are added via pyproject.toml
3. Poetry creates isolated virtual environment
4. Application runs inside managed environment

---

## Common Commands

| Command        | Description                 |
| -------------- | --------------------------- |
| poetry new     | Create new project          |
| poetry init    | Initialize existing project |
| poetry add     | Add dependency              |
| poetry remove  | Remove dependency           |
| poetry install | Install dependencies        |
| poetry env activate   | Activate environment        |
| poetry run     | Run commands                |
| poetry show    | List dependencies           |

---

## Troubleshooting

| Issue               | Cause            | Solution            |
| ------------------- | ---------------- | ------------------- |
| poetry not found    | PATH not set     | Add to PATH         |
| install fails       | network issue    | check internet      |
| env not activating  | shell issue      | use poetry run      |
| dependency conflict | version mismatch | update dependencies |

---

## Best Practices

* Always commit `pyproject.toml` and `poetry.lock`
* Use virtual environments for isolation
* Avoid global installations
* Separate dev and production dependencies
* Keep dependencies updated

---

## Contact Information

| Name   | Email                                                                             |
| ------ | --------------------------------------------------------------------------------- |
| Ankita | [ankita.singh.snaatak@mygurukulam.co](mailto:ankita.singh.snaatak@mygurukulam.co) |

---

## References

| Topic       | Link                                                               |
| ----------- | ------------------------------------------------------------------ |
| Poetry Docs | [https://python-poetry.org/docs/](https://python-poetry.org/docs/) |
| Python Docs | [https://docs.python.org/3/](https://docs.python.org/3/)           |
