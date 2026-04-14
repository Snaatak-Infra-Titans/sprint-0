# SOP: Common Stack | Operating System | Ubuntu | Disk Usage & Ulimit Management

---

## Author Table

| Author        | Created On   | Version | Last Updated By | Last Edited On | Reviewer        |
| ------------- | ------------ | ------- | --------------- | -------------- | --------------- |
| Saransh Rai | 14-04-2026 | 1.0     | Saransh Rai         | 14-04-2026   |  |

---

## Table of Contents

* [Introduction](#introduction)
* [Purpose](#purpose)
* [Scope](#scope)
* [Prerequisites](#prerequisites)
* [Disk Usage Monitoring](#disk-usage-monitoring)
* [Mount Points Verification](#mount-points-verification)
* [Ulimit (Resource Limits)](#ulimit-resource-limits)
* [Validation](#validation)
* [Use Cases](#use-cases)
* [Troubleshooting](#troubleshooting)
* [Best Practices](#best-practices)
* [Contact Information](#contact-information)
* [References](#references)

---

## Introduction

This SOP provides a structured guide to monitor disk usage, verify mount points, and configure ulimit settings in Ubuntu systems.

---

## Purpose

* Monitor disk utilization and prevent disk overflow
* Identify mounted file systems and storage allocation
* Configure resource limits (ulimit) for users and processes
* Ensure system stability and performance

---

## Scope

This SOP applies to:

* Linux/Ubuntu servers
* DevOps engineers and system administrators
* Production and staging environments

---

## Prerequisites

* Ubuntu 20.04 / 22.04
* Root or sudo access
* Basic knowledge of Linux commands

---

## Disk Usage Monitoring

### Step 1: Check Disk Usage (Filesystem Level)

```bash
df -h
```

### Screenshot Placeholder

<img width="1212" height="608" alt="image" src="https://github.com/user-attachments/assets/ca4746d0-ed63-46ad-80ec-3ad0c4716c74" />


---

### Step 2: Check Directory Size

```bash
du -sh /var/*
```

<img width="681" height="348" alt="image" src="https://github.com/user-attachments/assets/2c52a486-8b92-4bd1-8cb7-5b16cc85b992" />


---

### Step 3: Check Overall Disk Consumption

```bash
du -sh /*
```

<img width="496" height="150" alt="image" src="https://github.com/user-attachments/assets/e8d61bb8-305b-480f-8874-c5da2bccce45" />


---

## Mount Points Verification

### Step 1: List Block Devices

```bash
lsblk
```

<img width="787" height="287" alt="image" src="https://github.com/user-attachments/assets/3f7d62ad-d96f-4c9a-aef3-3b67cf05a1ed" />


---

### Step 2: Check Mounted Filesystems

```bash
mount | grep "^/dev"
```

<img width="1167" height="242" alt="image" src="https://github.com/user-attachments/assets/86e96122-b793-4458-a74d-0692d381b8f3" />

---

### Step 3: View Detailed Disk Info

```bash
fdisk -l
```

<img width="621" height="916" alt="image" src="https://github.com/user-attachments/assets/ca8adfb9-1fc3-4a20-ac30-b6b00eeb4f25" />


---

## Ulimit (Resource Limits)

### Step 1: Check Current Limits

```bash
ulimit -a
```

<img width="952" height="477" alt="image" src="https://github.com/user-attachments/assets/2e586ae9-4553-42de-b320-b48552cabddd" />


---

### Step 2: Check Open File Limit

```bash
ulimit -n
```

<img width="546" height="108" alt="image" src="https://github.com/user-attachments/assets/6add0ae4-2cc1-4692-9197-a1be29f6de8c" />


---

### Step 3: Temporarily Increase Limit

```bash
ulimit -n 65535
```

<img width="522" height="66" alt="image" src="https://github.com/user-attachments/assets/e5cdf5c9-35c4-4b60-849d-2d5823cd2f25" />


---

### Step 4: Permanent Configuration

```bash
sudo nano /etc/security/limits.conf
```

### Add Below Lines

```
* soft nofile 65535
* hard nofile 65535
```

---

### Step 5: Apply Changes

* Logout and login again
* Or restart the system

---

## Validation

### Verify Disk Usage

```bash
df -h
```


---

### Verify Ulimit

```bash
ulimit -n
```

Expected:

```
65535
```



---

## Use Cases

### Scenario 1: Disk Full

```bash
df -h
du -sh /*
sudo apt-get clean
```

<img width="921" height="722" alt="image" src="https://github.com/user-attachments/assets/fe792bd9-80cd-46fb-9561-22947c488624" />


---

### Scenario 2: Too Many Open Files

```bash
ulimit -n
ulimit -n 65535
```

---

## Troubleshooting

| Issue               | Cause                 | Solution                         |
| ------------------- | --------------------- | -------------------------------- |
| Disk full           | Large files/logs      | Use du to find large directories |
| System slow         | High disk usage       | Clean unused files               |
| Too many open files | Low ulimit            | Increase ulimit                  |
| Changes not applied | Session not restarted | Re-login                         |

---

## Best Practices

* Monitor disk usage regularly
* Clean logs and temporary files
* Avoid setting unlimited resource values
* Apply ulimit changes carefully
* Use automation tools for monitoring

---

## Contact Information

| Name        | Email                                                   |
| ----------- | ------------------------------------------------------- |
| Saransh Rai | saransh.rai.snaatak@mygurukulam.co |

---

## References

* Ubuntu Documentation
* Linux Man Pages

---
