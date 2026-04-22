#  Gunicorn Installation & Setup Guide (Ubuntu 24.04)

Run Python applications in production using Gunicorn (WSGI HTTP Server)

---

##  

| Author | Created on | Version | Last updated by | Last edited on | PRE Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
| ------ | ---------- | ------- | --------------- | -------------- | ------------ | ----------- | ----------- | ----------- |
| Gourav | 15-04-2026 | v1.0    | Gourav          | 15-04-2026     | Team         | -           | -           | -           |

---

##  Overview

This guide explains how to install and run Gunicorn using:

*  pip (Recommended)
*  Virtual Environment (Best Practice)
*  Systemd (Production Setup)

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
<img width="1171" height="202" alt="image" src="https://github.com/user-attachments/assets/ddfe3fd8-8c90-48f9-a353-6235d014323d" />

---

### Update System

```bash
sudo apt update && sudo apt upgrade -y
```
<img width="1171" height="202" alt="image" src="https://github.com/user-attachments/assets/8f3562e9-7594-4f94-9217-f6e6699229aa" />


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
<img width="1151" height="191" alt="image" src="https://github.com/user-attachments/assets/6ddd0b48-2e26-4289-b761-d9977fc6ed04" />

---

### Verify Installation

```bash
gunicorn --version
```
<img width="1282" height="379" alt="image" src="https://github.com/user-attachments/assets/10b14d4a-ea29-41b3-8bf2-f7cae9e0bdb7" />


---

### Method B: Install inside Virtual Environment (Best Practice)

```bash
python3 -m venv myenv
source myenv/bin/activate
pip install gunicorn
```
<img width="1205" height="510" alt="image" src="https://github.com/user-attachments/assets/275e3ad8-5c90-475e-a954-4208b053867d" />

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

<img width="1153" height="263" alt="image" src="https://github.com/user-attachments/assets/12dbb365-15f7-454d-a045-051bbf5e5e9a" />

---

##  Run Application with Gunicorn

```bash
gunicorn app:app
```
<img width="1307" height="654" alt="image" src="https://github.com/user-attachments/assets/b07a5b83-a68f-4f03-826d-b20a820981e6" />


 Format:

```
gunicorn <filename>:<app_variable>
```

---

### Run on Custom Port

```bash
gunicorn -b 0.0.0.0:8000 app:app 

gunicorn -b 127.0.0.1:8000 app:app 
```
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/539b9a07-03c9-4cab-9fb6-57ee156bca7e" />


<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/8f78a776-9760-4065-8ed9-01b8905d319b" />

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


##  Production Setup (Systemd Service)

### Create Service File

```bash
sudo nano /etc/systemd/system/gunicorn.service
```
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
<img width="1569" height="424" alt="image" src="https://github.com/user-attachments/assets/c66c2a96-3747-49e0-a09c-16f3860672aa" />


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
<img width="1693" height="708" alt="image" src="https://github.com/user-attachments/assets/f4681bd1-27df-4daf-9818-8a5b4300a690" />

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
<img width="1693" height="708" alt="image" src="https://github.com/user-attachments/assets/a9c9994c-965e-44c6-97f5-9f50ad0d4df1" />

---




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

## Contact Information

| Name   | Email                                                                             |
| ------ | --------------------------------------------------------------------------------- |
| gourav sharma | [gourav.sharma.snaatak@mygurukulam.co](mailto:gourav.sharma.snaatak@mygurukulam.co) |

---
