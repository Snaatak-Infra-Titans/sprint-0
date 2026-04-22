# SOP for Cron in Ubuntu

| Author           | Created on | Version | Last updated by | Last edited on | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer      |
|------------------|------------|---------|-----------------|----------------|--------------|-------------|-------------|------------------|
| Shivam Uniyal    | 14-04-2026 | v1.0    | Shivam Uniyal   | 22-04-2026     | Team         | Anuj Jain   | Prashant    | Piyush Upadhyay  |

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [Purpose](#2-purpose)
3. [Check Cron Service](#3-check-cron-service)
   - 3.1 [Check Status](#31-check-status)
   - 3.2 [Start Service](#32-start-service)
   - 3.3 [Enable at Boot](#33-enable-at-boot)
4. [Create a Cron Job](#4-create-a-cron-job)
   - 4.1 [Open Crontab](#41-open-crontab)
   - 4.2 [Cron Syntax](#42-cron-syntax)
   - 4.3 [Example](#43-example)
5. [Manage Cron Jobs](#5-manage-cron-jobs)
   - 5.1 [List Jobs](#51-list-jobs)
   - 5.2 [Edit Jobs](#52-edit-jobs)
   - 5.3 [Remove Jobs](#53-remove-jobs)
6. [Verify and Logs](#6-verify-and-logs)
   - 6.1 [Check Cron Logs](#61-check-cron-logs)
   - 6.2 [Check Output File](#62-check-output-file)
7. [Troubleshooting](#7-troubleshooting)
8. [FAQs](#8-faqs)
9. [Contact Information](#9-contact-information)
10. [References](#10-references)
11. [Conclusion](#11-conclusion)

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

## 3. Check Cron Service

### 3.1 Check Status
```bash
systemctl status cron
```

### 3.2 Start Service
```bash
sudo systemctl start cron
```

### 3.3 Enable at Boot
```bash
sudo systemctl enable cron
```

<img width="1232" height="508" src="https://github.com/user-attachments/assets/ff0ec827-1810-4e86-8354-8540cde13635" />

---

## 4. Create a Cron Job

### 4.1 Open Crontab
```bash
crontab -e
```

### 4.2 Cron Syntax
```bash
* * * * * command
| | | | |
| | | | └── Day of week (0-7)
| | | └──── Month (1-12)
| | └────── Day of month (1-31)
| └──────── Hour (0-23)
└────────── Minute (0-59)
```

### 4.3 Example
```bash
* * * * * echo "Hello Cron" >> /home/shivam/cron.log
```

<img width="1232" height="646" src="https://github.com/user-attachments/assets/90963e31-1721-42cc-b53f-59424d767940" />

---

## 5. Manage Cron Jobs

### 5.1 List Jobs
```bash
crontab -l
```

### 5.2 Edit Jobs
```bash
crontab -e
```

<img width="1232" height="677" src="https://github.com/user-attachments/assets/14b926e6-c9d4-4e85-a185-4742b528d993" />

### 5.3 Remove Jobs
```bash
crontab -r
```

<img width="779" height="272" src="https://github.com/user-attachments/assets/28e19248-1fcb-44b2-b73b-337b4b797871" />

---

## 6. Verify and Logs

### 6.1 Check Cron Logs
```bash
grep CRON /var/log/syslog
```
<img width="1436" height="776" alt="Screenshot 2026-04-22 at 5 02 03 PM" src="https://github.com/user-attachments/assets/ffb21fa7-200f-48fb-a380-f6c133b599bb" />

### 6.2 Check Output File
```bash
cat /home/shivam/cron.log
```

<img width="779" height="272" src="https://github.com/user-attachments/assets/bb8cf79c-1169-4375-9d9b-17c1be926d2d" />

---

## 7. Troubleshooting

| Issue                 | Possible Cause      | Solution                          |
|----------------------|-------------------|-----------------------------------|
| Cron not running     | Service stopped    | Start using `systemctl start cron` |
| Command not executing| Wrong syntax       | Verify cron format                |
| Permission denied    | Lack of privileges | Use sudo or correct permissions   |
| Logs not visible     | Wrong log path     | Check `/var/log/syslog`           |

---

## 8. FAQs

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

## 9. Contact Information

| Name           | Email ID |
|----------------|----------|
| Shivam Uniyal  | shivam.uniyal.snaatak@mygurukulam.co |

---

## 10. References

| Link | Description |
|------|------------|
| https://man7.org/linux/man-pages/man5/crontab.5.html | Official cron documentation |
| https://ubuntu.com | Ubuntu official documentation |

---

## 11. Conclusion

This SOP provides a clear and structured approach to managing cron jobs in Ubuntu. It enables automation of repetitive tasks, reducing manual effort and improving overall efficiency. By following the defined steps for creation, management, and monitoring, users can ensure reliable execution of scheduled jobs.

Proper verification and troubleshooting practices help maintain system stability and prevent failures.
