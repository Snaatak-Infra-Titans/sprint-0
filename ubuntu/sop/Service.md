# SOP: Managing Linux Services with systemctl

> A step-by-step guide to manage Linux services using "systemctl", including starting, stopping, enabling, disabling, and checking service status.

---
| Author | Created on | Version | Last updated by | Last edited on | PRE Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
| ------ | ---------- | ------- | --------------- | -------------- | ------------ | ----------- | ----------- | ----------- |
| Gourav | 14-04-2026 | v1.0    | Gourav          | 14-04-2026     | -            | -           | -           | -           |

---


## Table of Contents

1. [Purpose](#1-purpose)
2. [What is systemctl?](#2-what-is-systemctl)
3. [Core systemctl Commands](#3-core-systemctl-commands)
   - [3.1 Start a Service](#31-start-a-service)
   - [3.2 Stop a Service](#32-stop-a-service)
   - [3.3 Restart a Service](#33-restart-a-service)
   - [3.4 Enable a Service](#34-enable-a-service)
   - [3.5 Disable a Service](#35-disable-a-service)
4. [Checking Service Status](#4-checking-service-status)
5. [Viewing Service Logs with journalctl](#5-viewing-service-logs-with-journalctl)
6. [Start vs Enable — Understanding the Difference](#6-start-vs-enable--understanding-the-difference)
7. [systemctl for OT-Microservices](#7-systemctl-for-ot-microservices)
   - [7.1 PostgreSQL](#71-postgresql)
   - [7.2 Redis](#72-redis)
   - [7.3 nginx (Reverse Proxy)](#73-nginx-reverse-proxy)
8. [Troubleshooting](#8-troubleshooting--when-a-service-fails)
9. [Quick Reference](#9-quick-reference)
10. [Conclusion](#10-conclusion)

---

## 1. Purpose

This SOP explains how to manage Linux system services using the `systemctl` command. It is written for team members who are comfortable with basic Linux commands and want to learn how to start, stop, enable, disable, and check the status of services.

By the end of this document, you will be able to:

- Understand what `systemctl` is and when to use it
- Start and stop services immediately
- Enable and disable services so they persist across reboots
- Check the live status and logs of any service
- Troubleshoot services that fail to start or stop

> **  Note:** All commands are tested on Ubuntu 22.04 LTS.

---

## 2. What is systemctl?

`systemctl` is the main command-line tool for managing services on modern Linux systems that use **systemd** as their init system. It lets you control whether a service is running right now and whether it starts automatically when the server boots.

Some common things people use `systemctl` for:

- Starting a service manually after deploying a new version
- Stopping a service before making configuration changes
- Enabling a service so it auto-starts after every reboot
- Checking whether a service crashed and reading why
- Restarting services as part of deployment scripts

> **  Tip:** Think of `systemctl` as the remote control for every background process on your Linux server.

---

## 3. Core systemctl Commands

The basic syntax for all `systemctl` commands is:

```bash
sudo systemctl <action> <service-name>
```

---

### 3.1 Start a Service

Use this to immediately start a service that is currently stopped. This does **not** change whether it auto-starts on reboot.


# Start a service
sudo systemctl start nginx

<img width="1801" height="877" alt="Screenshot 2026-04-14 213741" src="https://github.com/user-attachments/assets/29695397-6046-436a-b4e6-e2d4e4aad648" />


# Start other common services
sudo systemctl start postgresql
sudo systemctl start redis

<img width="1645" height="450" alt="Screenshot 2026-04-14 220751" src="https://github.com/user-attachments/assets/ea34ba2e-1562-4bb1-ab26-a54cae644d00" />


> ** Note:** If no output is returned, the command executed successfully. Use "systemctl status" to verify the service state.

---

### 3.2 Stop a Service

Use this to immediately stop a running service. This does **not** prevent it from starting again on the next reboot.


# Stop a service
sudo systemctl stop nginx

<img width="1828" height="740" alt="Screenshot 2026-04-14 214245" src="https://github.com/user-attachments/assets/bdbd1d42-ac05-462f-a833-7b26d6d86468" />



# If a service does not stop cleanly, force it
sudo systemctl kill nginx



### 3.3 Restart a Service

Restart stops and then starts a service in one step. Use this after changing a config file.

# Restart a service (stop + start)
sudo systemctl restart nginx
<img width="1916" height="900" alt="Screenshot 2026-04-14 214530" src="https://github.com/user-attachments/assets/986a3e2f-356a-4198-ac00-8d3d13e377bd" />

# Reload config without downtime (if service supports it)
sudo systemctl reload nginx

> **  Tip:** Prefer `reload` over `restart` when possible. `reload` applies config changes without dropping active connections — especially useful for web servers like nginx.

---

### 3.4 Enable a Service

Enabling a service creates a symlink so that systemd starts it automatically the next time the server boots. It does **not** start the service right now.

# Enable a service to start at boot
sudo systemctl enable nginx

# Enable AND start in one command
sudo systemctl enable --now nginx

<img width="1752" height="277" alt="Screenshot 2026-04-14 215825" src="https://github.com/user-attachments/assets/1d94d037-8a31-4776-8736-b22125f438e0" />

---

### 3.5 Disable a Service

Disabling removes the boot-time symlink, so the service will **not** start automatically on reboot. It does not stop the currently running service.

# Disable a service from starting at boot
sudo systemctl disable nginx

# Disable AND stop in one command
sudo systemctl disable --now nginx

<img width="1726" height="402" alt="Screenshot 2026-04-14 220050" src="https://github.com/user-attachments/assets/9defbeaa-cb92-4b3d-b9f9-616ae9ef22f6" />

---

## 4. Checking Service Status

The `status` command is the single most useful `systemctl` command. It tells you whether a service is running, how long it has been running, and shows its recent log output all at once.

sudo systemctl status nginx

<img width="1792" height="631" alt="Screenshot 2026-04-14 220211" src="https://github.com/user-attachments/assets/975826bc-be8e-4d95-9f36-ef9d8012f798" />

<img width="1792" height="631" alt="Screenshot 2026-04-14 220211" src="https://github.com/user-attachments/assets/d856c174-3417-473c-bfbe-b98aa0889562" />

**Example output:**

```
● nginx.service - A high performance web server
   Loaded: loaded (/lib/systemd/system/nginx.service; enabled)
   Active: active (running) since Mon 2026-04-13 09:00:01 UTC
  Process: 1234 ExecStart=/usr/sbin/nginx
 Main PID: 1235 (nginx)
```

**Key things to look for in the output:**

| Field | What to Look For |
|-------|-----------------|
| `Active: active (running)` | Service is healthy and running |
| `Active: inactive (dead)` | Service is stopped — not running |
| `Active: failed` | Service crashed — check the logs below |
| `Loaded: ... enabled` | Service will start on next reboot |
| `Loaded: ... disabled` | Service will NOT start on next reboot |

---

## 5. Viewing Service Logs with journalctl

When a service fails or behaves unexpectedly, `journalctl` lets you read its detailed logs. Unlike reading raw log files, `journalctl` is structured and filterable.


# Show last 50 lines of logs for a service
journalctl -u nginx -n 50

<img width="1334" height="207" alt="Screenshot 2026-04-14 221137" src="https://github.com/user-attachments/assets/985b45a3-efb6-4f42-a57d-3be6386e20fd" />

# Watch logs live as they appear
journalctl -u nginx -f

<img width="1256" height="207" alt="Screenshot 2026-04-14 221313" src="https://github.com/user-attachments/assets/2c766541-1188-4060-bf9c-0ec406248451" />

# Logs from the last hour only
journalctl -u nginx --since '1 hour ago'

<img width="1532" height="589" alt="Screenshot 2026-04-14 221657" src="https://github.com/user-attachments/assets/2dcf8b70-88d2-4870-854a-f9f440d7757f" />

# Show only error messages
journalctl -u nginx -p err

<img width="1370" height="232" alt="Screenshot 2026-04-14 221812" src="https://github.com/user-attachments/assets/5841b8a9-7c90-4250-8b4c-06e034debd2e" />

---

## 6. Start vs Enable — Understanding the Difference

This is the most common point of confusion for beginners. `start` and `enable` do two completely different things:

| Action | Effect Now | Effect After Reboot |
|--------|------------|---------------------|
| `start` | Starts immediately | No change — does not persist |
| `stop` | Stops immediately | No change — does not persist |
| `enable` | No change | Will auto-start on every reboot |
| `disable` | No change | Will NOT auto-start on reboot |
| `enable --now` | Starts immediately | Will also auto-start on reboot |
| `disable --now` | Stops immediately | Will also NOT auto-start on reboot |

> ** Tip:** For production services like nginx, PostgreSQL, or Redis, you almost always want both. Use `enable --now` to enable and start in a single command.

---

## 6.1 Viewing Unit File Configuration

  systemctl cat nginx

   Shows actual service configuration


## 7. systemctl for OT-Microservices

Here are ready-to-use `systemctl` commands specific to this project. You can run these directly on the server.

### 7.1 PostgreSQL

```bash
sudo systemctl start postgresql
sudo systemctl stop postgresql
sudo systemctl enable --now postgresql
sudo systemctl status postgresql
```

### 7.2 Redis

```bash
sudo systemctl start redis
sudo systemctl stop redis
sudo systemctl enable --now redis
sudo systemctl status redis
```

### 7.3 nginx (Reverse Proxy)

```bash
sudo systemctl start nginx
sudo systemctl reload nginx      # Reload config without downtime
sudo systemctl enable --now nginx
sudo systemctl status nginx
```

---

## 8. Troubleshooting — When a Service Fails

Most `systemctl` problems come down to one of a few causes. Here is a quick reference:

| Problem | Likely Cause | What to Do |
|---------|--------------|------------|
| Service fails to start | Config file error or missing dependency | Run `journalctl -u <service> -n 30` and read the last error line |
| Service starts but crashes after a few seconds | Application error or missing env variable | Check logs with `journalctl -u <service> -f` and look for `Exit code` |
| Service stops after reboot | Not enabled | Run `sudo systemctl enable <service>` |
| Status shows `failed` | Previous crash was not cleared | Run `sudo systemctl reset-failed <service>`, then start it again |
| Permission denied error in logs | Service running as wrong user | Check the `User=` field in the unit file at `/etc/systemd/system/` |

---

## 9. Quick Reference

| Command | What it Does |
|---------|-------------|
| `sudo systemctl start <service>` | Start the service immediately |
| `sudo systemctl stop <service>` | Stop the service immediately |
| `sudo systemctl restart <service>` | Stop then start the service |
| `sudo systemctl reload <service>` | Reload config without stopping (if supported) |
| `sudo systemctl enable <service>` | Auto-start at boot (does not start now) |
| `sudo systemctl disable <service>` | Remove auto-start at boot (does not stop now) |
| `sudo systemctl enable --now <service>` | Enable AND start in one command |
| `sudo systemctl disable --now <service>` | Disable AND stop in one command |
| `sudo systemctl status <service>` | Show status, PID, uptime, and recent logs |
| `journalctl -u <service> -n 50` | Show last 50 log lines for a service |
| `journalctl -u <service> -f` | Watch service logs in real time |
| `sudo systemctl list-units --type=service` | List all active services |
| `sudo systemctl daemon-reload` | Reload systemd after editing a unit file |

---

## 10. Conclusion

`systemctl` is the standard way to manage services on any modern Ubuntu or RHEL-based Linux server. Once you understand the difference between `start`/`stop` (immediate) and `enable`/`disable` (boot-time), you will be able to confidently manage the full lifecycle of any service.

**Key things to remember:**

- Use `start` and `stop` to control services immediately
- Use `enable` and `disable` to control what happens after a reboot
- Use `enable --now` and `disable --now` to do both at once
- Always run `systemctl status` after making changes to confirm the result
- Always begin troubleshooting with journalctl -u <service> -n 50 to identify the root cause quickly.

---

## 11 References

| Resource | Link |
|----------|------|
|OT-Microservices Repository | https://github.com/OT-MICROSERVICES|
|Ubuntu Man Pages | https://manpages.ubuntu.com|
|Linux Command Library | https://linuxcommandlibrary.com|
|Explain Shell (breaks down any command) | https://explainshell.com|
|systemctl Official Documentation | https://www.freedesktop.org/software/systemd/man/systemctl.html|
|systemd Man Pages | https://www.freedesktop.org/software/systemd/man/|

---

*Author: Gourav Sharma | Sprint 0 | Infra Titans | 14 April 2026*
