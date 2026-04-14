# SOP: Ubuntu Concepts (Operating System)

---

| **Author** | **Created on** | **Version** | **Last updated by** | **Last Edited On** | **Level**       | **Reviewer** |
| ---------- | -------------- | ----------- | ------------------- | ------------------ | --------------- | ------------ |
| Ankita     | 2026-04-14     | 1.0         | Ankita              | 2026-04-14         | Internal Review | Team         |

---

## Table of Contents

* [Introduction](#introduction)
* [Purpose](#purpose)
* [Why Ubuntu in DevOps](#why-ubuntu-in-devops)
* [Core Concepts of Ubuntu](#core-concepts-of-ubuntu)
* [Software Management](#software-management)
* [Services & Process Management](#services--process-management)
* [File System Structure](#file-system-structure)
* [User & Permission Management](#user--permission-management)
* [Networking Basics](#networking-basics)
* [Logs & Monitoring](#logs--monitoring)
* [Troubleshooting](#troubleshooting)
* [Best Practices](#best-practices)
* [Contact Information](#contact-information)
* [References](#references)

---

## Introduction

Ubuntu is a Debian-based Linux operating system widely used in **DevOps, cloud environments, and microservices architecture** due to its stability, security, and strong package ecosystem.

---

## Purpose

This SOP provides conceptual understanding of Ubuntu covering:

* Core operating system components
* Software and service management
* File system and permissions
* Networking and logging

---

## Why Ubuntu in DevOps

Ubuntu is preferred because:

* Open-source and free
* Strong community support
* Stable LTS releases
* Seamless integration with cloud platforms (AWS, Azure, GCP)
* Rich package repositories (APT)

---

## Core Concepts of Ubuntu

### 1. Kernel

* Core of OS
* Manages hardware and system resources

### 2. Shell

* Interface to interact with OS
* Common shells: bash, zsh

### 3. Processes

* Running programs
* Each process has PID

### 4. Packages

* Software distributed via .deb files

---

## Software Management

Ubuntu uses **APT (Advanced Package Tool)**:

```bash
sudo apt update
sudo apt install nginx
sudo apt remove nginx
```

Key Concepts:

* Repository-based installation
* Dependency resolution
* Package version control

---

## Services & Process Management

Managed using **systemd**:

```bash
systemctl start nginx
systemctl stop nginx
systemctl status nginx
```

Concepts:

* Services run in background
* Units define service behavior

---

## File System Structure

| Directory | Purpose                |
| --------- | ---------------------- |
| /         | Root directory         |
| /etc      | Configuration files    |
| /var      | Logs and variable data |
| /home     | User directories       |
| /usr      | Installed applications |

---

## User & Permission Management

### Users

```bash
useradd user1
passwd user1
```

### Permissions

```bash
chmod 755 file
chown user:group file
```

Concepts:

* Read (r), Write (w), Execute (x)
* Ownership (user/group)

---

## Networking Basics

Check IP:

```bash
ip a
```

Check connectivity:

```bash
ping google.com
```

Ports:

```bash
ss -tulnp
```

---

## Logs & Monitoring

### System Logs

```bash
journalctl
```

### Application Logs

* Located in `/var/log/`

---

## Troubleshooting

| Issue                 | Cause               | Solution                 |
| --------------------- | ------------------- | ------------------------ |
| Service not running   | Misconfiguration    | Check `systemctl status` |
| Package install fails | Repo issue          | Run `apt update`         |
| Permission denied     | Insufficient rights | Use sudo                 |

---

## Best Practices

* Keep system updated
* Use least privilege principle
* Monitor logs regularly
* Use LTS versions
* Automate using scripts

---

## Contact Information

| Name   | Email                                                                             |
| ------ | --------------------------------------------------------------------------------- |
| Ankita | [ankita.singh.snaatak@mygurukulam.co](mailto:ankita.singh.snaatak@mygurukulam.co) |

---

## References

* Ubuntu Official Documentation
* Linux Man Pages

---

## Notes

This document aligns with instructor criteria: **Why, What, Software Management, Services** for Ubuntu concepts.
