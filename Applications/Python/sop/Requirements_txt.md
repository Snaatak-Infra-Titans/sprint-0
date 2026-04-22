<p align="center">
  <img src="https://cdn-icons-png.flaticon.com/512/919/919825.png" width="100" />
</p>

<h1 align="center">📄 SOP: requirements.txt</h1>

<p align="center">
  <b>Python Dependency Management Guide</b><br>
  <sub>Best Practices • Installation • Version Control • Optimization</sub>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.x-blue?logo=python">
  <img src="https://img.shields.io/badge/Dependencies-Managed-success">
  <img src="https://img.shields.io/badge/Platform-Ubuntu-orange?logo=ubuntu">
</p>

---

## Document Details

| Author      | Created    | Version | Last updated by | Last Edited On | L0 Reviewer | L1 Reviewer     | L2 Reviewer     |
| ----------- | ---------- | ------- | --------------- | -------------- | ----------- | --------------- | --------------- |
| Saransh Rai | 2026-04-13 | 1.1     | Saransh Rai     | 2026-04-22     | Anuj Jain   | Prashant Sharma | Piyush Upadhyay |

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [Purpose](#2-purpose)
3. [Prerequisites](#3-prerequisites)
4. [Installation from requirements.txt](#4-installation-from-requirementstxt)
5. [Generating Dependencies](#5-generating-dependencies)
6. [Troubleshooting](#6-troubleshooting)
7. [Best Practices](#7-best-practices)
8. [Conclusion](#8-conclusion)
9. [Contact Information](#9-contact-information)
10. [References](#10-references)

---

## 1. Introduction

This Standard Operating Procedure (SOP) provides guidelines for managing Python project dependencies using the `requirements.txt` file. It ensures that all developers and environments use consistent package versions, reducing compatibility issues and improving project stability.

<p align="center">
  <b>Developer</b> → <b>requirements.txt</b> → <b>Environment</b>
</p>

<p align="center">
  <sub>Defines dependencies → Stores versions → Installs packages</sub>
</p>

---

## 2. Purpose

The purpose of this document is to:

* Ensure consistent dependency management across environments
* Standardize installation and dependency generation processes
* Minimize environment-related issues during development and deployment
* Improve reproducibility of Python environments

---

## 3. Prerequisites

Before proceeding, ensure the following prerequisites are met:

* Python installed (recommended version: 3.8 or above)
* pip (Python package manager) installed and updated
* Basic understanding of command line/terminal usage
* Access to project repository containing `requirements.txt`

<img width="832" height="195" alt="image" src="https://github.com/user-attachments/assets/0d0bb849-083d-4ca0-b9a4-20b7e2ea73c2" />


---

## 4. Installation from requirements.txt

### Step 1: Create and Activate Virtual Environment

```bash
python -m venv venv
source venv/bin/activate      # Linux/Mac
venv\Scripts\activate         # Windows
```

📌 **Image Placeholder:** Screenshot of terminal showing virtual environment activation

---

### Step 2: Install Dependencies

```bash
pip install -r requirements.txt
```

📌 **Image Placeholder:** Screenshot of successful dependency installation

---

### Step 3: Verify Installation

```bash
pip list
```

📌 **Image Placeholder:** Screenshot of installed packages list

---

## 5. Generating Dependencies

### Generate requirements.txt from Existing Environment

```bash
pip freeze > requirements.txt
```

📌 **Image Placeholder:** Screenshot of generated requirements.txt file

---

### Validate Generated File

* Ensure only required dependencies are included
* Remove unnecessary or unused packages
* Confirm correct versions are captured

📌 **Image Placeholder:** Example of clean vs cluttered requirements.txt

---

## 6. Troubleshooting

| Issue                        | Possible Cause                        | Resolution                                                   |
| ---------------------------- | ------------------------------------- | ------------------------------------------------------------ |
| Package Installation Failure | Outdated pip / incompatible Python    | Upgrade pip using `pip install --upgrade pip`                |
| Version Conflicts            | Conflicting package versions          | Align versions in `requirements.txt`                         |
| Missing Dependencies         | Incomplete installation               | Re-run `pip install -r requirements.txt`                     |
| Environment Mismatch         | Wrong or inactive virtual environment | Activate correct environment or recreate virtual environment |

📌 **Image Placeholder:** Error screenshot example (e.g., pip install failure)

---

## 7. Best Practices

| Practice                   | Description                                                   |
| -------------------------- | ------------------------------------------------------------- |
| Use Virtual Environments   | Always isolate project dependencies using venv                |
| Pin Versions               | Use exact versions (e.g., `package==1.2.3`) for consistency   |
| Clean Dependencies         | Remove unused packages before committing                      |
| Separate Requirement Files | Maintain different files for dev and production               |
| Regular Updates            | Periodically update dependencies while checking compatibility |
| Review Before Commit       | Validate requirements.txt before pushing to version control   |

📌 **Image Placeholder:** Example of well-structured requirements.txt

---

## 8. Conclusion

Proper management of dependencies using `requirements.txt` ensures consistency, reduces errors, and improves collaboration across teams. Following this SOP will help maintain stable and reproducible environments.

---

## 9. Contact Information

| Name        | Email Id                                                                        |
| ----------- | ------------------------------------------------------------------------------- |
| Saransh Rai | [saransh.rai.snaatak@mygurukulam.co](mailto:saransh.rai.snaatak@mygurukulam.co) |

---

## 10. References

| Source/Organization               | Description                                        | Link                                                                                                                                   |
| --------------------------------- | -------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| Python Packaging Authority (PyPA) | Official documentation for requirements.txt format | [https://pip.pypa.io/en/stable/reference/requirements-file-format/](https://pip.pypa.io/en/stable/reference/requirements-file-format/) |
