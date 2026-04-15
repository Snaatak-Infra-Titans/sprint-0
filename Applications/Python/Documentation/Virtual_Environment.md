# 📘 Common Stack | Applications | Python | Virtual Environment Documentation

---

## Author Table

| Author  | Created on | Version | Last updated by | Last Edited On | Pre Reviewer | L0 Reviewer | L1 Reviewer |
| ------- | ---------- | ------- | --------------- | -------------- | ------------ | ----------- | ----------- |
| Saransh | 15-04-2026 | 1.0     | Saransh Rai              | -              | -            | -           | -           |

---

## Table of Contents

* [Introduction](#introduction)
* [Purpose](#purpose)
* [What is Virtual Environment](#what-is-virtual-environment)
* [Why Virtual Environment](#why-virtual-environment)
* [How to Setup Virtual Environment](#how-to-setup-virtual-environment)

  * [Installation](#installation)
  * [Create Virtual Environment](#create-virtual-environment)
  * [Activate Virtual Environment](#activate-virtual-environment)
  * [Install Dependencies](#install-dependencies)
  * [Deactivate Virtual Environment](#deactivate-virtual-environment)
* [Directory Structure](#directory-structure)
* [Best Practices](#best-practices)
* [Use Cases](#use-cases)
* [Troubleshooting](#troubleshooting)
* [Contact Information](#contact-information)
* [References](#references)

---

## Introduction

A **Python Virtual Environment (venv)** is an isolated workspace that allows developers to install and manage Python packages separately for each project.

Instead of installing all libraries globally on the system, virtual environments ensure that every project has its own dependencies, avoiding conflicts and maintaining stability.

---

## Purpose

This document explains:

* What a virtual environment is
* Why it is used
* How to set it up
* Best practices and real-world usage

---

## What is Virtual Environment

A virtual environment is a **self-contained directory** that includes:

* A Python interpreter
* Installed packages through pip
* Project-specific dependencies

It behaves like an independent Python installation for a specific project.

---

## Why Virtual Environment

### Dependency Isolation

Different projects may require different versions of the same library. Virtual environments prevent conflicts.

### Clean System Environment

Avoids cluttering the global Python installation.

### Version Control

You can control package versions using `requirements.txt`.

### Easy Collaboration

Team members can recreate the same setup easily.

### Safe Testing

Test new libraries without affecting other projects.

---

## How to Setup Virtual Environment

### Installation

```bash
sudo apt update
sudo apt install python3-venv -y
```

### Create Virtual Environment

```bash
python3 -m venv venv
```

### Activate Virtual Environment

```bash
source venv/bin/activate
```

### Install Dependencies

```bash
pip install flask
pip install -r requirements.txt
```

### Deactivate Virtual Environment

```bash
deactivate
```

---

## Directory Structure

```text
project/
│
├── venv/               # Virtual environment
├── app.py              # Application code
├── requirements.txt    # Dependencies list
└── config.yaml         # Configuration file
```

---

## Best Practices

* Create a separate virtual environment for each project
* Do not commit `venv/` to Git
* Maintain `requirements.txt`
* Use fixed versions of packages
* Activate environment before use

---

## Use Cases

### Multiple Projects

Run multiple projects with different dependencies without conflict.

### Deployment

```bash
pip install -r requirements.txt
```

### Testing

Safely test different versions of libraries.

---

## Troubleshooting

| Issue             | Reason             | Solution               |
| ----------------- | ------------------ | ---------------------- |
| venv not found    | Missing package    | Install python3-venv   |
| Activation issue  | Wrong path         | Use correct command    |
| Module not found  | Missing dependency | Install using pip      |
| Permission denied | Lack of access     | Use proper permissions |

---

## Contact Information

| Name    | Email                                                   |
| ------- | ------------------------------------------------------- |
| Saransh | saransh.rai.snaatak@mygurukulam.co |

---

## References

* Python Documentation: [https://docs.python.org/3/library/venv.html](https://docs.python.org/3/library/venv.html)
* Pip Documentation: [https://pip.pypa.io/en/stable/](https://pip.pypa.io/en/stable/)

---
