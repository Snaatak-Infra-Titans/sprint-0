# SOP: requirements.txt

## Document Details

| Author      | Created    | Version | Last updated by | Last Edited On       | L0 Reviewer | L1 Reviewer   | L2 Reviewer   |
| ----------- | ---------- | ------- | --------------- | -------------------- | ----------- | ------------- | ------------- |
| Saransh Rai | 2026-04-13 | 1.0     | Saransh Rai     | .................... |             | ............. | ............. |

---

## Table of Contents

1. [Scope](#1-scope)
2. [Purpose](#2-purpose)
3. [Installation from requirements.txt](#3-installation-from-requirementstxt)
4. [Generating Dependencies](#4-generating-dependencies)
5. [Troubleshooting](#5-troubleshooting)
6. [Reference](#6-reference)
7. [Contact](#7-contact)

---

## 1. Scope

This SOP defines the standard procedures for:

* Installing dependencies using `requirements.txt`
* Generating dependency files
* Troubleshooting common issues related to dependency management

---

## 2. Purpose

The purpose of this document is to:

* Ensure consistent dependency management across environments
* Standardize installation and dependency generation processes
* Minimize environment-related issues during development and deployment

---

## 3. Installation from requirements.txt

### Step 1: Activate Virtual Environment

```
python -m venv venv
source venv/bin/activate      # Linux/Mac
venv\Scripts\activate         # Windows
```

### Step 2: Install Dependencies

```
pip install -r requirements.txt
```

### Step 3: Verify Installation

```
pip list
```

---

## 4. Generating Dependencies

### Generate requirements.txt from Existing Environment

```
pip freeze > requirements.txt
```

### Verify Generated File

* Ensure only required dependencies are included
* Remove unnecessary or unused packages

---

## 5. Troubleshooting

### Issue: Package Installation Failure

* Verify Python and pip versions
* Upgrade pip:

```
pip install --upgrade pip
```

### Issue: Version Conflicts

* Check conflicting package versions
* Update or align versions in `requirements.txt`

### Issue: Missing Dependencies

* Reinstall using:

```
pip install -r requirements.txt
```

### Issue: Environment Mismatch

* Ensure virtual environment is activated
* Recreate environment if required

---

## 6. Reference

* [https://pip.pypa.io/en/stable/reference/requirements-file-format/](https://pip.pypa.io/en/stable/reference/requirements-file-format/)

---

## 7. Contact

| Name        | Email Id                                                  |
| ----------- | --------------------------------------------------------- |
| Saransh Rai | saransh.rai.snaatak@mygurukulam.co |
