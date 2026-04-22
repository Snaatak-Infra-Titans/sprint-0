<p align="center">
  <img width="480" height="360" alt="image" src="https://github.com/user-attachments/assets/e8d4a2fc-ac40-4650-a6c6-bf0cd48763ac" />
</p>


# SOP: Common Stack | Operating System | Ubuntu | Disk Usage & Ulimit Management

---

# Author Table

| **Author**  | **Created On** | **Version** | **Last Updated By** | **Last Edited On** | **Pre Reviewer** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ----------- | -------------- | ----------- | ------------------- | ------------------ | ---------------- | --------------- | --------------- | --------------- |
| Saransh Rai | 14-04-2026     | 1.0         | Saransh Rai         | 14-04-2026         |                  |                 |                 |                 |

---

# Table of Contents

1. [Introduction](#1-introduction)
2. [Purpose](#2-purpose)
3. [Disk Usage Monitoring](#3-disk-usage-monitoring)
4. [Mount Points Verification](#4-mount-points-verification)
5. [Ulimit (Resource Limits)](#5-ulimit-resource-limits)
6. [Validation](#6-validation)
7. [Use Cases](#7-use-cases)
8. [Troubleshooting](#8-troubleshooting)
9. [Best Practices](#9-best-practices)
10. [Contact Information](#10-contact-information)
11. [Conclusion](#11-conclusion)
12. [References](#12-references)

---

# 1. Introduction

This SOP provides a structured guide to monitor disk usage, verify mount points, and configure ulimit settings in Ubuntu systems.

---

# 2. Purpose

I. Monitor disk utilization and prevent disk overflow  
II. Identify mounted file systems and storage allocation  
III. Configure resource limits (ulimit) for users and processes  
IV. Ensure system stability and performance

---

# 3. Disk Usage Monitoring

### Step 1: Check Disk Usage (Filesystem Level)

```bash
df -h
```

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

# 4. Mount Points Verification

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

# 5. Ulimit (Resource Limits)

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

image

Add Below Lines:

```bash
* soft nofile 65535
* hard nofile 65535
```

---

### Step 5: Apply Changes

* Logout and login again
* Or restart the system

---

# 6. Validation

### Verify Disk Usage

```bash
df -h
```

---

### Verify Ulimit

```bash
ulimit -n
```

**Expected:**

```
65535
```

---

# 7. Use Cases

| **Scenario**        | **Commands / Actions**                                  |
| ------------------- | ------------------------------------------------------- |
| Disk Full           | `df -h`<br>`du -sh /*`<br>`sudo apt-get clean` |
| Too Many Open Files | `ulimit -n`<br>`ulimit -n 65535`                        |

---

# 8. Troubleshooting

| **Issue**           | **Cause**             | **Solution**                     |
| ------------------- | --------------------- | -------------------------------- |
| Disk full           | Large files/logs      | Use du to find large directories |
| System slow         | High disk usage       | Clean unused files               |
| Too many open files | Low ulimit            | Increase ulimit                  |
| Changes not applied | Session not restarted | Re-login or reboot system        |

---

# 9. Best Practices

| # | Best Practice                           | Description                          |
| - | --------------------------------------- | ------------------------------------ |
| 1 | Monitor disk usage regularly            | Use df/du or monitoring tools        |
| 2 | Clean logs and temporary files          | Prevent unnecessary disk consumption |
| 3 | Avoid setting unlimited resource values | Reduces risk of system exhaustion    |
| 4 | Apply ulimit changes carefully          | Test before applying in production   |
| 5 | Use automation tools for monitoring     | Enables proactive alerts             |

---

# 10. Contact Information

| **Name**    | **Email**                                                                       |
| ----------- | ------------------------------------------------------------------------------- |
| Saransh Rai | [saransh.rai.snaatak@mygurukulam.co](mailto:saransh.rai.snaatak@mygurukulam.co) |

---

# 11. Conclusion

This SOP provides a comprehensive approach to monitoring disk usage, verifying mount points, and managing system resource limits using ulimit in Ubuntu environments. By following these steps, administrators can proactively prevent disk-related issues, optimize system performance, and ensure stability in production systems.

---

# 12. References

| Topic                | Link                                                                                                                                                                           |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Ubuntu Documentation | [https://help.ubuntu.com/](https://help.ubuntu.com/)                                                                                                                           |
| Linux Man Pages      | [https://man7.org/linux/man-pages/](https://man7.org/linux/man-pages/)                                                                                                         |
| Ulimit Documentation | [https://www.geeksforgeeks.org/linux-unix/ulimit-soft-limits-and-hard-limits-in-linux/](https://www.geeksforgeeks.org/linux-unix/ulimit-soft-limits-and-hard-limits-in-linux/) |
| Disk Usage (df, du)  | [https://www.geeksforgeeks.org/linux-unix/df-command-in-linux-with-examples/](https://www.geeksforgeeks.org/linux-unix/df-command-in-linux-with-examples/)                     |

