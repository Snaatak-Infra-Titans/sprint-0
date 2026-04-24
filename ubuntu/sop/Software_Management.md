# SOP: Software Management using APT (Ubuntu)

---

| **Author**   | **Created on** | **Version** | **Last updated by** | **Last Edited On** | **Level**       | **Reviewer** |
| ------------ | -------------- | ----------- | ------------------- | ------------------ | --------------- | ------------ |
| Mukesh Kharb | 2026-04-14     | 1.0         | Mukesh Kharb        | 2026-04-14         | Internal Review | Team         |

---

## Table of Contents

* Introduction
* Purpose
* Prerequisites
* Package Management Concepts
* Update Packages
* Install Software
* Remove Software
* Upgrade System
* Advanced Package Management
* Troubleshooting
* Best Practices
* Contact Information
* References

---

## Introduction

Software management in Ubuntu is handled using package management tools such as **APT (Advanced Package Tool)**, **dpkg**, and **snap**. These tools allow administrators to install, update, remove, and manage software efficiently while maintaining dependency integrity.

---

## Purpose

This SOP provides step-by-step procedures to:

* Install software
* Update package repositories
* Upgrade system packages
* Remove software safely
* Manage dependencies and repositories

---

## Prerequisites

* Ubuntu 20.04 / 22.04 / 24.04
* User with **sudo privileges**
* Internet connectivity

---

## Package Management Concepts

| Tool    | Description                              |
| ------- | ---------------------------------------- |
| apt     | High-level package manager |
| apt-get | Low-level backend tool                   |
| dpkg    | Handles .deb packages                    |
| snap    | Containerized package system             |

---

## Update Packages

### Refresh Package Index

```bash
sudo apt update
```

### Upgrade Installed Packages

```bash
sudo apt upgrade -y
```

### Full Upgrade (Handles dependencies)

```bash
sudo apt full-upgrade -y
```

---

## Install Software

### Install a Package

```bash
sudo apt install nginx -y
```

### Install Multiple Packages

```bash
sudo apt install git curl wget -y
```

### Install Specific Version

```bash
sudo apt install nginx=1.18.0
```

---

## Remove Software

### Remove Package

```bash
sudo apt remove nginx -y
```

### Remove with Configuration

```bash
sudo apt purge nginx -y
```

### Remove Unused Dependencies

```bash
sudo apt autoremove -y
```

---

## Upgrade System

### Check Upgradable Packages

```bash
apt list --upgradable
```

### Distribution Upgrade

```bash
sudo apt dist-upgrade -y
```

---

## Advanced Package Management

### Search for Package

```bash
apt search nginx
```

### Show Package Details

```bash
apt show nginx
```

### List Installed Packages

```bash
dpkg -l
```

### Install .deb Package

```bash
sudo dpkg -i package.deb
```

### Fix Broken Packages

```bash
sudo apt --fix-broken install
```

---

## Repository Management

### View Sources

```bash
cat /etc/apt/sources.list
```

### Add Repository

```bash
sudo add-apt-repository ppa:deadsnakes/ppa
```

### Update After Adding Repo

```bash
sudo apt update
```

---

## Snap Package Management

### Install Snap Package

```bash
sudo snap install docker
```

### List Snap Packages

```bash
snap list
```

### Remove Snap Package

```bash
sudo snap remove docker
```

---

## Troubleshooting

| Issue                    | Cause                       | Solution                            |
| ------------------------ | --------------------------- | ----------------------------------- |
| Unable to locate package | Repo not updated            | Run `sudo apt update`               |
| Broken dependencies      | Interrupted install         | Run `sudo apt --fix-broken install` |
| Permission denied        | Not using sudo              | Use `sudo`                          |
| Lock file error          | Another apt process running | Wait or kill process                |

---

## Best Practices

* Always run `apt update` before installing packages
* Use `apt upgrade` regularly for security patches
* Avoid mixing apt and dpkg unnecessarily
* Clean unused packages using `autoremove`
* Use official repositories when possible

---

## Contact Information

| Name         | Email                                           |
| ------------ | ----------------------------------------------- |
| Mukesh Kharb | [mukesh.Kharb.snaatak@mygurukulam.co](mailto:mukesh.Kharb.snaatak@mygurukulam.co) |

---

## References

* Ubuntu APT Documentation
* Debian Package Management Guide

---

## Notes

This SOP aligns with the project directory structure and Ubuntu SOP standards.
