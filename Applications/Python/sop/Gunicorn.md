#  Gunicorn Installation & Setup Guide (Ubuntu 24.04)

Run Python applications in production using Gunicorn (WSGI HTTP Server)

---

##  Document Information

| Author | Created on | Version | Last updated by | Last edited on | PRE Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
| ------ | ---------- | ------- | --------------- | -------------- | ------------ | ----------- | ----------- | ----------- |
| Gourav | 15-04-2026 | v1.0    | Gourav          | 15-04-2026     | -            | -           | -           | -           |

---

##  Overview

This guide explains how to install and run Gunicorn using:

* ✅ pip (Recommended)
* ✅ Virtual Environment (Best Practice)
* ✅ Systemd (Production Setup)

---

## What is Gunicorn?

Gunicorn (**Green Unicorn**) is a:

* Python WSGI HTTP Server
* Used to run apps like Flask, Django in production
* Works behind NGINX

---

## Gunicorn Basics

| Component | Purpose                                  |
| --------- | ---------------------------------------- |
| WSGI      | Interface between Python app & server    |
| Gunicorn  | Runs Python app                          |
| Workers   | Handle multiple requests                 |
| NGINX     | Reverse proxy (optional but recommended) |

> Gunicorn runs your app, not for development (use Flask dev server only for testing)

---

##  Prerequisites

### Check Python Installed

```bash
python3 --version
```

---

### Update System

```bash
sudo apt update && sudo apt upgrade -y
```

> 📸 *Add screenshot here*

---

### Install pip & venv (if not installed)

```bash
sudo apt install -y python3-pip python3-venv
```

---

##  Installation

###  Method A: Install via pip (Recommended)

```bash
pip3 install gunicorn
```

---

### Verify Installation

```bash
gunicorn --version
```

> 📸 *Add screenshot here*

---

### Method B: Install inside Virtual Environment (Best Practice)

```bash
python3 -m venv myenv
source myenv/bin/activate
pip install gunicorn
```

---

##  Sample Application (Flask)

Create a test app:

```bash
nano app.py
```

```python
from flask import Flask
app = Flask(__name__)

@app.route("/")
def home():
    return "Hello from Gunicorn!"

if __name__ == "__main__":
    app.run()
```

---

## ▶️ Run Application with Gunicorn

```bash
gunicorn app:app
```

👉 Format:

```
gunicorn <filename>:<app_variable>
```

---

### Run on Custom Port

```bash
gunicorn -b 0.0.0.0:8000 app:app
```

---

### Run with Multiple Workers

```bash
gunicorn -w 4 app:app
```

---

## ⚙️ Gunicorn Important Options

| Option      | Meaning                 |
| ----------- | ----------------------- |
| `-w`        | Number of workers       |
| `-b`        | Bind address            |
| `--threads` | Number of threads       |
| `--reload`  | Auto restart (dev only) |
| `--daemon`  | Run in background       |

---

##  Worker Recommendation

```bash
workers = (2 × CPU cores) + 1
```

Example:

```bash
nproc
```

---

##  Production Setup (Systemd Service)

### Create Service File

```bash
sudo nano /etc/systemd/system/gunicorn.service
```

---

### Add Configuration

```ini
[Unit]
Description=Gunicorn Service
After=network.target

[Service]
User=snaatak
Group=www-data
WorkingDirectory=/home/snaatak/myapp
ExecStart=/home/snaatak/myenv/bin/gunicorn -w 3 -b 0.0.0.0:8000 app:app

[Install]
WantedBy=multi-user.target
```

---

### Reload Systemd

```bash
sudo systemctl daemon-reexec
sudo systemctl daemon-reload
```

---

### Start Gunicorn Service

```bash
sudo systemctl start gunicorn
```

---

### Enable on Boot

```bash
sudo systemctl enable gunicorn
```

---

### Check Status

```bash
sudo systemctl status gunicorn
```

---

### Stop Service

```bash
sudo systemctl stop gunicorn
```

---

### Restart Service

```bash
sudo systemctl restart gunicorn
```

---

##  Logs & Debugging

```bash
journalctl -u gunicorn -f
```

---

## (Optional) Use with NGINX

Gunicorn runs on port 8000 → NGINX handles public traffic

Flow:

```
User → NGINX → Gunicorn → App
```

---

## ❗ Common Issues

### Command not found

```bash
pip3 install gunicorn
```

---

### Permission Denied

```bash
chmod +x myenv/bin/gunicorn
```

---

### Port Already in Use

```bash
sudo lsof -i :8000
```

---

### App Not Loading

Check:

```bash
gunicorn app:app
```

Make sure:

* File name correct
* App variable name correct

---

##  Quick Commands

| Task             | Command                            |
| ---------------- | ---------------------------------- |
| Install Gunicorn | `pip3 install gunicorn`            |
| Run app          | `gunicorn app:app`                 |
| Run on port      | `gunicorn -b 0.0.0.0:8000 app:app` |
| Workers          | `gunicorn -w 4 app:app`            |
| Start service    | `systemctl start gunicorn`         |
| Check status     | `systemctl status gunicorn`        |
| Logs             | `journalctl -u gunicorn -f`        |

---

## 🎉 Done!

You have successfully:

* Installed Gunicorn
* Run a Python app using Gunicorn
* Configured production service using systemd

---

**Author:** Gourav Sharma | Sprint 0 | OT-Microservices 
