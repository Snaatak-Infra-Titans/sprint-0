# Gunicorn — Introduction

| Author | Created On | Version | Last Updated By | Last Edited On | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|--------|------------|---------|-----------------|----------------|--------------|-------------|-------------|-------------|
| Deepak | April 2026 | v1.0 | Deepak | April 2026 | | | | |

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [What is Gunicorn?](#2-what-is-gunicorn)
3. [Why Gunicorn?](#3-why-gunicorn)
4. [Key Features](#4-key-features)
5. [How Gunicorn Works](#5-how-gunicorn-works)
6. [Gunicorn in OT-Microservices](#6-gunicorn-in-ot-microservices)
7. [Conclusion](#7-conclusion)
8. [Contact Information](#8-contact-information)
9. [References](#9-references)

---

## 1. Introduction

When you build a Python web application using a framework like Flask or Django, the framework comes with a built-in development server. That server is intentionally minimal — it handles one request at a time, has no fault tolerance, and is explicitly not designed for production use. 

To serve a Python application to real users in production, you need a **production-grade WSGI server**. Gunicorn is the most widely used solution for this in the Python ecosystem.

> **In the context of OT-Microservices:** Gunicorn is used to run the **Attendance API** (Python/Flask) in production on port 8081.

---

## 2. What is Gunicorn?

**Gunicorn** (short for **Green Unicorn**) is a **Python WSGI HTTP Server** for Unix. It is a pre-fork worker model server — meaning it forks multiple worker processes from a master process to handle incoming HTTP requests concurrently.

| Attribute | Detail |
|-----------|--------|
| **Full Name** | Green Unicorn |
| **Type** | WSGI (Web Server Gateway Interface) HTTP Server |
| **Language** | Written in Python |
| **License** | MIT |
| **First Released** | 2010 |
| **Interface Standard** | WSGI (PEP 3333) |
| **Supported Frameworks** | Flask, Django, FastAPI (via adapter), Pyramid, and any WSGI-compatible app |
| **Install** | `pip install gunicorn` |

### 2.1 What is WSGI?

**WSGI** stands for **Web Server Gateway Interface**. It is a Python standard (defined in PEP 3333) that specifies how a web server communicates with a Python web application.

Think of WSGI as a contract: as long as your Python app follows the WSGI specification, any WSGI server (like Gunicorn) can run it — regardless of which framework was used to build it.

```
Browser / Client
      │
      ▼
  Nginx (Reverse Proxy)         ← handles static files, SSL, load balancing
      │
      ▼
  Gunicorn (WSGI Server)        ← manages worker processes, handles concurrency
      │
      ▼
  Flask App (WSGI Application)  ← your actual application logic
      │
      ▼
  PostgreSQL / Redis             ← databases
```

---

## 3. Why Gunicorn?

### 3.1 The Problem with Flask's Built-in Server

Flask includes a development server that you start with `flask run` or `app.run()`. It is useful during development but has critical limitations that make it unsuitable for production:

| Limitation | Impact |
|------------|--------|
| **Single-threaded** | Only handles one request at a time — all other requests wait in a queue |
| **No worker management** | If the process crashes, the app goes down and nothing restarts it |
| **No request queuing** | Under load, requests are dropped rather than queued |
| **Security warnings built-in** | Flask itself prints "Do not use the development server in a production environment" |
| **No graceful shutdown** | Killing the process mid-request corrupts in-flight operations |

### 3.2 Why Gunicorn Solves This

Gunicorn addresses every one of these limitations:

| Flask Dev Server | Gunicorn |
|------------------|----------|
| 1 worker, 1 request at a time | Multiple workers handle requests in parallel |
| Crashes bring the app down | Master process restarts crashed workers automatically |
| No request management | Workers are managed and monitored continuously |
| Development only | Designed and hardened for production traffic |
| No signal handling | Supports graceful restarts and zero-downtime deploys |

### 3.3 Why Gunicorn Over Alternatives?

Several WSGI servers exist for Python. Gunicorn is the most commonly chosen for these reasons:

| Server | Strengths | Weakness vs Gunicorn |
|--------|-----------|----------------------|
| **Gunicorn** | Simple config, stable, battle-tested, excellent Flask/Django support | Not async-native |
| **uWSGI** | Very feature-rich, high performance | Complex configuration, steeper learning curve |
| **Waitress** | Cross-platform (works on Windows) | Lower performance under high concurrency |
| **mod_wsgi** | Deep Apache integration | Requires Apache, heavier setup |
| **Uvicorn** | Excellent for async (ASGI) frameworks like FastAPI | Not WSGI — not suitable for standard Flask |

For a straightforward Flask microservice like the Attendance API, Gunicorn offers the best balance of simplicity, reliability, and performance.

---

## 4. Key Features

### 4.1 Pre-Fork Worker Model

Gunicorn uses a **pre-fork** architecture. When Gunicorn starts, a **master process** forks a configurable number of **worker processes** before any requests arrive. Each worker is an independent Python process that handles requests independently.

```
Gunicorn Master Process (PID 1234)
├── Worker 1 (PID 1235)  ← handling request from User A
├── Worker 2 (PID 1236)  ← handling request from User B
├── Worker 3 (PID 1237)  ← idle, waiting for next request
└── Worker 4 (PID 1238)  ← handling request from User C
```

**Benefits of pre-forking:**
- Workers are ready before requests arrive — no startup delay per request
- If one worker crashes, the master immediately forks a replacement
- Workers are completely isolated — a crash in Worker 1 does not affect Workers 2, 3, or 4

### 4.2 Multiple Worker Types

Gunicorn supports different types of workers depending on the workload:

| Worker Type | Flag | Best For |
|-------------|------|----------|
| **sync** (default) | `--worker-class sync` | Standard Flask/Django apps, CPU-bound work |
| **gthread** | `--worker-class gthread` | Apps with I/O wait, uses threads per worker |
| **gevent** | `--worker-class gevent` | High-concurrency I/O-bound apps (requires `gevent`) |
| **tornado** | `--worker-class tornado` | Tornado-based applications |
| **uvicorn** | `--worker-class uvicorn.workers.UvicornWorker` | ASGI apps (FastAPI) running under Gunicorn |

For the OT-Microservices Attendance API, the default `sync` worker is appropriate.

### 4.3 Configurable Worker Count

The number of workers is configurable. The commonly recommended formula is:

```
workers = (2 × CPU cores) + 1
```

For a 2-core server, this means 5 workers. Each worker can handle one request at a time, so 5 workers means 5 simultaneous requests.

```bash
# Start with 5 workers
gunicorn --workers 5 --bind 0.0.0.0:8081 app:app
```

### 4.4 Automatic Worker Restart

If a worker process crashes (due to an unhandled exception, memory issue, or signal), the master process detects this and immediately spawns a replacement. The application never fully goes down due to a single worker failure.

### 4.5 Graceful Reloads (Zero-Downtime Deploys)

When you update your application code and need to restart Gunicorn, you can send a `HUP` signal instead of killing the process. Gunicorn will:

1. Fork new workers running the new code
2. Wait for the old workers to finish their in-flight requests
3. Gracefully shut down the old workers

```bash
# Graceful reload without dropping any requests
kill -HUP <gunicorn_master_pid>
```

### 4.6 Request Timeout

Gunicorn automatically kills workers that take too long to respond, preventing slow requests from blocking workers indefinitely.

```bash
# Kill any worker that doesn't respond within 30 seconds
gunicorn --timeout 30 app:app
```

### 4.7 Unix Socket Support

Instead of binding to a TCP port, Gunicorn can listen on a Unix socket file. This is faster when Nginx and Gunicorn run on the same machine because Unix socket communication avoids the TCP/IP stack.

```bash
# Bind to a Unix socket instead of a port
gunicorn --bind unix:/tmp/attendance.sock app:app
```

### 4.8 Logging

Gunicorn has built-in access and error logging, configurable to write to files or stdout:

```bash
gunicorn --access-logfile /var/log/attendance-access.log \
         --error-logfile  /var/log/attendance-error.log \
         app:app
```

### 4.9 Integration with Nginx

Gunicorn is designed to sit **behind** a reverse proxy like Nginx, not be exposed directly to the internet. Nginx handles:
- SSL/TLS termination
- Static file serving
- Rate limiting and DDoS protection
- Connection buffering

Gunicorn then handles:
- WSGI request processing
- Worker process management
- Python application execution

This separation of concerns is the standard production deployment pattern for Python web applications.

---

## 5. How Gunicorn Works

### 5.1 Startup Sequence

When you run `gunicorn app:app`:

1. Gunicorn reads the app reference (`app:app` means: from the module named `app`, use the object named `app`)
2. The master process loads the application once into memory
3. The master forks N worker processes (each inheriting the loaded app from the master)
4. Workers bind to the configured address and start accepting connections
5. The master enters a monitoring loop — watching for worker crashes, signals, and config changes

### 5.2 Request Lifecycle

```
1. Client sends HTTP request
2. Nginx receives it, forwards to Gunicorn (via TCP port or Unix socket)
3. Gunicorn master assigns the request to an available worker
4. Worker calls the WSGI application (Flask app) with the request data
5. Flask processes the request (queries DB, applies business logic)
6. Flask returns an HTTP response to Gunicorn
7. Gunicorn sends the response back to Nginx
8. Nginx sends the response back to the client
```

### 5.3 Basic Command Syntax

```bash
gunicorn [OPTIONS] MODULE:APPLICATION

# MODULE   = the Python file name (without .py)
# APPLICATION = the Flask/Django app object inside that file
```

**Examples:**

```bash
# Minimal — bind to 0.0.0.0:8000 with 1 worker (default)
gunicorn app:app

# Production — 4 workers, specific port, logging
gunicorn --workers 4 --bind 0.0.0.0:8081 app:app

# Background process with log output
nohup gunicorn --workers 4 --bind 0.0.0.0:8081 app:app > gunicorn.log 2>&1 &
```

---

## 6. Gunicorn in OT-Microservices

In the OT-Microservices project, Gunicorn serves the **Attendance API** (Flask application).

### 6.1 How It Is Started

```bash
cd ~/attendance-api

# Start Gunicorn in the background, managed by Poetry's virtual environment
nohup poetry run gunicorn --bind 0.0.0.0:8081 app:app > ~/attendance.log 2>&1 &
```

| Part | Meaning |
|------|---------|
| `poetry run` | Execute the command inside Poetry's virtual environment |
| `gunicorn` | The WSGI server |
| `--bind 0.0.0.0:8081` | Listen on all network interfaces, port 8081 |
| `app:app` | Load object `app` from the file `app.py` |
| `> ~/attendance.log 2>&1 &` | Redirect all output to a log file and run in background |

### 6.2 Architecture Position

```
Browser
  │
  ▼
Nginx (Port 80)
  │  location /attendance/ → proxy to localhost:8081
  ▼
Gunicorn (Port 8081)
  │  runs the Flask WSGI app
  ▼
Flask Attendance API (app.py)
  │
  ├──► PostgreSQL (attendance records)
  └──► Redis (response caching)
```

### 6.3 Verifying It Is Running

```bash
# Check the health endpoint through Nginx
curl http://localhost/attendance/health

# Check Gunicorn is listening on port 8081 directly
curl http://localhost:8081/api/v1/attendance/health

# Check the process is running
ps aux | grep gunicorn

# Watch live logs
tail -f ~/attendance.log
```

---

## 7. Conclusion

Gunicorn fills a critical gap in Python web application deployment — the space between a development server and a full production stack. Its pre-fork model, automatic worker restart, graceful reloads, and simple configuration make it the go-to WSGI server for Flask and Django applications.

Key takeaways:

- Flask's built-in server is for **development only** — Gunicorn is required for production
- Gunicorn uses a **pre-fork worker model** — multiple isolated processes handle requests in parallel
- It integrates naturally with **Nginx**, which sits in front and handles SSL, static files, and connection buffering
- In OT-Microservices, Gunicorn runs the **Attendance API** on port 8081 inside Poetry's virtual environment
- Worker count should follow the formula: **(2 × CPU cores) + 1**

---

## 8. Contact Information

| Name | Role | Email |
|------|------|-------|
| Deepak | Author | deepak.nagar.snaatak@mygurukulam.co |

---

## 9. References

| Resource | Link |
|----------|------|
| Gunicorn Official Documentation | https://gunicorn.org |
| Gunicorn Configuration Reference | https://docs.gunicorn.org/en/stable/settings.html |
| PEP 3333 — WSGI Standard | https://peps.python.org/pep-3333/ |
| Flask Deployment Options | https://flask.palletsprojects.com/en/3.0.x/deploying/ |
| OT-Microservices Attendance API | https://github.com/OT-MICROSERVICES/attendance-api |

---

*Author: Deepak | Sprint 0 | Infra-Titans | April 2026*
