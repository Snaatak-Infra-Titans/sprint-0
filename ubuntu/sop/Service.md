# SOP: Managing Linux Services with systemctl

> A step-by-step guide to manage Linux services using "systemctl", including starting, stopping, enabling, disabling, and checking service status.

---

## Document Information

| Author | Date       | Version | Project                      | Audience                        |
|--------|------------|---------|------------------------------|---------------------------------|
| Gourav | 14 April 2026 | 1.0     | OT-Microservices \| Sprint 0 | Beginners to Mid-level Engineers |

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


# Start other common services
sudo systemctl start postgresql
sudo systemctl start redis

![alt text](image.png)


> ** Note:** If no output is returned, the command executed successfully. Use "systemctl status" to verify the service state.

---

### 3.2 Stop a Service

Use this to immediately stop a running service. This does **not** prevent it from starting again on the next reboot.


# Stop a service
sudo systemctl stop nginx


# If a service does not stop cleanly, force it
sudo systemctl kill nginx



### 3.3 Restart a Service

Restart stops and then starts a service in one step. Use this after changing a config file.

# Restart a service (stop + start)
sudo systemctl restart nginx


# Reload config without downtime (if service supports it)
sudo systemctl reload nginx

> **  Tip:** Prefer `reload` over `restart` when possible. `reload` applies config changes without dropping active connections — especially useful for web servers like nginx.

---

### 3.4 Enable a Service

Enabling a service creates a symlink so that systemd starts it automatically the next time the server boots. It does **not** start the service right now.

```bash
# Enable a service to start at boot
sudo systemctl enable nginx

# Enable AND start in one command
sudo systemctl enable --now nginx
```

---

### 3.5 Disable a Service

Disabling removes the boot-time symlink, so the service will **not** start automatically on reboot. It does not stop the currently running service.

```bash
# Disable a service from starting at boot
sudo systemctl disable nginx

# Disable AND stop in one command
sudo systemctl disable --now nginx
```


---

## 4. Checking Service Status

The `status` command is the single most useful `systemctl` command. It tells you whether a service is running, how long it has been running, and shows its recent log output all at once.

```bash
sudo systemctl status nginx
```

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


# Watch logs live as they appear
journalctl -u nginx -f


# Logs from the last hour only
journalctl -u nginx --since '1 hour ago'


# Show only error messages
journalctl -u nginx -p err


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

| Resource | Where to Find It |
|----------|-----------------|
| systemd Documentation | `man systemctl` (run in terminal) |
| OT-Microservices Repository | https://github.com/OT-MICROSERVICES |
| Cron Jobs SOP | SOP_Cron_Jobs.docx |
| Common Linux Commands SOP | SOP_Common_Commands.md |

---

*Author: Gourav Sharma | Sprint 0 | Opstree Solutions | 14 April 2026*
