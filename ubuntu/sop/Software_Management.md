# SOP: Software Management using APT (Ubuntu)

---

## Document Control

| Author       | Created on | Version | Last updated by | Last Edited On | Level           | Reviewer |
| ------------ | ---------- | ------- | --------------- | -------------- | --------------- | -------- |
| Mukesh Kharb | 2026-04-14 | 1.0     | Mukesh Kharb    | 2026-04-14     | Internal Review | Team     |

---

## Table of Contents

* [Introduction](#introduction)
* [Purpose](#purpose)
* [Prerequisites](#prerequisites)
* [Package Management Concepts](#package-management-concepts)
* [Update Packages](#update-packages)
* [Install Software](#install-software)
* [Remove Software](#remove-software)
* [Upgrade System](#upgrade-system)
* [Advanced Package Management](#advanced-package-management)
* [Repository Management](#repository-management)
* [Snap Package Management](#snap-package-management)
* [Troubleshooting](#troubleshooting)
* [Best Practices](#best-practices)
* [Contact Information](#contact-information)
* [References](#references)

---

<a id="introduction"></a>

## Introduction

> [!NOTE]
> Software management in Ubuntu is handled using package management tools such as APT (Advanced Package Tool), dpkg, and snap.

These tools allow administrators to install, update, remove, and manage software efficiently while maintaining dependency integrity.

---

<a id="purpose"></a>

## Purpose

> [!IMPORTANT]
> This SOP provides step-by-step procedures for managing software in Ubuntu environments.

* Install software
* Update package repositories
* Upgrade system packages
* Remove software safely
* Manage dependencies and repositories

---

<a id="prerequisites"></a>

## Prerequisites

> [!WARNING]
> Ensure prerequisites are met before executing package management commands.

* Ubuntu 20.04 / 22.04 / 24.04
* User with sudo privileges
* Internet connectivity

---

<a id="package-management-concepts"></a>

## Package Management Concepts

| Tool    | Description                  |
| ------- | ---------------------------- |
| apt     | High-level package manager   |
| apt-get | Low-level backend tool       |
| dpkg    | Handles .deb packages        |
| snap    | Containerized package system |

---

<a id="update-packages"></a>

## Update Packages

> [!TIP]
> Always refresh package index before installation.

### Refresh Package Index

```
sudo apt update
```
><img width="1377" height="889" alt="image" src="https://github.com/user-attachments/assets/71508a7d-4083-41cb-bcdb-4817f29dec16" />

### Upgrade Installed Packages

```
sudo apt upgrade -y
```

### Full Upgrade (Handles dependencies)

```
sudo apt full-upgrade -y
```
><img width="1441" height="855" alt="image" src="https://github.com/user-attachments/assets/6e5fd144-1d88-4203-bb07-7662df85a650" />

---

<a id="install-software"></a>

## Install Software

> [!TIP]
> Use -y flag for non-interactive installations in automation scripts.

### Install a Package

```
sudo apt install nginx -y
```
><img width="1435" height="786" alt="image" src="https://github.com/user-attachments/assets/57ff783e-c6f1-41d2-b06c-775d705efd20" />

### Install Multiple Packages

```
sudo apt install git curl wget -y
```

### Install Specific Version

```
sudo apt install nginx=1.18.0
```

---

<a id="remove-software"></a>

## Remove Software

### Remove Package

```
sudo apt remove nginx -y
```

### Remove with Configuration

```
sudo apt purge nginx -y
```

### Remove Unused Dependencies

```
sudo apt autoremove -y
```

---

<a id="upgrade-system"></a>

## Upgrade System

### Check Upgradable Packages

```
apt list --upgradable
```
><img width="1219" height="338" alt="image" src="https://github.com/user-attachments/assets/2be4850d-bd9f-4ba5-a3bb-66d9e9dff35d" />

### Distribution Upgrade

```
sudo apt dist-upgrade -y
```

---

<a id="advanced-package-management"></a>

## Advanced Package Management

### Search for Package

```
apt search nginx
```

### Show Package Details

```
apt show nginx
```

### List Installed Packages

```
dpkg -l
```

### Install .deb Package

```
sudo dpkg -i package.deb
```

### Fix Broken Packages

```
sudo apt --fix-broken install
```

---

<a id="repository-management"></a>

## Repository Management

### View Sources

```
cat /etc/apt/sources.list
```

### Add Repository

```
sudo add-apt-repository ppa:deadsnakes/ppa
```

### Update After Adding Repo

```
sudo apt update
```

---

<a id="snap-package-management"></a>

## Snap Package Management

### Install Snap Package

```
sudo snap install docker
```

### List Snap Packages

```
snap list
```

### Remove Snap Package

```
sudo snap remove docker
```

---

<a id="troubleshooting"></a>

## Troubleshooting

> [!WARNING]
> Most APT issues are related to repositories, locks, or broken dependencies.

| Issue                    | Cause                       | Solution                            |
| ------------------------ | --------------------------- | ----------------------------------- |
| Unable to locate package | Repo not updated            | Run `sudo apt update`               |
| Broken dependencies      | Interrupted install         | Run `sudo apt --fix-broken install` |
| Permission denied        | Not using sudo              | Use `sudo`                          |
| Lock file error          | Another apt process running | Wait or kill process                |

---

<a id="best-practices"></a>

## Best Practices

> [!IMPORTANT]
> Follow these practices for stable and secure package management.

* Always run `apt update` before installing packages
* Use `apt upgrade` regularly for security patches
* Avoid mixing apt and dpkg unnecessarily
* Clean unused packages using `autoremove`
* Use official repositories when possible

---

<a id="contact-information"></a>

## Contact Information

| Name         | Email                                                                             |
| ------------ | --------------------------------------------------------------------------------- |
| Mukesh Kharb | [mukesh.Kharb.snaatak@mygurukulam.co](mailto:mukesh.Kharb.snaatak@mygurukulam.co) |

---

<a id="references"></a>

## References

* [https://docs.ubuntu.com/](https://docs.ubuntu.com/)
* [https://manpages.ubuntu.com/](https://manpages.ubuntu.com/)

---

## Notes

This SOP aligns with the project directory structure and Ubuntu SOP standards.
