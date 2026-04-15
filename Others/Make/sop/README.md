#  Make Installation & Usage Guide (Ubuntu 24.04)

Automate build and task execution using Make (GNU Make)

---

##  Document Information

| Author | Created on | Version | Last updated by | Last edited on | PRE Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
| ------ | ---------- | ------- | --------------- | -------------- | ------------ | ----------- | ----------- | ----------- |
| Gourav | 15-04-2026 | v1.0    | Gourav          | 15-04-2026     | -            | -           | -           | -           |

---

##  Overview

This guide explains:

* ✅ Make Installation (APT)
* ✅ Makefile Basics
* ✅ Common Commands
* ✅ Practical Examples

---

##  What is Make?

Make (GNU Make) is a:

* Build automation tool
* Task runner
* Used in C, C++, DevOps, CI/CD pipelines

---

##  Make Basics

| Component  | Purpose                      |
| ---------- | ---------------------------- |
| Makefile   | File containing instructions |
| Target     | Task to execute              |
| Dependency | Required files               |
| Command    | Action to run                |

---

##  Prerequisites

### Check Ubuntu Version

```bash
lsb_release -a
```

---

### Update System

```bash
sudo apt update && sudo apt upgrade -y
```

> 📸 *Add screenshot here*

---

##  Installation

###  Method A: Install Make (Recommended)

```bash
sudo apt install -y make
```

---

### Verify Installation

```bash
make --version
```

> 📸 *Add screenshot here*

---

###  Install Build Essentials (Recommended for DevOps)

```bash
sudo apt install -y build-essential
```

👉 Includes:

* make
* gcc (compiler)
* g++
* libraries

---

## 📂 Makefile Structure

Basic syntax:

```make
target: dependency
	command
```

>  Command must start with **TAB (not spaces)**

---

##  First Example

### Create Makefile

```bash
nano Makefile
```

---

### Add Content

```make
hello:
	echo "Hello, Gourav!"
```

---

### Run Make

```bash
make hello
```

---

## 🔄 Multiple Targets Example

```make
install:
	echo "Installing..."

build:
	echo "Building..."

run:
	echo "Running app..."
```

---

### Execute

```bash
make install
make build
make run
```

---

## ⚙️ Variables in Makefile

```make
NAME=Gourav

greet:
	echo "Hello $(NAME)"
```

---

## 🔗 Dependency Example

```make
app: build
	echo "App is ready"

build:
	echo "Building project..."
```

---

Run:

```bash
make app
```

👉 First runs `build`, then `app`

---

##  Commonly Used Commands

### Run Default Target

```bash
make
```

👉 Runs first target in Makefile

---

### Run Specific Target

```bash
make build
```

---

### Dry Run (Check Commands)

```bash
make -n
```

---

### Debug Mode

```bash
make -d
```

---

### Ignore Errors

```bash
make -i
```

---

### Parallel Execution

```bash
make -j4
```

---

##  Useful Options

| Option | Meaning              |
| ------ | -------------------- |
| `-n`   | Show commands only   |
| `-d`   | Debug output         |
| `-j`   | Run jobs in parallel |
| `-f`   | Specify Makefile     |
| `-C`   | Run in directory     |

---

##  Real DevOps Example

```make
install:
	pip install -r requirements.txt

run:
	python app.py

test:
	pytest

clean:
	rm -rf __pycache__
```

---

##  Debugging

### Show Commands Without Executing

```bash
make -n
```

---

### Debug Dependency Issues

```bash
make -d
```

---

### Verbose Output

```bash
make VERBOSE=1
```

---

## ❗ Common Issues

### make: command not found

```bash
sudo apt install -y make
```

---

### Missing TAB Error

❌ Wrong:

```make
echo "Hello"
```

✅ Correct:

```make
	echo "Hello"
```

---

### Target Not Found

Check:

```bash
make <target-name>
```

---

### File Not Updating

Force rebuild:

```bash
make -B
```

---

##  Quick Commands

| Task          | Command                 |
| ------------- | ----------------------- |
| Install Make  | `sudo apt install make` |
| Check version | `make --version`        |
| Run default   | `make`                  |
| Run target    | `make <target>`         |
| Debug         | `make -d`               |
| Dry run       | `make -n`               |
| Parallel      | `make -j4`              |

---

## 🎉 Done!

You have successfully:

* Installed Make
* Created your first Makefile
* Used targets and dependencies
* Learned debugging techniques

---

**Author:** Gourav Sharma | Sprint 0 | OT-Microservices 