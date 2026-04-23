
# Common Stack | Operating System | Ubuntu | Concepts

<p align="center">
  <img src="https://upload.wikimedia.org/wikipedia/commons/e/e0/Ubuntu_logo_orange.png" alt="Ubuntu" width="250"/>
</p>

---

## Author Table

| Author  | Created on | Version | Last updated by | Last Edited On | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|--------|------------|---------|----------------|---------------|-------------|------------|------------|------------|
| Ankita | 15-04-2026 | v1.1    | Ankita         | 23-04-2026    | Team        | Komal Jaiswal | Akshit Kapil | Mahesh Kumar |

---

## Table of Contents

1. [Introduction](#introduction)  
2. [Purpose](#purpose)  
3. [Why Ubuntu in DevOps](#why-ubuntu-in-devops)  
4. [Core Concepts of Ubuntu](#core-concepts-of-ubuntu)  
5. [Common Commands](#common-commands)  
6. [Software Management](#software-management)  
7. [Services & Process Management](#services--process-management)  
8. [Disk & Ulimit](#disk--ulimit)  
9. [Cron](#cron)  
10. [Logrotate](#logrotate)  
11. [Sysctl](#sysctl)  
12. [File System Structure](#file-system-structure)  
13. [User & Permission Management](#user--permission-management)  
14. [Networking Basics](#networking-basics)  
15. [Logs & Monitoring](#logs--monitoring)  
16. [Troubleshooting](#troubleshooting)  
17. [Best Practices](#best-practices)  
18. [Contact Information](#contact-information)  
19. [References](#references)

---

## Introduction

Ubuntu is a Debian-based Linux operating system widely used in DevOps, cloud computing, and microservices environments.

---

## Purpose

This document provides a conceptual understanding of Ubuntu and its operational components used in real-world DevOps environments.

---

## Why Ubuntu in DevOps

- Open-source and free  
- Stable LTS releases  
- Strong community support  
- Cloud-ready (AWS, Azure, GCP)  
- APT-based package management  

---

## Core Concepts of Ubuntu

### Kernel
- Core of OS managing hardware  

### Shell
- Interface (bash, zsh)  

### Processes
- Running programs with PID  

### Packages
- Installable software units  

---

## Common Commands

Basic Linux commands used to navigate, manage files, and perform everyday system operations.

```bash
ls
cd
pwd
cp
mv
rm
````

**Reference:** [Common Commands SOP](https://github.com/Snaatak-Infra-Titans/sprint-0/blob/SCRUM-7-deepak/ubuntu/sop/Common_commands.md)

---

## Software Management

Handles installation, update, and removal of packages using the APT package manager.

```bash
sudo apt update
sudo apt install nginx
sudo apt remove nginx
```

**Reference:** [Software Management SOP](https://github.com/Snaatak-Infra-Titans/sprint-0/blob/SCRUM-9-mukesh/ubuntu/sop/Software_Management.md)

---

## Services & Process Management

Used to control and monitor background services and system processes using tools like systemctl.

```bash
systemctl start nginx
systemctl stop nginx
systemctl status nginx
```

**Reference:** [Services SOP](https://github.com/Snaatak-Infra-Titans/sprint-0/blob/SCRUM-8-gourav/ubuntu/sop/Service.md)

---

## Disk & Ulimit

Manages disk usage and system resource limits such as file descriptors and process counts.

```bash
df -h
du -sh *
ulimit -n
ulimit -u
```

**Reference:** [Disk & Ulimit SOP](https://github.com/Snaatak-Infra-Titans/sprint-0/blob/SCRUM-10-saransh/ubuntu/sop/Disk_and_Ulimit.md)

---

## Cron

Schedules and automates repetitive tasks to run at specific times or intervals.

```bash
crontab -e
```

Example:

```bash
* * * * * /path/script.sh
```

**Reference:** [Cron SOP](https://github.com/Snaatak-Infra-Titans/sprint-0/blob/SCRUM-11-shivam/ubuntu/sop/Cron.md)

---

## Logrotate

Manages log files by rotating, compressing, and removing old logs to save disk space.

```bash
logrotate /etc/logrotate.conf
```

**Reference:** [Logrotate SOP](https://github.com/Snaatak-Infra-Titans/sprint-0/blob/SCRUM-12-versha/ubuntu/sop/Log_Rotate.md)

---

## Sysctl

Configures and modifies Linux kernel parameters at runtime for performance and security tuning.

```bash
sysctl -a
sysctl -w net.ipv4.ip_forward=1
```

**Reference:** [Sysctl SOP](https://github.com/Snaatak-Infra-Titans/sprint-0/blob/SCRUM-13-ankita/ubuntu/sop/Sysctl.md)

---

## File System Structure

| Directory | Purpose |
| --------- | ------- |
| /         | Root    |
| /etc      | Config  |
| /var      | Logs    |
| /home     | Users   |
| /usr      | Apps    |

---

## User & Permission Management

```bash
useradd user1
passwd user1
chmod 755 file
chown user:group file
```

---

## Networking Basics

```bash
ip a
ping google.com
ss -tulnp
```

---

## Logs & Monitoring

```bash
journalctl
```

Path:

```
/var/log/
```

---

## Troubleshooting

| Issue               | Solution         |
| ------------------- | ---------------- |
| Service not running | systemctl status |
| Install fails       | apt update       |
| Permission denied   | sudo             |

---

## Best Practices

* Keep system updated
* Use least privilege
* Monitor logs
* Use LTS versions
* Automate tasks

---

## Contact Information

| Name   | Email                                                                             |
| ------ | --------------------------------------------------------------------------------- |
| Ankita | [ankita.singh.snaatak@mygurukulam.co](mailto:ankita.singh.snaatak@mygurukulam.co) |

---

## References

* [Ubuntu Documentation](https://ubuntu.com/tutorials)
* [Linux Man Pages](https://man7.org)
