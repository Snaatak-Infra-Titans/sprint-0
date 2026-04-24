# requirements.txt - Documentation

<p align="center">
  <a href="https://docs.python.org/3/">
    <img src="https://img.shields.io/badge/python-dependency--management-blue" />
  </a>
  <a href="https://en.wikipedia.org/wiki/DevOps">
    <img src="https://img.shields.io/badge/usecase-devops%20%7C%20backend-green" />
  </a>
  <a href="https://en.wikipedia.org/wiki/Configuration_file">
    <img src="https://img.shields.io/badge/type-configuration-orange" />
  </a>
</p>

---

## Metadata

| Author       | Created On | Version | Last Updated By | Last Edited On | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer  |
| ------------ | ---------- | ------- | --------------- | -------------- | ------------ | ----------- | ----------- | ------------ |
| Mukesh Kharb | 15/04/2026 | 1.0     | Mukesh Kharb    | 15/04/2026     | Team         | Mohit Kumar | Faisal Khan | Mahesh Kumar |
| Mukesh Kharb | 22/04/2026 | 1.1     | Mukesh Kharb    | 22/04/2026     | Team         | Mohit Kumar | Faisal Khan | Mahesh Kumar |

---

## Table of Contents

* [Introduction](#introduction)
* [Why requirements.txt](#why-requirementstxt)
* [Versioning](#versioning)
* [Workflow](#workflow)
* [Commands](#commands)
* [Troubleshooting](#troubleshooting)
* [References](#references)
* [Contact Information](#contact-information)

---

## Introduction

Python projects depend on external libraries such as web frameworks, database drivers, and utilities. Managing these dependencies manually becomes difficult as projects grow.

The `requirements.txt` file is a simple and reliable way to list all required packages so that any system can install them in a consistent manner.

---

## Why requirements.txt

| Benefit          | Description                                  |
| ---------------- | -------------------------------------------- |
| Consistency      | Same dependencies across all environments    |
| Fast Setup       | Install everything using one command         |
| Reliability      | Prevents version mismatch issues             |
| Deployment Ready | Used directly in CI/CD and cloud deployments |

---

## Example of requirement.txt

```txt
flask==2.3.2
requests==2.31.0
redis==4.5.0
```

| Type           | Example       | Purpose                 |
| -------------- | ------------- | ----------------------- |
| Exact Version  | flask==2.3.2  | Stable production setup |
| Latest Allowed | requests>=2.0 | Flexible development    |

---

## Versioning

| Symbol | Meaning         |
| ------ | --------------- |
| ==     | Exact version   |
| >=     | Minimum version |
| <=     | Maximum version |
| !=     | Exclude version |

---

## Workflow

><img width="1200" height="800" alt="ChatGPT Image Apr 22, 2026, 09_27_47 PM" src="https://github.com/user-attachments/assets/17a0f064-9f47-4c73-a1de-9e9c49c883e8" />


---

## Commands

| Task             | Command                         |
| ---------------- | ------------------------------- |
| Install packages | pip install -r requirements.txt |
| Generate file    | pip freeze > requirements.txt   |
| List packages    | pip list                        |
| Upgrade package  | pip install --upgrade <package> |

---

## Troubleshooting

| Issue              | Cause             | Solution                        |
| ------------------ | ----------------- | ------------------------------- |
| Module not found   | Missing package   | Install using requirements file |
| Version conflict   | Incompatible libs | Adjust versions                 |
| Works locally only | Env mismatch      | Use same requirements file      |

---

## References

| Resource      | Link                                                                                                                                       |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| Official Docs | [https://pip.pypa.io/en/stable/reference/requirements-file-format/](https://pip.pypa.io/en/stable/reference/requirements-file-format/)     |
| Guide         | [https://www.freecodecamp.org/news/python-requirementstxt-explained/](https://www.freecodecamp.org/news/python-requirementstxt-explained/) |

---

## Contact Information

| Name         | Email                                                                             |
| ------------ | --------------------------------------------------------------------------------- |
| Mukesh Kharb | [mukesh.Kharb.snaatak@mygurukulam.co](mailto:mukesh.Kharb.snaatak@mygurukulam.co) |

---
