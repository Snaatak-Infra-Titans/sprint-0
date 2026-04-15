# Python — Introduction

| Author | Created On | Version | Last Updated By | Last Edited On | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|--------|------------|---------|-----------------|----------------|--------------|-------------|-------------|-------------|
| Deepak | April 2026 | v1.0 | Deepak | April 2026 | | | | |

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [History](#2-history)
3. [Features](#3-features)
4. [Use Cases](#4-use-cases)
5. [Python in OT-Microservices](#5-python-in-ot-microservices)
6. [Conclusion](#6-conclusion)
7. [Contact Information](#7-contact-information)
8. [References](#8-references)

---

## 1. Introduction

Python is a high-level, general-purpose, interpreted programming language known for its clean syntax and readability. Created with the philosophy that code should be easy to read and write, Python has grown into one of the most widely used programming languages in the world — spanning web development, data science, automation, artificial intelligence, and systems tooling.

Python follows the principle: **"There should be one — and preferably only one — obvious way to do it."** This makes Python codebases consistent and approachable across teams of different experience levels.

> **In the context of OT-Microservices:** Python powers the **Attendance API**, built with the Flask framework, and uses PostgreSQL for relational data storage and Redis for caching.

---

## 2. History

Understanding Python's history helps explain why it is designed the way it is and why it became so dominant.

### 2.1 Origin

| Year | Event |
|------|-------|
| **Late 1980s** | Guido van Rossum, a Dutch programmer at Centrum Wiskunde & Informatica (CWI) in the Netherlands, began designing Python as a successor to the ABC language |
| **1991** | Python 0.9.0 was released publicly — the first published version. It already included functions, exception handling, and core data types like lists and dictionaries |
| **1994** | Python 1.0 released, introducing functional programming tools like `lambda`, `map`, `filter`, and `reduce` |
| **2000** | Python 2.0 released, adding list comprehensions, garbage collection, and Unicode support |
| **2008** | Python 3.0 released — a major, backward-incompatible revision that cleaned up design inconsistencies. `print` became a function, integer division was fixed, and Unicode was made the default string type |
| **2020** | Python 2 officially reached End of Life. All active projects were expected to migrate to Python 3 |
| **2023–2024** | Python 3.11 and 3.12 released with significant performance improvements (up to 60% faster than Python 3.10) |

### 2.2 The Name

Python is **not** named after the snake. Guido van Rossum named it after the British comedy series **Monty Python's Flying Circus**, which he was watching while writing the language. This is why Python documentation and tutorials often contain playful references to spam, eggs, and parrots.

### 2.3 Governance

Python is developed and maintained by the **Python Software Foundation (PSF)**, a non-profit organization. Development is guided by **PEPs (Python Enhancement Proposals)** — formal documents that propose new features, syntax changes, or community guidelines.

The most famous PEP is **PEP 8**, which defines the official Python style guide and is followed by virtually all Python projects.

---

## 3. Features

Python's design decisions make it distinctly suited for both beginners and experienced engineers.

### 3.1 Readable and Clean Syntax

Python uses indentation to define code blocks instead of braces `{}`. This enforces a consistent code style and eliminates the "where does this block end?" problem common in other languages.

```python
# Python: indentation IS the structure
def greet(name):
    if name:
        print(f"Hello, {name}!")
    else:
        print("Hello, stranger!")
```

Compare this to Java or C, where the same logic requires braces, semicolons, and type declarations. Python's syntax resembles pseudocode — it reads almost like written English.

### 3.2 Interpreted Language

Python code is executed line by line by the Python interpreter at runtime. There is no separate compile step. This means:

- You can run a `.py` file immediately after writing it
- Errors are caught at runtime (not ahead of time)
- Interactive testing is possible using the Python REPL (`python3` in the terminal)

```bash
$ python3
>>> 2 + 2
4
>>> print("hello")
hello
```

### 3.3 Dynamically Typed

You do not need to declare the type of a variable. Python figures it out at runtime.

```python
x = 10          # integer
x = "hello"     # now a string — no error
x = [1, 2, 3]   # now a list — still no error
```

This speeds up development but requires careful attention to types in production code. Python 3.5+ introduced **optional type hints** to add static-typing-like documentation without losing flexibility:

```python
def add(a: int, b: int) -> int:
    return a + b
```

### 3.4 Large Standard Library

Python ships with an extensive standard library — called the **"batteries included"** philosophy. Without installing anything extra, you can:

| Module | What it does |
|--------|-------------|
| `os` | File system operations, environment variables |
| `json` | Parse and generate JSON |
| `datetime` | Date and time manipulation |
| `re` | Regular expressions |
| `http.server` | Spin up a basic HTTP server |
| `subprocess` | Run shell commands from Python |
| `logging` | Structured application logging |
| `unittest` | Write and run test cases |

### 3.5 Rich Third-Party Ecosystem (PyPI)

Beyond the standard library, Python has the **Python Package Index (PyPI)** with over 500,000 packages. Install any package with a single command:

```bash
pip install flask        # Web framework
pip install requests     # HTTP client
pip install psycopg2     # PostgreSQL driver
pip install redis        # Redis client
```

### 3.6 Cross-Platform

Python runs on Linux, macOS, and Windows without code changes. The same `.py` file runs identically on all platforms. This is especially important in DevOps and cloud contexts where the development machine (macOS/Windows) differs from the deployment server (Linux).

### 3.7 Multiple Programming Paradigms

Python supports several styles of programming:

| Paradigm | Description | Python Support |
|----------|-------------|----------------|
| **Procedural** | Step-by-step instructions using functions | ✅ Full support |
| **Object-Oriented** | Organize code into classes and objects | ✅ Full support |
| **Functional** | Use functions as values, avoid shared state | ✅ Partial (lambdas, map, filter) |
| **Scripting** | Write quick automation scripts | ✅ Ideal for this |

### 3.8 Memory Management

Python handles memory automatically using **reference counting** and a **garbage collector**. Developers do not manually allocate or free memory (unlike C or C++). This reduces a major class of bugs — memory leaks and dangling pointers — at the cost of some performance overhead.

### 3.9 Strong Community and Documentation

Python has one of the largest and most active developer communities in the world. The official documentation at [docs.python.org](https://docs.python.org) is comprehensive, well-maintained, and beginner-friendly.

---

## 4. Use Cases

Python's versatility means it is used across virtually every domain of software. The following are the major areas where Python excels.

### 4.1 Web Development

Python has mature web frameworks that power production applications at scale.

| Framework | Type | Used For |
|-----------|------|----------|
| **Flask** | Micro-framework | Lightweight APIs, microservices (used in OT-Microservices) |
| **Django** | Full-stack framework | Large web applications with admin panels, ORMs |
| **FastAPI** | Modern async framework | High-performance REST APIs with automatic docs |

**Example — Flask API endpoint (same pattern as the Attendance API):**

```python
from flask import Flask, jsonify, request

app = Flask(__name__)

@app.route('/api/v1/attendance/health', methods=['GET'])
def health_check():
    return jsonify({"message": "Attendance API is running fine..."})

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=8081)
```

### 4.2 Data Science and Machine Learning

Python is the dominant language in data science, largely due to its numerical computing libraries.

| Library | Purpose |
|---------|---------|
| `NumPy` | Fast numerical arrays and matrix operations |
| `Pandas` | Data manipulation and analysis (DataFrames) |
| `Matplotlib` / `Seaborn` | Data visualization and charting |
| `Scikit-learn` | Classical machine learning algorithms |
| `TensorFlow` / `PyTorch` | Deep learning and neural networks |

Companies like Google, Meta, and Netflix use Python as their primary data science language.

### 4.3 Automation and Scripting

Python is ideal for writing scripts that automate repetitive tasks:

- Renaming thousands of files
- Parsing log files and generating reports
- Sending automated emails
- Scraping websites for data
- Running database cleanup jobs

```python
import os

# Rename all .log files to include today's date
from datetime import date
today = date.today().isoformat()

for filename in os.listdir('/var/log/app'):
    if filename.endswith('.log'):
        os.rename(filename, f"{today}_{filename}")
```

### 4.4 DevOps and Infrastructure Automation

Python is heavily used in the DevOps space:

| Tool / Platform | Python Role |
|-----------------|-------------|
| **Ansible** | Playbooks are YAML but modules are written in Python |
| **AWS Boto3** | Official AWS SDK for Python — used to automate EC2, S3, RDS |
| **Terraform** (via CDK) | AWS CDK supports Python for infrastructure as code |
| **Fabric** | SSH-based deployment automation in Python |
| **pytest** | Testing infrastructure configurations |

### 4.5 System Administration

System administrators use Python to write tools that interact with the operating system, parse configuration files, manage users, and schedule tasks — all without needing a compiled binary.

### 4.6 Database Scripting

Python connects to virtually every major database:

| Database | Python Driver |
|----------|---------------|
| PostgreSQL | `psycopg2`, `asyncpg` |
| MySQL / MariaDB | `mysql-connector-python` |
| Redis | `redis-py` |
| MongoDB | `pymongo` |
| ScyllaDB / Cassandra | `cassandra-driver` |
| SQLite | Built into standard library (`sqlite3`) |

### 4.7 Testing and Quality Assurance

Python's testing ecosystem is mature:

- `unittest` — built-in testing framework
- `pytest` — the most popular testing library, supports fixtures and plugins
- `selenium` — browser automation for end-to-end testing
- `locust` — load testing framework written in Python

### 4.8 Artificial Intelligence and Generative AI

With the rise of large language models and AI tooling, Python has become even more central:

- Most AI model APIs (OpenAI, Anthropic, Hugging Face) provide official Python SDKs
- Jupyter Notebooks (Python) are the standard environment for AI research
- Python is used for fine-tuning, prompt engineering, and building AI-powered applications

---

## 5. Python in OT-Microservices

In the OT-Microservices project, Python is used specifically for the **Attendance API**.

| Attribute | Detail |
|-----------|--------|
| **Framework** | Flask (micro-framework) |
| **Port** | 8081 |
| **Database** | PostgreSQL (via `psycopg2`) |
| **Cache** | Redis (via `redis-py`) |
| **Dependency Manager** | Poetry |
| **Production Server** | Gunicorn |
| **Python Version** | 3.11 (specified in `pyproject.toml`) |

**Why Python for Attendance?**
The Attendance API handles time-series records — one row per employee per date. This relational structure fits PostgreSQL well, and Python's Flask framework provides a fast way to expose simple REST endpoints over this data. The lightweight nature of Flask means the service starts quickly and consumes minimal memory.

**Why Gunicorn in production?**
Flask's built-in development server is single-threaded and not suitable for production traffic. Gunicorn is a WSGI server that spawns multiple worker processes, allowing the Flask app to handle concurrent requests safely.

```bash
# How the Attendance API is started in production
gunicorn --bind 0.0.0.0:8081 app:app
```

---

## 6. Conclusion

Python's combination of readable syntax, vast library ecosystem, and versatility across domains — from web APIs to data science to infrastructure automation — makes it one of the most valuable languages to know in modern software engineering.

Key takeaways:

- Python was designed for **readability first**, making it maintainable at scale
- It is **interpreted and dynamically typed**, enabling rapid development and iteration
- Its ecosystem (Flask, Django, Pandas, Ansible) covers virtually every engineering domain
- In OT-Microservices, Python serves as the **Attendance API** using Flask + PostgreSQL + Redis
- Understanding Python fundamentals directly enables contributing to the Attendance API codebase

---

## 7. Contact Information

| Name | Role | Email |
|------|------|-------|
| Deepak | Author | deepak.nagar.snaatak@mygurukulam.co |

---

## 8. References

| Resource | Link |
|----------|------|
| Official Python Documentation | https://docs.python.org/3/ |
| Python Software Foundation | https://www.python.org/psf/ |
| PEP 8 — Style Guide | https://peps.python.org/pep-0008/ |
| Flask Documentation | https://flask.palletsprojects.com |
| Gunicorn Documentation | https://gunicorn.org |
| PyPI — Python Package Index | https://pypi.org |
| OT-Microservices Repository | https://github.com/OT-MICROSERVICES |
| Attendance API Source | https://github.com/OT-MICROSERVICES/attendance-api |

---

*Author: Deepak | Sprint 0 | Infra-Titans | April 2026*
