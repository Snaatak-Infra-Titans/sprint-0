# SOP for Python Virtual Environment (venv)

| Author           | Created on | Version | Last updated by | Last edited on | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer      |
|------------------|------------|---------|-----------------|----------------|--------------|-------------|-------------|------------------|
| Shivam Uniyal    | 15-04-2026 | v1.0    | Shivam Uniyal   | 15-04-2026     | Team         | Anuj Jain   | Prashant    | Piyush Upadhyay  |

---

## Table of Contents

1. [Introduction](#introduction)  
2. [Purpose](#purpose)  
3. [Prerequisites](#prerequisites)  
4. [System Requirements](#system-requirements)  
5. [Step-by-Step Procedure](#step-by-step-procedure)  
6. [Troubleshooting](#troubleshooting)  
7. [Best Practices](#best-practices)  
8. [FAQs](#faqs)  
9. [Contact Information](#contact-information)  
10. [References](#references)   

---

## 1. Introduction

A Python Virtual Environment (venv) is an isolated workspace that allows developers to create separate environments for different Python projects. Each environment contains its own Python interpreter and installed packages, ensuring that dependencies from one project do not interfere with another.

In real-world DevOps and development workflows, multiple projects often require different versions of the same library. Virtual environments help manage these dependencies efficiently, improve reproducibility, and maintain a clean system environment without polluting the global Python installation.

---

## 2. Purpose

The purpose of this SOP is to provide a structured and easy-to-follow guide for managing Python virtual environments in Ubuntu.

This document helps users to:

- Create and configure a virtual environment  
- Activate and work inside the environment  
- Install and manage Python packages  
- Export dependencies for reuse  
- Deactivate and delete environments  
- Troubleshoot common issues  

Following this SOP ensures consistency, avoids dependency conflicts, and aligns with DevOps best practices for environment isolation.

---

## 3. Prerequisites

Before proceeding, ensure the following requirements are met:

- Ubuntu 24.04 installed  
- Python3 installed and configured  
- Terminal access  
- Basic understanding of Linux commands  
- Internet connectivity (for installing packages)

---

## 4. System Requirements

| Component | Minimum Requirement |
|----------|-------------------|
| CPU      | Dual Core          |
| RAM      | 4 GB               |
| Disk     | 10 GB free space   |
| OS       | Ubuntu 24.04       |

---

## 5. Step-by-Step Procedure

### Step 1: Install venv package

The `python3-venv` package provides the functionality required to create virtual environments. Install it if not already available.

```bash
sudo apt update
sudo apt install python3-venv -y
```

---

### Step 2: Create Virtual Environment

Create a new virtual environment using the following command:

```bash
python3 -m venv myenv
```

This will create a directory named `myenv` containing the isolated Python environment.

Verify creation:

```bash
ls
```

---

### Step 3: Activate Virtual Environment

Activate the environment to start using it:

```bash
source myenv/bin/activate
```

Once activated:
- The terminal prompt will change to show `(myenv)`
- All Python and pip commands will now run inside this environment

---

### Step 4: Install Python Packages

Install required Python packages using pip:

```bash
pip install requests
```

You can install multiple packages as needed for your project.

Verify installed packages:

```bash
pip list
```

---

### Step 5: Freeze Dependencies

To save all installed dependencies into a file (useful for sharing or deployment):

```bash
pip freeze > requirements.txt
```

This file can later be used to recreate the environment.

Check contents:

```bash
cat requirements.txt
```

---

### Step 6: Deactivate Virtual Environment

Exit the virtual environment using:

```bash
deactivate
```

After deactivation:
- The `(myenv)` prefix will disappear  
- System Python will be used again  

---

### Step 7: Delete Virtual Environment

To completely remove the environment:

```bash
rm -rf myenv
```

This deletes all installed packages and the environment directory.

---

## 6. Troubleshooting

| Issue | Possible Cause | Solution |
|------|---------------|----------|
| Activation not working | Incorrect command | Use `source myenv/bin/activate` |
| Permission denied | Missing execution rights | Run `chmod +x myenv/bin/activate` |
| pip not found | pip not installed | Run `python3 -m ensurepip --upgrade` |
| Wrong Python version | Multiple Python versions installed | Verify using `python3 --version` |
| Environment not activating | Wrong directory | Navigate to correct folder before activating |
| Packages not installing | Network issue or pip outdated | Run `pip install --upgrade pip` |

---

## 7. Best Practices

- Always use a virtual environment for every project  
- Do not install packages globally unless required  
- Use `requirements.txt` to maintain dependency consistency  
- Use meaningful environment names (e.g., project-specific)  
- Regularly update pip and packages  
- Avoid committing the virtual environment folder to Git (add to `.gitignore`)  

---

## 8. FAQs

**Q1. What is a virtual environment?**  
It is an isolated Python environment used to manage dependencies separately.

**Q2. Why use virtual environments?**  
To avoid conflicts between different projects and maintain a clean development setup.

**Q3. How do I activate the environment?**  
```
source myenv/bin/activate
```

**Q4. How do I install dependencies from a file?**  
```
pip install -r requirements.txt
```

**Q5. Can I create multiple virtual environments?**  
Yes, you can create multiple environments for different projects.

---

## 9. Contact Information

| Name           | Email ID |
|----------------|----------|
| Shivam Uniyal  | shivam.uniyal.snaatak@mygurukulam.co |

---

## 10. References

| Link | Description |
|------|------------|
| https://docs.python.org/3/library/venv.html | Official Python venv documentation |
| https://ubuntu.com | Ubuntu documentation |
