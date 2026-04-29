# SOP For Logrotate

## Document Information

| Author | Created On | Version | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|--------|------------|---------|-------------|-------------|-------------|
| Versha Tripathi | 13-04-2026 | v1.0 | Prince Batra | Nikita Joshi | Piyush Upadhyay |

---



## Table of Contents

1. [Purpose](#1-purpose)
2. [Prerequisites](#2-prerequisites)
3. [Logrotate Configuration Structure](#3-logrotate-configuration-structure)
4. [Key Configuration Parameters](#4-key-configuration-parameters)
5. [Configuration Steps](#5-configuration-steps)
6. [Rotation Frequency](#6-rotation-frequency)
7. [Retention Policy](#7-retention-policy)
8. [Testing Configuration](#8-testing-configuration)
9. [Automation](#9-automation)
10. [Monitoring & Troubleshooting](#10-monitoring--troubleshooting)
11. [Conclusion](#11-conclusion)




--- 
## 1. Purpose


Log rotation is a critical system administration practice that ensures log files do not consume unlimited disk space over time. **Logrotate** is a standard Linux utility that automates this process — it periodically rotates, compresses, and removes old log files based on configurable rules. This SOP provides step-by-step guidance for setting up and managing logrotate across system and application services.


This SOP explains how to manage logs using **logrotate** to prevent disk space issues, improve system performance, and maintain clean, manageable log files.

---


## 2. Prerequisites

- logrotate installed on the system

### Verify Installation

```bash
logrotate --version
```



<img width="609" height="227" alt="image" src="https://github.com/user-attachments/assets/11a069aa-b8d3-40d1-a707-4b159499e35e" />


---

## 3. Logrotate Configuration Structure

Logrotate uses two key config locations:

- **`/etc/logrotate.conf`** — The main global configuration file that defines default rotation settings applied across the system.
- **`/etc/logrotate.d/`** — A directory containing service-specific configuration files, where each application can define its own rotation rules independently.

<img width="653" height="670" alt="image" src="https://github.com/user-attachments/assets/089dbf0f-99ed-4edf-8d87-cdc68a8de206" />

---

---

## 4. Key Configuration Parameters

| Directive | Parameter | Description |
|-----------|-----------|-------------|
| `daily` / `weekly` / `monthly` | Rotation Frequency | Defines how often log rotation runs — use `daily` for high-traffic apps, `weekly` for moderate, `monthly` for low-volume logs. |
| `rotate N` | Number of Logs to Keep | Sets how many rotated log files are retained before older ones are deleted; e.g., `rotate 7` keeps one week of daily logs. |
| `compress` | Compress Rotated Logs | Compresses old log files using gzip to save disk space; compressed files get a `.gz` extension automatically. |
| `delaycompress` | Delay Compression by One Cycle | Skips compression on the most recently rotated log, allowing active processes that may still write to it to close safely first. |
| `missingok` | Ignore Missing Log Files | Prevents logrotate from throwing an error if the specified log file does not exist; useful during early app deployment. |
| `notifempty` | Skip Rotation of Empty Logs | Does not rotate a log file if it contains no data, avoiding unnecessary empty archived files. |
| `create` | Create New Log File After Rotation | Automatically creates a fresh, empty log file with specified permissions after the old one is rotated away. |
| `copytruncate` | Truncate Instead of Rename | Copies the log to a new file and then empties the original in-place, useful when an app cannot be restarted to reopen the log file. |

---

## 5. Configuration Steps

### 5.1 Global Configuration

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

### 5.2 Service-Specific Configuration

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

## 6. Rotation Frequency

| Requirement | Config Directive |
|-------------|-----------------|
| Daily | `daily` |
| Weekly | `weekly` |
| Monthly | `monthly` |

---

---

## 7. Retention Policy

```conf
rotate 14
```

Keeps logs for 14 rotation cycles (e.g., 14 days if rotating daily).

---


## 8. Testing Configuration

### Dry Run (Simulate Without Applying)

```bash
sudo logrotate -d /etc/logrotate.conf
```

### Force Run (Apply Immediately)

```bash
sudo logrotate -f /etc/logrotate.conf
```

---

## 9. Automation

Logrotate runs automatically via one of the following:

- **cron** → `/etc/cron.daily/logrotate`
- **systemd** → `logrotate.timer`

```bash
systemctl status logrotate.timer
```

<img width="1498" height="279" alt="image" src="https://github.com/user-attachments/assets/6a9be864-f235-40ad-bde8-96ac9e8dc787" />


---

## 10. Monitoring & Troubleshooting

### Check Rotation Status

```bash
cat /var/lib/logrotate/status
```

### Common Issues

| Issue | Cause | Solution |
|-------|-------|----------|
| Logs not rotating | Bad/invalid config | Run with `-d` flag to debug and validate the configuration file. |
| Permission denied | Wrong file ownership | Fix the `create` directive to set correct owner and permissions. |
| Logs still growing | No truncation configured | Add `copytruncate` directive to truncate the original log in-place. |

---

## 11. Conclusion

Logrotate is a reliable and lightweight solution for automating log management on Linux systems. By defining appropriate rotation frequency, retention policies, and compression settings, teams can effectively prevent disk exhaustion, maintain system performance, and ensure logs remain accessible and well-organized. Regular testing of configurations using the dry-run mode, combined with automated scheduling via cron or systemd, ensures a robust and hands-free log management workflow across all environments.

---

## Contact Information

| Name | Email |
|------|-------|
| Versha Tripathi | versha.tripathi.snaatak@mygurukulam.co |

---

## References

| Reference | Link |
|-----------|------|
| logrotate man page | `man logrotate` |
| logrotate GitHub | https://github.com/logrotate/logrotate |
