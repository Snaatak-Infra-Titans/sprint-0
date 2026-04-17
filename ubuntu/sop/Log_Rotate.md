
#  SOP: Log Rotation Management Using Logrotate

---

##  Document Information

| Author           | Created on  | Version | Last updated by | Last edited on | PRE Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|------------------|------------|---------|-----------------|----------------|-------------|------------|------------|------------|
| Versha Tripathi  | 13-04-2026 | v1.0    | Versha Tripathi | 13-04-2026     | Team           | -          | -          | -          |


---

## Table of Contents

1. [Purpose](#1-purpose)
2. [Scope](#2-scope)
3. [Prerequisites](#3-prerequisites)
4. [Configuration Structure](#4-logrotate-configuration-structure)
5. [Key Parameters](#5-key-configuration-parameters)
6. [Configuration Steps](#6-configuration-steps)
7. [Testing](#11-testing-configuration)
8. [Automation](#12-automation)
9. [Troubleshooting](#13-monitoring--troubleshooting)
10. [Best Practices](#14-best-practices)
11. [Example](#15-production-example)


---

##  1. Purpose

This SOP explains how to manage logs using **logrotate** to:

* Prevent disk space issues
* Improve system performance
* Maintain clean and manageable logs

---

##  2. Scope

Applicable to all Linux servers using logrotate for:

* System logs
* Application logs

---

##  3. Prerequisites

* Root / sudo access
* logrotate installed

###  Verify Installation

```bash
logrotate --version
```



<img width="609" height="227" alt="image" src="https://github.com/user-attachments/assets/11a069aa-b8d3-40d1-a707-4b159499e35e" />


---

##  4. Logrotate Configuration Structure

| Path                  | Purpose                  |
| --------------------- | ------------------------ |
| `/etc/logrotate.conf` | Main config              |
| `/etc/logrotate.d/`   | Service-specific configs |

<img width="653" height="670" alt="image" src="https://github.com/user-attachments/assets/089dbf0f-99ed-4edf-8d87-cdc68a8de206" />

---

##  5. Key Configuration Parameters

| Directive                | Description            |
| ------------------------ | ---------------------- |
| daily / weekly / monthly | Rotation frequency     |
| rotate N                 | Number of logs to keep |
| compress                 | Compress logs          |
| delaycompress            | Delay compression      |
| missingok                | Ignore missing logs    |
| notifempty               | Skip empty logs        |
| create                   | Create new log file    |
| copytruncate             | Truncate original log  |

---

##  6. Configuration Steps

### 6.1 Global Configuration

```bash
sudo nano /etc/logrotate.conf
```

```conf
weekly
rotate 4
create
compress
include /etc/logrotate.d
```
<img width="1090" height="642" alt="image" src="https://github.com/user-attachments/assets/009a8931-1c3c-418f-aa13-768dbb07505f" />

---

### 6.2 Service-Specific Configuration

```bash
sudo nano /etc/logrotate.d/myapp
```

```conf
/var/log/myapp/*.log {
    daily
    rotate 7
    compress
    delaycompress
    missingok
    notifempty
    create 0640 root adm
    copytruncate
}
```

<img width="626" height="314" alt="image" src="https://github.com/user-attachments/assets/2c38f0ec-518c-4f4c-9ff5-8da69b544732" />

---

##  7. Rotation Frequency

| Requirement | Config    |
| ----------- | --------- |
| Daily       | `daily`   |
| Weekly      | `weekly`  |
| Monthly     | `monthly` |

---

##  8. Retention Policy

```conf
rotate 14
```

➡ Keeps logs for 14 days

---

##  9. Compression

```conf
compress
delaycompress
```

* Saves disk space
* Delays compression for safety

---

##  10. Post-Rotation Actions

```conf
postrotate
    systemctl restart myapp
endscript
```

📸 **Screenshot Placeholder:**

```
![Post rotate action](screenshots/post-rotate.png)
```

---

##  11. Testing Configuration

### Dry Run

```bash
sudo logrotate -d /etc/logrotate.conf
```

### Force Run

```bash
sudo logrotate -f /etc/logrotate.conf
```

📸 **Screenshot Placeholder:**

```
![Logrotate test](screenshots/logrotate-test.png)
```

---

##  12. Automation

* Runs automatically via:

  * cron → `/etc/cron.daily/logrotate`
  * systemd → `logrotate.timer`

```bash
systemctl status logrotate.timer
```

<img width="1498" height="279" alt="image" src="https://github.com/user-attachments/assets/6a9be864-f235-40ad-bde8-96ac9e8dc787" />


---

##  13. Monitoring & Troubleshooting

### Check Status

```bash
cat /var/lib/logrotate/status
```

### Common Issues

| Issue              | Cause           | Solution           |
| ------------------ | --------------- | ------------------ |
| Logs not rotating  | Bad config      | Use `-d`           |
| Permission denied  | Wrong ownership | Fix `create`       |
| Logs still growing | No truncation   | Use `copytruncate` |

---

##  14. Best Practices

* Use separate config per app
* Enable compression
* Avoid very high retention
* Always test configs
* Monitor disk usage

---

##  15. Production Example

```conf
/var/log/myapp/*.log {
    daily
    rotate 30
    compress
    delaycompress
    missingok
    notifempty
    create 0640 myapp myapp
    copytruncate
}
```




##  Final Note

Using logrotate properly helps keep your system:

* Clean
* Efficient
* Production-ready
