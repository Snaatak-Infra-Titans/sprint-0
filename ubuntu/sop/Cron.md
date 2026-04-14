# SOP for Cron in Ubuntu

| Author           | Created on | Version | Last updated by | Last edited on | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|------------------|------------|---------|-----------------|----------------|--------------|-------------|-------------|-------------|
| Shivam Uniyal    | 14-04-2026 | v1.0    | Shivam Uniyal   | 14-04-2026     |              |             |             |             |

---

## Table of Contents

1. Introduction  
2. Purpose  
3. Prerequisites  
4. Step 1: Check Cron Service  
5. Step 2: Create a Cron Job  
6. Step 3: Manage Cron Jobs  
7. Step 4: Verify and Logs  
8. Troubleshooting  
9. FAQs  
10. Contact Information  
11. References  

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
* * * * * echo "Hello Cron" >> /home/$USER/cron.log
```

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

Remove all cron jobs:

```bash
crontab -r
```

---

## 7. Step 4: Verify and Logs

Check cron logs:

```bash
grep CRON /var/log/syslog
```

Check output file:

```bash
cat /home/$USER/cron.log
```

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
