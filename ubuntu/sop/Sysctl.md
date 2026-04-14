# SOP: Common Stack | Operating System | Ubuntu | Sysctl

---

## Author Table

| **Author** | **Created on** | **Version** | **Last updated by** | **Last Edited On** | **Level**       | **Reviewer** |
| ---------- | -------------- | ----------- | ------------------- | ------------------ | --------------- | ------------ |
| Ankita     | 2026-04-14     | 1.0         | Ankita              | 2026-04-14         | Internal Review | Team         |

---

## Table of Contents

* [Overview](#overview)
* [Purpose](#purpose)
* [Prerequisites](#prerequisites)
* [What is Sysctl?](#what-is-sysctl)
* [Step-by-Step Implementation](#step-by-step-implementation)

  * [Step 1: View Kernel Parameters](#step-1-view-kernel-parameters)
  * [Step 2: Modify Parameters Temporarily](#step-2-modify-parameters-temporarily)
  * [Step 3: Make Changes Permanent](#step-3-make-changes-permanent)
  * [Step 4: Apply Changes](#step-4-apply-changes)
* [Common Use Cases](#common-use-cases)
* [Troubleshooting](#troubleshooting)
* [Best Practices](#best-practices)
* [Contact Information](#contact-information)
* [References](#references)

---

## Overview

This SOP explains **how to manage Linux kernel parameters using `sysctl` in Ubuntu** in a simple and beginner-friendly way.

Think of `sysctl` as a tool that helps you **control how your system behaves internally**, like:

* How networking works 🌐
* How memory is used 💾
* Security settings 🔐

---

## Purpose

By following this SOP, you will learn:

* How to view system settings
* How to change them safely
* How to make changes permanent
* How to verify your changes

---

## Prerequisites

Before starting, make sure:

* You are using Ubuntu (20.04 / 22.04 / 24.04)
* You have **sudo access**
* You can run basic Linux commands

---

## What is Sysctl?

In Linux, many system settings are controlled by the **kernel (core of OS)**.

These settings are stored in:

```bash
/proc/sys/
```

Instead of editing files manually, we use:

```bash
sysctl
```

👉 It allows you to:

* View settings
* Change settings
* Apply changes instantly

Configuration files:

```bash
/etc/sysctl.conf
/etc/sysctl.d/*.conf
```

---

## Step-by-Step Implementation

### Step 1: View Kernel Parameters

👉 First, let’s see current system settings

View all parameters:

```bash
sysctl -a
```

📸 Screenshot Placeholder:

```
(Add screenshot of sysctl -a output here)
```

View a specific parameter:

```bash
sysctl net.ipv4.ip_forward
```

📸 Screenshot Placeholder:

```
(Add screenshot showing parameter value)
```

Directly from system file:

```bash
cat /proc/sys/net/ipv4/ip_forward
```

---

### Step 2: Modify Parameters Temporarily

👉 These changes work immediately but reset after reboot

```bash
sudo sysctl -w <parameter>=<value>
```

Example:

```bash
sudo sysctl -w net.ipv4.ip_forward=1
```

📸 Screenshot Placeholder:

```
(Add screenshot showing successful change)
```

Another example:

```bash
sudo sysctl -w vm.swappiness=10
```

---

### Step 3: Make Changes Permanent

👉 To keep changes after reboot, we save them in config files

#### Option 1: Global config file

```bash
sudo vi /etc/sysctl.conf
```

Add:

```bash
net.ipv4.ip_forward=1
vm.swappiness=10
```

📸 Screenshot Placeholder:

```
(Add screenshot of sysctl.conf file)
```

---

#### Option 2: Recommended method (modular config)

```bash
sudo vi /etc/sysctl.d/99-custom.conf
```

Add:

```bash
net.ipv4.tcp_syncookies=1
net.ipv4.conf.all.rp_filter=1
```

📸 Screenshot Placeholder:

```
(Add screenshot of custom config file)
```

---

### Step 4: Apply Changes

👉 Apply changes without restarting system

```bash
sudo sysctl --system
```

📸 Screenshot Placeholder:

```
(Add screenshot of apply output)
```

Verify changes:

```bash
sysctl -a | grep ip_forward
```

---

## Common Use Cases

### Networking

Enable IP forwarding:

```bash
net.ipv4.ip_forward=1
```

### Security Hardening

```bash
net.ipv4.conf.all.rp_filter=1
net.ipv4.tcp_syncookies=1
```

### Performance Tuning

```bash
vm.swappiness=10
fs.file-max=100000
```

---

## Troubleshooting

| **Issue**                 | **Cause**           | **Solution**            |
| ------------------------- | ------------------- | ----------------------- |
| Permission denied         | Not using sudo      | Use `sudo`              |
| Changes not applied       | Config not reloaded | Run `sysctl --system`   |
| Parameter not found       | Wrong name          | Check using `sysctl -a` |
| Changes lost after reboot | Not saved           | Add in config file      |

---

## Best Practices

* Always take backup before changes
* Use `/etc/sysctl.d/` instead of editing main file
* Test changes before production use
* Keep documentation of changes
* Avoid unnecessary tuning

---

## Contact Information

| **Name** | **Email Address**                                                                 |
| -------- | --------------------------------------------------------------------------------- |
| Ankita   | [ankita.singh.snaatak@mygurukulam.co](mailto:ankita.singh.snaatak@mygurukulam.co) |

---

## References

* Ubuntu Sysctl Man Page
* Linux Kernel Documentation
* Internal SOP Template
