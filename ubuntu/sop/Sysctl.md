# SOP: Common Stack | Operating System | Ubuntu | sysctl

---

## Author Table

| **Author** | **Created on** | **Version** | **Last updated by** | **Last Edited On** | **Level**       | **Reviewer** |
| ---------- | -------------- | ----------- | ------------------- | ------------------ | --------------- | ------------ |
| Ankita     | 2026-04-15     | 1.3         | Ankita              | 2026-04-15         | Internal Review | Team         |

---

## Table of Contents

* [Overview](#overview)
* [Purpose](#purpose)
* [Prerequisites](#prerequisites)
* [What is sysctl?](#what-is-sysctl)
* [Where are these settings stored?](#where-are-these-settings-stored)
* [Step-by-Step Implementation](#step-by-step-implementation)

  * [Step 1: See Current Settings](#step-1-see-current-settings)
  * [Step 2: Change a Setting](#step-2-change-a-setting)
  * [Step 3: Make Change Permanent](#step-3-make-change-permanent)
  * [Step 4: Apply & Verify](#step-4-apply--verify)
* [Easy Examples](#easy-examples)
* [Common Mistakes](#common-mistakes)
* [Troubleshooting](#troubleshooting)
* [Best Practices](#best-practices)
* [Contact Information](#contact-information)
* [References](#references)

---

## Overview

This SOP explains **sysctl** in the simplest way possible.

Think of `sysctl` like **settings in your phone** — it changes how your system behaves internally.

You can control:

* Networking behavior
* Memory usage
* Security rules

---

## Purpose

After this guide, you will be able to:

* Understand what sysctl does
* Change system settings safely
* Make changes permanent
* Verify if changes worked

---

## Prerequisites

* Ubuntu (20.04 / 22.04 / 24.04)
* Sudo access
* Basic terminal usage

---

## What is sysctl?

* **Kernel** = Brain of the OS
* **sysctl** = Settings panel for the brain

It lets you change system behavior **without rebooting**.

---

## Where are these settings stored?

Runtime (live values):

```bash
/proc/sys/
```

Permanent config files:

```bash
/etc/sysctl.conf
/etc/sysctl.d/*.conf
```

---

## Step-by-Step Implementation

### Step 1: See Current Settings

Show all settings:

```bash
sysctl -a
```

Check one setting:

```bash
sysctl net.ipv4.ip_forward
```

---

### Step 2: Change a Setting

Works instantly, but resets after reboot

```bash
sudo sysctl -w net.ipv4.ip_forward=1
```

---

### Step 3: Make Change Permanent

Open config file:

```bash
sudo vi /etc/sysctl.conf
```

Add:

```bash
net.ipv4.ip_forward=1
```

---

### Step 4: Apply & Verify

Apply changes:

```bash
sudo sysctl --system
```

Verify:

```bash
sysctl net.ipv4.ip_forward
```

---

## Easy Examples

### Enable IP Forwarding (for networking)

```bash
net.ipv4.ip_forward=1
```

### Reduce Memory Swapping (performance)

```bash
vm.swappiness=10
```

### Enable Security Feature

```bash
net.ipv4.tcp_syncookies=1
```

---

## Common Mistakes

* Forgetting sudo
* Not applying changes
* Editing wrong parameter
* Not saving file properly

---

## Troubleshooting

| Problem            | Reason      | Fix                   |
| ------------------ | ----------- | --------------------- |
| Change not working | Not applied | Run `sysctl --system` |
| Permission denied  | No sudo     | Use sudo              |
| Value resets       | Not saved   | Add to config file    |

---

## Best Practices

* Take backup before changes
* Use `/etc/sysctl.d/` for better organization
* Test changes first
* Avoid random tuning from internet

---

## Contact Information

| Name   | Email                                                                             |
| ------ | --------------------------------------------------------------------------------- |
| Ankita | [ankita.singh.snaatak@mygurukulam.co](mailto:ankita.singh.snaatak@mygurukulam.co) |

---

## References

* Ubuntu sysctl Documentation
* Linux Kernel Docs

---

## Notes

This version is **super beginner-friendly** with simple explanations and real examples.
