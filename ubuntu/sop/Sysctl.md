# SOP: Common Stack | Operating System | Ubuntu | Sysctl

---

## Author Table

| **Author** | **Created on** | **Version** | **Last updated by** | **Last Edited On** | **Pre Reviewer** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ---------- | -------------- | ----------- | ------------------- | ------------------ | ---------------- | --------------- | --------------- | --------------- |
| Ankita     | 15-04-2026     | v1.0        | Ankita              | 17-04-2026         | Team             |                 |                 |                 |

---

## Table of Contents

1. [Overview](#overview)
2. [Purpose](#purpose)
3. [Prerequisites](#prerequisites)
4. [What is Sysctl?](#what-is-sysctl)
5. [Step-by-Step Implementation](#step-by-step-implementation)
6. [Common Use Cases](#common-use-cases)
7. [Troubleshooting](#troubleshooting)
8. [Best Practices](#best-practices)
9. [Contact Information](#contact-information)
10. [References](#references)

---

## Overview

This document provides a beginner-friendly Standard Operating Procedure (SOP) for using the `sysctl` command in Ubuntu.

The `sysctl` command is used to view and modify Linux kernel parameters such as networking, memory management, and security settings.

It is widely used in DevOps and system administration for performance tuning and system configuration.

---

## Purpose

The purpose of this SOP is to:

* Explain what `sysctl` is
* Help users view kernel parameters
* Guide users to modify parameters safely
* Show how to make changes temporary or permanent
* Apply changes without reboot

---

## Prerequisites

* Ubuntu 20.04 / 22.04 / 24.04
* Basic Linux command knowledge
* sudo or root access

(Optional but recommended)

```bash
sudo cp /etc/sysctl.conf /etc/sysctl.conf.backup
```

---

## What is Sysctl?

`sysctl` is a Linux utility used to interact with kernel parameters at runtime.

These parameters are stored in:

```bash
/proc/sys/
```

Example:

```bash
cat /proc/sys/net/ipv4/ip_forward
```

It allows administrators to control system behavior without modifying kernel code.

---

## Step-by-Step Implementation

### Step 1: View All Kernel Parameters

```bash
sysctl -a
```

---

### Step 2: Check Specific Parameter

```bash
sysctl net.ipv4.ip_forward
```

Example output:

```
net.ipv4.ip_forward = 0
```

---

### Step 3: Temporary Changes (Runtime Only)

Apply changes immediately (not persistent after reboot):

```bash
sudo sysctl -w net.ipv4.ip_forward=1
```

Example:

```bash
sudo sysctl -w vm.swappiness=10
```

---

### Step 4: Permanent Changes

#### Option 1: Edit global configuration

```bash
sudo nano /etc/sysctl.conf
```

Add:

```bash
net.ipv4.ip_forward = 1
vm.swappiness = 10
```

---

#### Option 2: Use sysctl.d directory (Recommended)

```bash
sudo nano /etc/sysctl.d/99-custom.conf
```

Add:

```bash
net.ipv4.ip_forward = 1
vm.swappiness = 10
```

---

### Step 5: Apply Changes

```bash
sudo sysctl --system
```

Verify:

```bash
sysctl net.ipv4.ip_forward
```

---

## Common Use Cases

| Use Case               | Command                       |
| ---------------------- | ----------------------------- |
| Enable IP forwarding   | net.ipv4.ip_forward=1         |
| Improve memory usage   | vm.swappiness=10              |
| Enable SYN cookies     | net.ipv4.tcp_syncookies=1     |
| Reverse path filtering | net.ipv4.conf.all.rp_filter=1 |

---

## Troubleshooting

| Issue                  | Cause               | Solution            |
| ---------------------- | ------------------- | ------------------- |
| Permission denied      | Not using sudo      | Use sudo            |
| Changes not persistent | Not saved in config | Add to sysctl.conf  |
| Parameter not found    | Wrong parameter     | Use sysctl -a       |
| Changes not applied    | Not reloaded        | Run sysctl --system |

---

## Best Practices

* Take backup before making changes
* Use `/etc/sysctl.d/` for modular configuration
* Test changes before applying in production
* Avoid unnecessary kernel tuning
* Document all changes

---

## Contact Information

| Name   | Email                                                                             |
| ------ | --------------------------------------------------------------------------------- |
| Ankita | [ankita.singh.snaatak@mygurukulam.co](mailto:ankita.singh.snaatak@mygurukulam.co) |

---

## References

| Topic                      | Link                                                                                                                                 |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| Ubuntu Sysctl Man Page     | [https://manpages.ubuntu.com/manpages/jammy/en/man8/sysctl.8.html](https://manpages.ubuntu.com/manpages/jammy/en/man8/sysctl.8.html) |
| Linux Kernel Documentation | [https://www.kernel.org/doc/](https://www.kernel.org/doc/)                                                                           |
