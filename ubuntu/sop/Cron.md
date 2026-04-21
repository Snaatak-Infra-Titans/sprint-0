# SOP for Cron in Ubuntu

| Author           | Created on | Version | Last updated by | Last edited on | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer      |
|------------------|------------|---------|-----------------|----------------|--------------|-------------|-------------|------------------|
| Shivam Uniyal    | 14-04-2026 | v1.0    | Shivam Uniyal   | 21-04-2026     | Team         | Anuj Jain   | Prashant    | Piyush Upadhyay  |

---

## Table of Contents

- [Introduction](#introduction)
- [Purpose](#purpose)
- [Prerequisites](#prerequisites)
- [Step 1 Check Cron Service](#step-1-check-cron-service)
- [Step 2 Create a Cron Job](#step-2-create-a-cron-job)
- [Step 3 Manage Cron Jobs](#step-3-manage-cron-jobs)
- [Step 4 Verify and Logs](#step-4-verify-and-logs)
- [Troubleshooting](#troubleshooting)
- [FAQs](#faqs)
- [Contact Information](#contact-information)
- [References](#references)

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

It helps ensure reliable automation and follows DevOps best practices.

---

## 3. Prerequisites

- Ubuntu 24.04 (Local Machine)  
- Basic Linux command knowledge  
- Terminal access  

---

## 4. Step 1: Check Cron Service

Check if cron service is running:

```bash
systemctl status cron
```

Start cron service if not running:

```bash
sudo systemctl start cron
```

Enable cron at boot:

```bash
sudo systemctl enable cron
```
<img width="1232" height="508" alt="Screenshot 2026-04-14 at 11 08 34 PM" src="https://github.com/user-attachments/assets/ff0ec827-1810-4e86-8354-8540cde13635" />
---

## 5. Step 2: Create a Cron Job

Open crontab editor:

```bash
crontab -e
```

### Cron Syntax

```bash
* * * * * command
| | | | |
| | | | └── Day of week (0-7)
| | | └──── Month (1-12)
| | └────── Day of month (1-31)
| └──────── Hour (0-23)
└────────── Minute (0-59)
```

### Example

Run a command every minute:

```bash
* * * * * echo "Hello Cron" >> /home/shivam/cron.log
```
<img width="1232" height="646" alt="Screenshot 2026-04-14 at 11 17 47 PM" src="https://github.com/user-attachments/assets/90963e31-1721-42cc-b53f-59424d767940" />

---

## 6. Step 3: Manage Cron Jobs

List cron jobs:

```bash
crontab -l
```

Edit cron jobs:

```bash
crontab -e
```
<img width="1232" height="677" alt="Screenshot 2026-04-14 at 11 18 06 PM" src="https://github.com/user-attachments/assets/14b926e6-c9d4-4e85-a185-4742b528d993" />

Remove all cron jobs:

```bash
crontab -r
```
<img width="779" height="272" alt="Screenshot 2026-04-14 at 11 22 59 PM" src="https://github.com/user-attachments/assets/28e19248-1fcb-44b2-b73b-337b4b797871" />

---

## 7. Step 4: Verify and Logs

Check cron logs:

```bash
grep CRON /var/log/syslog
```

Check output file:

```bash
cat /home/shivam/cron.log
```
<img width="779" height="272" alt="Screenshot 2026-04-14 at 11 21 51 PM" src="https://github.com/user-attachments/assets/bb8cf79c-1169-4375-9d9b-17c1be926d2d" />

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

## 10. Contact Information

| Name           | Email ID |
|----------------|----------|
| Shivam Uniyal  | shivam.uniyal.snaatak@mygurukulam.co |

---

## 11. References

| Link | Description |
|------|------------|
| https://man7.org/linux/man-pages/man5/crontab.5.html | Official cron documentation |
| https://ubuntu.com | Ubuntu official documentation |
