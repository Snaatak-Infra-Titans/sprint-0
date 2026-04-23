<p align="center">
  <img width="1000" height="420" alt="image" src="https://github.com/user-attachments/assets/c6234238-3dad-4597-9dcc-474ee67f07ab" />
  <br/>
</p>


<h1 align="center">Common Stack | Applications | Python | Virtual Environment Documentation</h1>

<p align="center">

---

## Author Table

| **Author**  | **Created on** | **Version** | **Last updated by** | **Last Edited On** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ----------- | -------------- | ----------- | ------------------- | ------------------ | --------------- | --------------- | --------------- |
| Saransh Rai | 19-04-2026     | 1.1         | Saransh Rai         | 19-04-2026         |  Anuj Jain      | Prashant Sharma | Piyush Upadhyay |

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [Purpose](#2-purpose)
3. [What is Virtual Environment](#3-what-is-virtual-environment)
4. [Why Virtual Environment](#4-why-virtual-environment)
5. [Setup Virtual Environment](#5-setup-virtual-environment)
6. [Directory Structure](#6-directory-structure)
7. [Best Practices](#7-best-practices)
8. [Use Cases](#8-use-cases)
9. [Troubleshooting](#9-troubleshooting)
10. [Conclusion](#10-conclusion)
11. [Contact Information](#11-contact-information)
12. [References](#12-references)

---

## 1. Introduction

A Python Virtual Environment (venv) is an isolated workspace that allows developers to install and manage Python packages separately for each project.

Instead of installing all libraries globally on the system, virtual environments ensure that every project has its own dependencies, avoiding conflicts and maintaining stability.

---

## 2. Purpose

This document explains:

* What a virtual environment is
* Why it is used
* How to set it up
* Best practices and real-world usage

---

## 3. What is Virtual Environment

A virtual environment is a self-contained directory that includes:

* A Python interpreter
* Installed packages through pip
* Project-specific dependencies

It behaves like an independent Python installation for a specific project.

---

## 4. Why Virtual Environment

* **Dependency Isolation** – Prevents conflicts between different project dependencies
* **Clean System Environment** – Avoids cluttering global Python installation
* **Version Control** – Manage package versions using `requirements.txt`
* **Easy Collaboration** – Teams can replicate the same setup easily
* **Safe Testing** – Test libraries without impacting other projects

---

## 5. Setup Virtual Environment

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

## 6. Directory Structure

```
project/
│
├── venv/               # Virtual environment
├── app.py              # Application code
├── requirements.txt    # Dependencies list
└── config.yaml         # Configuration file
```

---

## 7. Best Practices

* Create a separate virtual environment for each project
* Do not commit `venv/` to Git
* Maintain `requirements.txt`
* Use fixed versions of packages
* Always activate environment before use

---

## 8. Use Cases

| **Use Case**      | **Description**                                                    |
| ----------------- | ------------------------------------------------------------------ |
| Multiple Projects | Run multiple projects with different dependencies without conflict |
| Deployment        | Install dependencies using `pip install -r requirements.txt`       |
| Testing           | Safely test different versions of libraries                        |

---

## 9. Troubleshooting

| **Issue**         | **Reason**         | **Solution**           |
| ----------------- | ------------------ | ---------------------- |
| venv not found    | Missing package    | Install python3-venv   |
| Activation issue  | Wrong path         | Use correct command    |
| Module not found  | Missing dependency | Install using pip      |
| Permission denied | Lack of access     | Use proper permissions |

---

## 10. Conclusion

Using Python virtual environments enables developers to isolate project dependencies, maintain a clean system environment, and ensure consistent application behavior across different setups. By leveraging virtual environments, teams can easily manage package versions, collaborate efficiently, and safely test new libraries without impacting other projects. This approach enhances reliability, reproducibility, and overall development efficiency, making it a fundamental practice in modern Python development.

---

## 11. Contact Information

| **Name**    | **Email**                                                                       |
| ----------- | ------------------------------------------------------------------------------- |
| Saransh Rai | [saransh.rai.snaatak@mygurukulam.co](mailto:saransh.rai.snaatak@mygurukulam.co) |

---

## 12. References

| **Topic**                       | **Link**                                                                                   |
| ------------------------------- | ------------------------------------------------------------------------------------------ |
| Python Virtual Environment Docs | [https://docs.python.org/3/library/venv.html](https://docs.python.org/3/library/venv.html) |
| Pip Documentation               | [https://pip.pypa.io/en/stable/](https://pip.pypa.io/en/stable/)                           |
