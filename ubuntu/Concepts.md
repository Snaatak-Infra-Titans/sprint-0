# Common Stack | Operating System | Ubuntu | Concepts

---

## Author Table

| **Author** | **Created on** | **Version** | **Last updated by** | **Last Edited On** | **Pre Reviewer** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ---------- | -------------- | ----------- | ------------------- | ------------------ | ---------------- | --------------- | --------------- | --------------- |
| Ankita     | 15-04-2026     | v1.0        | Ankita              | 15-04-2026         | Team             |                 |                 |                 |

---

## Table of Contents

1. [Introduction](#introduction)

2. [Purpose](#purpose)

3. [Why Ubuntu in DevOps](#why-ubuntu-in-devops)

4. [Core Concepts of Ubuntu](#core-concepts-of-ubuntu)

5. [Software Management](#software-management)

6. [Services & Process Management](#services--process-management)

7. [File System Structure](#file-system-structure)

8. [User & Permission Management](#user--permission-management)

9. [Networking Basics](#networking-basics)

10. [Logs & Monitoring](#logs--monitoring)

11. [Troubleshooting](#troubleshooting)

12. [Best Practices](#best-practices)

13. [FAQs](#faqs)

14. [Contact Information](#contact-information)

15. [References](#references)

16. [Introduction](#introduction)

17. [Why Ubuntu in DevOps](#why-ubuntu-in-devops)

18. [Core Concepts of Ubuntu](#core-concepts-of-ubuntu)

19. [Software Management](#software-management)

20. [Services & Process Management](#services--process-management)

21. [File System Structure](#file-system-structure)

22. [User & Permission Management](#user--permission-management)

23. [Networking Basics](#networking-basics)

24. [Logs & Monitoring](#logs--monitoring)

25. [Troubleshooting](#troubleshooting)

26. [Best Practices](#best-practices)

27. [FAQs](#faqs)

28. [Contact Information](#contact-information)

29. [References](#references)

---

## Introduction

Ubuntu is a Debian-based Linux operating system widely used in DevOps, cloud computing, and microservices environments.

It is known for its stability, security, and strong package management system.

Ubuntu is commonly used in servers, cloud platforms, and development environments due to its ease of use and large community support.

---

## Purpose

This document provides a conceptual understanding of Ubuntu, covering key operating system components, system management, networking, and best practices.

It is designed to help beginners understand how Ubuntu works in real-world DevOps and cloud environments.

---

Ubuntu is a Debian-based Linux operating system widely used in DevOps, cloud computing, and microservices environments.

It is known for its stability, security, and strong package management system.

Ubuntu is commonly used in servers, cloud platforms, and development environments due to its ease of use and large community support.

---

## Why Ubuntu in DevOps

Ubuntu is preferred in DevOps workflows because:

* Open-source and free to use
* Stable Long-Term Support (LTS) releases
* Strong community and documentation support
* Seamless integration with cloud platforms (AWS, Azure, GCP)
* Rich package ecosystem using APT

---

## Core Concepts of Ubuntu

### 1. Kernel

* The core of the operating system
* Manages hardware resources such as CPU, memory, and devices

### 2. Shell

* Interface to interact with the operating system
* Common shells include bash and zsh

### 3. Processes

* Programs running on the system
* Each process has a unique Process ID (PID)

### 4. Packages

* Software distributed as installable files
* Managed using package managers like APT

---

## Software Management

Ubuntu uses APT (Advanced Package Tool) for managing software.

Update package list:

```bash
sudo apt update
```

Install a package:

```bash
sudo apt install nginx
```

Remove a package:

```bash
sudo apt remove nginx
```

Key Concepts:

* Repository-based installation
* Automatic dependency resolution
* Version management

---

## Services & Process Management

Ubuntu uses systemd to manage services.

Start a service:

```bash
systemctl start nginx
```

Stop a service:

```bash
systemctl stop nginx
```

Check status:

```bash
systemctl status nginx
```

Key Concepts:

* Services run in the background
* Managed using units in systemd

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

Create user:

```bash
sudo useradd user1
```

Set password:

```bash
sudo passwd user1
```

---

### Permissions

Change permissions:

```bash
chmod 755 file
```

Change ownership:

```bash
chown user:group file
```

Key Concepts:

* Read (r), Write (w), Execute (x)
* Ownership (user and group)

---

## Networking Basics

Check IP address:

```bash
ip a
```

Check connectivity:

```bash
ping google.com
```

Check open ports:

```bash
ss -tulnp
```

---

## Logs & Monitoring

View system logs:

```bash
journalctl
```

Application logs are usually stored in:

```
/var/log/
```

---

## Troubleshooting

| Issue                 | Cause               | Solution               |
| --------------------- | ------------------- | ---------------------- |
| Service not running   | Misconfiguration    | Check systemctl status |
| Package install fails | Repository issue    | Run apt update         |
| Permission denied     | Insufficient rights | Use sudo               |

---

## Best Practices

* Keep system updated regularly
* Use least privilege principle
* Monitor logs frequently
* Use LTS versions for stability
* Automate repetitive tasks using scripts

---

## FAQs

**Q1: What is Ubuntu?**
Ubuntu is a Linux-based operating system used for servers and development.

**Q2: What is APT?**
APT is a package manager used to install and manage software.

**Q3: What is systemd?**
systemd is a service manager used to control system services.

**Q4: Where are logs stored?**
Logs are stored in `/var/log/`.

---

## Contact Information

| Name   | Email                                                                             |
| ------ | --------------------------------------------------------------------------------- |
| Ankita | [ankita.singh.snaatak@mygurukulam.co](mailto:ankita.singh.snaatak@mygurukulam.co) |

---

## References

| Topic                | Link                                                                   |
| -------------------- | ---------------------------------------------------------------------- |
| Ubuntu Documentation | [https://ubuntu.com/tutorials](https://ubuntu.com/tutorials)           |
| Linux Man Pages      | [https://man7.org/linux/man-pages/](https://man7.org/linux/man-pages/) |
