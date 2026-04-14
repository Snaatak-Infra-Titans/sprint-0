# SOP: Common Stack | Operating System | Ubuntu | Disk Usage & Ulimit Management

---

## Author Table

| Author        | Created On   | Version | Last Updated By | Last Edited On | Reviewer        |
| ------------- | ------------ | ------- | --------------- | -------------- | --------------- |
| Saransh Rai | 14-04-2026 | 1.0     | Saransh         | 14-042026  |  |

---

## Table of Contents

* Introduction
* Purpose
* Scope
* Prerequisites
* Disk Usage Monitoring
* Mount Points Verification
* Ulimit (Resource Limits)
* Validation
* Use Cases
* Troubleshooting
* Best Practices
* Contact Information
* References

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

📸 *Insert Screenshot: df -h output here*

---

### Step 2: Check Directory Size

```bash
du -sh /var/*
```

📸 *Insert Screenshot: du -sh /var/* output here*

---

### Step 3: Check Overall Disk Consumption

```bash
du -sh /*
```

📸 *Insert Screenshot: du -sh /* output here*

---

## Mount Points Verification

### Step 1: List Block Devices

```bash
lsblk
```

📸 *Insert Screenshot: lsblk output here*

---

### Step 2: Check Mounted Filesystems

```bash
mount | grep "^/dev"
```

📸 *Insert Screenshot: mount output here*

---

### Step 3: View Detailed Disk Info

```bash
fdisk -l
```

📸 *Insert Screenshot: fdisk -l output here*

---

## Ulimit (Resource Limits)

### Step 1: Check Current Limits

```bash
ulimit -a
```

📸 *Insert Screenshot: ulimit -a output here*

---

### Step 2: Check Open File Limit

```bash
ulimit -n
```

📸 *Insert Screenshot: ulimit -n output here*

---

### Step 3: Temporarily Increase Limit

```bash
ulimit -n 65535
```

📸 *Insert Screenshot: temporary ulimit change here*

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

📸 *Insert Screenshot: limits.conf configuration here*

---

### Step 5: Apply Changes

* Logout and login again
* Or restart the system

📸 *Insert Screenshot: post-login validation*

---

## Validation

### Verify Disk Usage

```bash
df -h
```

📸 *Insert Screenshot: validation df output*

---

### Verify Ulimit

```bash
ulimit -n
```

Expected:

```
65535
```

📸 *Insert Screenshot: ulimit validation output*

---

## Use Cases

### Scenario 1: Disk Full

```bash
df -h
du -sh /*
sudo apt-get clean
```

📸 *Insert Screenshot: disk cleanup process*

---

### Scenario 2: Too Many Open Files

```bash
ulimit -n
ulimit -n 65535
```

📸 *Insert Screenshot: ulimit issue fix*

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

| Name | Email |
| ---- | ----- |
| Saransh |  saransh.rai.snaatak@mygurukulam.co     |
