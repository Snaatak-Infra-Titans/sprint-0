# Python Installation SOP

---

| Author       | Created on | Version | Last updated by | Last edited on | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
| ------------ | ---------- | ------- | --------------- | -------------- | ------------ | ----------- | ----------- | ----------- |
| Mukesh Kharb | 2026-04-15 | 1.0     | Mukesh Kharb    | 2026-04-15     | Team         | Mohit Kumar |Faisal Khan  | Mahesh Kumar   |             |

---

## Table of Contents

* [Introduction](#introduction)
* [What is Python Installation](#what-is-python-installation)
* [Why Multiple Installation Methods](#why-multiple-installation-methods)
* [Installation Methods Overview](#installation-methods-overview)
* [Installation via Package Manager](#installation-via-package-manager)
* [Installation via Tarball](#installation-via-tarball)
* [Installation via Bash Script](#installation-via-bash-script)
* [Version Management](#version-management)
* [Best Practices](#best-practices)
* [Troubleshooting](#troubleshooting)
* [Summary](#summary)
* [References](#references)

---

<a id="introduction"></a>

## Introduction

> [!NOTE]
> This document explains different ways to install Python in a flexible and production-friendly manner.

Python can be installed using multiple approaches depending on the use case. In real environments, we often need control over versions, upgrades, and dependencies.

This SOP covers practical methods including package managers, tarball builds, and automated bash scripts.

---

<a id="what-is-python-installation"></a>

## What is Python Installation

Python installation refers to setting up the Python runtime environment on a system so that scripts and applications can be executed.

It may include:

* Installing interpreter
* Managing versions
* Setting environment paths
* Installing pip and dependencies

---

<a id="why-multiple-installation-methods"></a>

## Why Multiple Installation Methods

Different environments require different installation approaches:

* Development → flexible version control
* Production → stable and reproducible builds
* CI/CD → automated setup

Using multiple methods ensures compatibility and control.

---

<a id="installation-methods-overview"></a>

## Installation Methods Overview

| Method          | Use Case                     |
| --------------- | ---------------------------- |
| Package Manager | Quick and easy setup         |
| Tarball         | Custom builds and control    |
| Bash Script     | Automation and repeatability |

---

<a id="installation-via-package-manager"></a>

## Installation via Package Manager

```bash
sudo apt update
sudo apt install python3 python3-pip -y
```
><img width="700" height="auto" alt="image" src="https://github.com/user-attachments/assets/569ab1a6-54f1-4c2b-8be2-774d26a94261" />
><img width="700" height="auto" alt="image" src="https://github.com/user-attachments/assets/284f197a-82ff-491c-9a37-29ea0edb0244" />

---

<a id="installation-via-tarball"></a>

## Installation via Tarball

```bash
wget https://www.python.org/ftp/python/3.12.0/Python-3.12.0.tgz
tar -xvf Python-3.12.0.tgz
cd Python-3.12.0
./configure
make
sudo make install
```
><img width="700" height="auto" alt="image" src="https://github.com/user-attachments/assets/e483c17e-4018-4883-873c-943d59fbb406" />
><img width="700" height="auto" alt="image" src="https://github.com/user-attachments/assets/74b514cd-10c5-4104-93fa-b3a46bcbea56" />


* Provides full control over version
* Useful for custom builds
* Requires manual dependency handling

---

<a id="installation-via-bash-script"></a>

## Installation via Bash Script

> [!IMPORTANT]
> Bash scripts are used to automate Python installation across systems.

### Example Script

><img width="900" height="auto" alt="image" src="https://github.com/user-attachments/assets/2f25c616-5e56-4b68-a495-4698b5a68081" />

><img width="700" height="auto" alt="image" src="https://github.com/user-attachments/assets/9388f109-3726-4f62-b542-d86d9d6d88b2" />

### Script Explanation

* **set -e**
  Stops the script immediately if any command fails, ensuring safe execution.

* **PYTHON_VERSION variable**
  Defines which Python version to install, making the script reusable and easy to update.

* **Install dependencies**
  Installs required build tools and libraries needed to compile Python from source.

* **Download tarball**
  Fetches the specified Python version directly from official source.

* **Extract and navigate**
  Unpacks the archive and moves into the source directory.

* **Configure build**
  Prepares the build environment with optimizations enabled.

* **Compile using make**
  Builds Python using all available CPU cores for faster execution.

* **Install using altinstall**
  Installs Python without overriding system default version.

---

<a id="version-management"></a>

## Version Management

```bash
python3 --version
update-alternatives --config python3
```

* Helps switch between versions
* Useful in development environments

---

<a id="best-practices"></a>

## Best Practices

* Use virtual environments for projects
* Avoid system Python modification
* Prefer scripts for automation
* Keep dependencies isolated

---

<a id="troubleshooting"></a>

## Troubleshooting

| Issue            | Cause                | Solution             |
| ---------------- | -------------------- | -------------------- |
| Python not found | PATH issue           | Update PATH variable |
| pip missing      | Not installed        | Install python3-pip  |
| Build failed     | Missing dependencies | Install build tools  |

---

<a id="summary"></a>

## Summary

* Python can be installed using multiple methods
* Bash scripts provide automation and consistency
* Tarball gives control, package manager gives simplicity
* Choose method based on use case

---

<a id="references"></a>

## References

* [https://www.python.org/downloads/](https://www.python.org/downloads/)
* [https://docs.python.org/3/using/unix.html](https://docs.python.org/3/using/unix.html)
* [https://realpython.com/installing-python/](https://realpython.com/installing-python/)

---
