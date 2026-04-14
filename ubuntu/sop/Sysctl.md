# SOP: Common Stack | Operating System | Ubuntu | Systemctl

---

## Author Table

| **Author** | **Created on** | **Version** | **Last updated by** | **Last Edited On** | **Level**       | **Reviewer** |
| ---------- | -------------- | ----------- | ------------------- | ------------------ | --------------- | ------------ |
| Ankita     | 2026-04-15     | 1.0         | Ankita              | 2026-04-15         | Internal Review | Team         |

---

## Table of Contents

* [Overview](#overview)
* [Purpose](#purpose)
* [Prerequisites](#prerequisites)
* [What is systemctl?](#what-is-systemctl)
* [Step-by-Step Implementation](#step-by-step-implementation)

  * [Step 1: Check Service Status](#step-1-check-service-status)
  * [Step 2: Start and Stop Services](#step-2-start-and-stop-services)
  * [Step 3: Enable and Disable Services](#step-3-enable-and-disable-services)
  * [Step 4: Restart and Reload Services](#step-4-restart-and-reload-services)
* [Common Commands](#common-commands)
* [Troubleshooting](#troubleshooting)
* [Best Practices](#best-practices)
* [Contact Information](#contact-information)
* [References](#references)

---

## Overview

This SOP explains how to use **systemctl** in Ubuntu in a simple and beginner-friendly way.

`systemctl` is used to manage **services (background processes)** in Linux.

Examples of services:

* nginx (web server)
* mysql (database)
* ssh (remote access)

---

## Purpose

By following this SOP, you will learn:

* How to check service status
* How to start/stop services
* How to enable services on boot
* How to troubleshoot services

---

## Prerequisites

* Ubuntu 20.04 / 22.04 / 24.04
* Sudo privileges
* Basic Linux command knowledge

---

## What is systemctl?

`systemctl` is a command used to interact with **systemd**, which manages services in Linux.

👉 In simple terms:

* It controls background services
* Helps start, stop, restart applications
* Manages services during system boot

---

## Step-by-Step Implementation

### Step 1: Check Service Status

```bash
systemctl status nginx
```

📸 Screenshot

<img width="1106" height="783" alt="image" src="https://github.com/user-attachments/assets/2e48382d-6c84-40d8-9f9f-29678de90b88" />

---

### Step 2: Start and Stop Services

Start a service:

```bash
sudo systemctl start nginx
```

Stop a service:

```bash
sudo systemctl stop nginx
```

📸 Screenshot

<img width="1106" height="673" alt="image" src="https://github.com/user-attachments/assets/2715a30e-4cfb-43a5-827c-7d2f26bbf59e" />

---

### Step 3: Enable and Disable Services

Enable service at boot:

```bash
sudo systemctl enable nginx
```

Disable service:

```bash
sudo systemctl disable nginx
```

📸 Screenshot

<img width="1106" height="673" alt="image" src="https://github.com/user-attachments/assets/ef6daa05-93a1-4fb4-8950-061b10743a2f" />

---

### Step 4: Restart and Reload Services

Restart service:

```bash
sudo systemctl restart nginx
```

Reload configuration:

```bash
sudo systemctl reload nginx
```

📸 Screenshot

<img width="1106" height="673" alt="image" src="https://github.com/user-attachments/assets/dd58e8e5-4143-49ef-b6f5-84fb150bc1b2" />
<img width="1106" height="673" alt="image" src="https://github.com/user-attachments/assets/4d2c5ba7-a8cf-41cd-b841-83f9f741cd05" />

---

## Common Commands

| Command                     | Description     |
| --------------------------- | --------------- |
| systemctl status <service>  | Check status    |
| systemctl start <service>   | Start service   |
| systemctl stop <service>    | Stop service    |
| systemctl restart <service> | Restart service |
| systemctl enable <service>  | Enable at boot  |
| systemctl disable <service> | Disable at boot |

---

## Troubleshooting

| Issue                | Cause            | Solution                    |
| -------------------- | ---------------- | --------------------------- |
| Service not starting | Config issue     | Check logs using journalctl |
| Permission denied    | Not using sudo   | Use sudo                    |
| Service failed       | Dependency issue | Check service status output |

---

## Best Practices

* Always check status before troubleshooting
* Use restart only when needed
* Enable only required services
* Monitor logs using journalctl

---

## Contact Information

| Name   | Email                                                                             |
| ------ | --------------------------------------------------------------------------------- |
| Ankita | [ankita.singh.snaatak@mygurukulam.co](mailto:ankita.singh.snaatak@mygurukulam.co) |

---

## References

* Ubuntu systemctl Documentation
* systemd Official Docs

---

## Notes

This SOP is designed for beginners and follows standard internal documentation format.
