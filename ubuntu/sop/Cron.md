# SOP for Cron in Ubuntu

| Author           | Created on | Version | Last updated by | Last edited on | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer      |
|------------------|------------|---------|-----------------|----------------|--------------|-------------|-------------|------------------|
| Shivam Uniyal    | 14-04-2026 | v1.0    | Shivam Uniyal   | 22-04-2026     | Team         | Anuj Jain   | Prashant    | Piyush Upadhyay  |

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [Purpose](#2-purpose)
3. [Prerequisites](#3-prerequisites)
4. [Check Cron Service](#4-check-cron-service)
5. [Create a Cron Job](#5-create-a-cron-job)
6. [Manage Cron Jobs](#6-manage-cron-jobs)
7. [Verify and Logs](#7-verify-and-logs)
8. [Troubleshooting](#8-troubleshooting)
9. [FAQs](#9-faqs)
10. [Conclusion](#10-conclusion)
11. [Contact Information](#11-contact-information)
12. [References](#12-references)

---

## 1. Introduction

Cron is a time-based job scheduler in Linux that allows users to automate repetitive and routine tasks such as running scripts, taking backups, clearing logs, and performing system maintenance activities at predefined intervals.  
It runs in the background and executes commands based on defined time patterns (minute, hour, day, etc.), ensuring consistency, saving time, and reducing manual effort.

---

## 2. Purpose

This SOP provides a step-by-step guide to:

- Create cron jobs  
- Edit and manage cron jobs  
- Monitor execution using logs  
- Troubleshoot common issues  

---

## 3. Prerequisites

Before proceeding, ensure the following:

- Ubuntu system installed  
- Basic knowledge of Linux commands  
- Terminal access 

---

## 4. Check Cron Service

### 4.1 Check Status
```bash
systemctl status cron
```

### 4.2 Start Service
```bash
sudo systemctl start cron
```

### 4.3 Enable at Boot
```bash
sudo systemctl enable cron
```

<img width="1232" height="508" src="https://github.com/user-attachments/assets/ff0ec827-1810-4e86-8354-8540cde13635" />

---

## 5. Create a Cron Job

### 5.1 Open Crontab
```bash
crontab -e
```

### 5.2 Cron Syntax
```bash
* * * * * command
| | | | |
| | | | └── Day of week (0-7)
| | | └──── Month (1-12)
| | └────── Day of month (1-31)
| └──────── Hour (0-23)
└────────── Minute (0-59)
```

### 5.3 Example
```bash
* * * * * echo "Hello Cron" >> /home/shivam/cron.log
```

<img width="1232" height="646" src="https://github.com/user-attachments/assets/90963e31-1721-42cc-b53f-59424d767940" />

---

## 6. Manage Cron Jobs

### 6.1 List Jobs
```bash
crontab -l
```

### 6.2 Edit Jobs
```bash
crontab -e
```

<img width="1232" height="677" src="https://github.com/user-attachments/assets/14b926e6-c9d4-4e85-a185-4742b528d993" />

### 6.3 Remove Jobs
```bash
crontab -r
```

<img width="779" height="272" src="https://github.com/user-attachments/assets/28e19248-1fcb-44b2-b73b-337b4b797871" />

---

## 7. Verify and Logs

### 7.1 Check Cron Logs
```bash
grep CRON /var/log/syslog
```

<img width="1436" height="776" src="https://github.com/user-attachments/assets/ffb21fa7-200f-48fb-a380-f6c133b599bb" />

### 7.2 Check Output File
```bash
cat /home/shivam/cron.log
```

<img width="779" height="272" src="https://github.com/user-attachments/assets/bb8cf79c-1169-4375-9d9b-17c1be926d2d" />

---

## 8. Troubleshooting

| Issue                 | Possible Cause      | Solution                          |
|----------------------|-------------------|-----------------------------------|
| Cron not running     | Service stopped    | Start using `systemctl start cron` |
| Command not executing| Wrong syntax       | Verify cron format                |
| Permission denied    | Lack of privileges | Use sudo or correct permissions   |
| Logs not visible     | Wrong log path     | Check `/var/log/syslog`           |

---

## 9. FAQs

**Q1. What is cron used for?**  
Cron is used to automate repetitive tasks like backups, scripts, and system maintenance.

**Q2. How do I edit an existing cron job?**  
```bash
crontab -e
```

**Q3. How can I check if my cron job is running?**  
```bash
grep CRON /var/log/syslog
```

**Q4. What happens if cron syntax is incorrect?**  
The job will not run, so always verify syntax before saving.

---

## 10. Conclusion

This SOP helps automate repetitive tasks using cron.  
It improves efficiency and ensures reliable execution of scheduled jobs.

---

## 11. Contact Information

| Name           | Email ID |
|----------------|----------|
| Shivam Uniyal  | shivam.uniyal.snaatak@mygurukulam.co |

---

## 12. References

| Link | Description |
|------|------------|
| https://man7.org/linux/man-pages/man5/crontab.5.html | Official cron documentation |
| https://ubuntu.com | Ubuntu official documentation |
