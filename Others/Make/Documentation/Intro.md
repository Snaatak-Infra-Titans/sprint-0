# Make — Introduction

| Author | Created On | Version | Last Updated By | Last Edited On | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|--------|------------|---------|-----------------|----------------|--------------|-------------|-------------|-------------|
| Deepak | April 2026 | v1.0 | Deepak | April 2026 | | | | |

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [What is Make?](#2-what-is-make)
3. [Why Make?](#3-why-make)
4. [Key Features](#4-key-features)
5. [Make in OT-Microservices](#5-make-in-ot-microservices)
6. [Conclusion](#6-conclusion)
7. [Contact Information](#7-contact-information)
8. [References](#8-references)

---

## 1. Introduction

Every software project has a set of repeated tasks — compile the code, run the tests, build a Docker image, run database migrations, clean up generated files. As a project grows, these tasks become longer, more complex, and easier to get wrong when typed manually every time.

**Make** is a build automation tool that solves this by letting you define tasks once in a file called a `Makefile` and run them with a single short command. Instead of remembering and typing a long sequence of commands, you type `make build` or `make run-migrations` and Make handles the rest.

> **In the context of OT-Microservices:** Every service — Employee API (Go), Salary API (Java), Attendance API (Python) — has a `Makefile` with targets for building, testing, running migrations, and more. Commands like `make run-migrations` are used directly in the deployment guide.

---

## 2. What is Make?

**Make** is an open-source **build automation tool** originally designed to manage the compilation of large C and C++ programs. It reads a file called a **Makefile** that defines a set of **targets** (tasks) and the **commands** to execute for each target.

| Attribute | Detail |
|-----------|--------|
| **Full Name** | GNU Make |
| **Developed By** | Stuart Feldman (Bell Labs, 1976); GNU version by Richard Stallman |
| **First Released** | 1976 — one of the oldest developer tools still in active use |
| **License** | GNU General Public License (GPL) |
| **Config File** | `Makefile` (no extension) |
| **Install** | `sudo apt install -y make` (usually pre-installed on Ubuntu) |
| **Version Check** | `make --version` |
| **Platform** | Linux, macOS, Unix (Windows via WSL or MinGW) |

Although Make was originally built for C compilation, it has evolved into a **general-purpose task runner** used across nearly every language and technology stack — Go, Java, Python, JavaScript, Docker, Ansible, and more.

### 2.1 What is a Makefile?

A `Makefile` is a plain text file that contains one or more **rules**. Each rule has three parts:

```makefile
target: dependencies
	command
	command
```

| Part | Meaning |
|------|---------|
| **target** | The name of the task (e.g., `build`, `test`, `clean`) |
| **dependencies** | Other targets that must run first (optional) |
| **command** | One or more shell commands to execute (must be indented with a TAB, not spaces) |

**A simple example:**

```makefile
build:
	go build -o employee-api

test:
	go test ./...

clean:
	rm -f employee-api

run: build
	./employee-api
```

Running `make build` executes `go build -o employee-api`. Running `make run` first runs `build` (its dependency), then runs `./employee-api`.

> ⚠️ **Critical:** Commands in a Makefile **must** be indented with a real **TAB character**, not spaces. Using spaces will cause `make: *** missing separator` errors.

---

## 3. Why Make?

### 3.1 The Problem Without Make

On any project, developers accumulate a set of commands they run repeatedly. Over time these become:

- Long and hard to remember (`poetry run gunicorn --bind 0.0.0.0:8081 app:app`)
- Inconsistent across team members (different flags, different orders)
- Undocumented — new team members have no idea what commands to run
- Error-prone when typed manually under pressure

Without a task runner, the typical solution is a `README.md` that says "run these commands" — but this relies on every person reading it carefully and typing correctly every time.

### 3.2 How Make Solves This

| Problem | Make's Solution |
|---------|----------------|
| Long commands are hard to remember | Wrap them in a named target — `make start` |
| Inconsistency across team members | Everyone runs the same `make` command — same result every time |
| No documentation of tasks | The `Makefile` itself is the documentation |
| Manual multi-step processes | Chain targets with dependencies — `make deploy` runs `build` then `test` then `push` |
| Repeated work | Make tracks file timestamps and skips targets whose outputs are already up to date |

### 3.3 Why Make Over Alternatives?

Several tools exist for task automation. Make remains widely used for specific reasons:

| Tool | Language | Strengths | When to Choose Over Make |
|------|----------|-----------|--------------------------|
| **Make** | Any (shell) | Universal, zero dependencies, pre-installed everywhere | — |
| **Taskfile** | Any (YAML) | Easier syntax than Makefile, cross-platform | When team finds Makefile syntax confusing |
| **Gradle** | Java/Groovy | Deep Java/Android integration | Java-only projects needing complex builds |
| **npm scripts** | JavaScript | Built into Node.js projects | JavaScript/Node.js projects |
| **Invoke** | Python | Pure Python task runner | Python-only projects |
| **Just** | Any | Simpler Makefile alternative | Modern projects preferring cleaner syntax |

Make's key advantage is that it requires **zero installation** on any Linux or macOS machine and is understood by virtually every developer regardless of their primary language. In a polyglot project like OT-Microservices — with Go, Java, Python, and React — Make is the one tool that works uniformly across all of them.

---

## 4. Key Features

### 4.1 Targets as Named Tasks

The most fundamental feature of Make is the ability to give a long, complex command sequence a short, memorable name.

```makefile
# Without Make — developer must remember and type this every time:
# poetry run gunicorn --bind 0.0.0.0:8081 --workers 4 --timeout 30 app:app

# With Make — developer just types: make run-app
run-app:
	poetry run gunicorn --bind 0.0.0.0:8081 --workers 4 --timeout 30 app:app
```

This becomes the shared, agreed-upon way to start the application. No one needs to remember the full command.

### 4.2 Target Dependencies

Targets can declare other targets as dependencies. Make automatically runs dependencies in the correct order before running the target itself.

```makefile
# 'deploy' depends on 'test' which depends on 'build'
# Running 'make deploy' automatically runs: build → test → deploy

build:
	go build -o employee-api

test: build
	go test ./...

deploy: test
	scp employee-api user@server:/opt/apps/
```

This enforces a safe sequence — you cannot accidentally deploy without building and testing first.

### 4.3 Variables

Makefiles support variables to avoid repeating values and make configuration easy to change in one place.

```makefile
# Define variables at the top
APP_NAME    = employee-api
GO_VERSION  = 1.21
BINARY_DIR  = ./bin
PORT        = 8080

# Use variables with $(VARIABLE_NAME)
build:
	go build -o $(BINARY_DIR)/$(APP_NAME)

run:
	$(BINARY_DIR)/$(APP_NAME) --port $(PORT)

docker-build:
	docker build -t $(APP_NAME):latest .
```

Variables can also be overridden from the command line:

```bash
# Override APP_NAME when running make
make build APP_NAME=employee-api-v2
```

### 4.4 Phony Targets

By default, Make checks whether a file with the target's name exists. If a file called `build` exists in the directory, `make build` does nothing — Make thinks the target is already up to date.

The `.PHONY` declaration tells Make that a target is a task name, not a filename, and should always run when called:

```makefile
# Always declare task targets as .PHONY
.PHONY: build test clean run run-migrations docker-build help

build:
	go build -o employee-api

clean:
	rm -rf bin/ *.log
```

Without `.PHONY`, if someone accidentally creates a file called `clean`, the `make clean` command silently does nothing — a very confusing bug.

### 4.5 Environment Variables and Shell Commands

Makefiles can read system environment variables and execute shell commands inline:

```makefile
# Read an environment variable
DB_HOST ?= 127.0.0.1   # Use 127.0.0.1 if DB_HOST is not set

# Execute a shell command and capture its output
GIT_COMMIT := $(shell git rev-parse --short HEAD)
BUILD_DATE := $(shell date +%Y-%m-%d)

build:
	go build \
	  -ldflags "-X main.Version=$(GIT_COMMIT) -X main.BuildDate=$(BUILD_DATE)" \
	  -o employee-api
```

### 4.6 Default Target

The first target in a Makefile is the **default target** — the one that runs when you type `make` with no arguments. A common pattern is to make the default target print a help menu:

```makefile
.PHONY: help build test clean

# Default target — runs when you type just 'make'
help:
	@echo "Available targets:"
	@echo "  make build          - Compile the application"
	@echo "  make test           - Run unit tests"
	@echo "  make run-migrations - Run database migrations"
	@echo "  make clean          - Remove build artifacts"
	@echo "  make docker-build   - Build Docker image"
```

The `@` prefix suppresses the command itself from being printed — only the output is shown.

### 4.7 Silent Mode and Output Control

By default, Make prints each command before running it. You can control this:

```makefile
# @ prefix: suppress printing this specific command
build:
	@echo "Building application..."
	go build -o employee-api         # This line IS printed
	@echo "Build complete."          # The echo itself is NOT printed

# Run make silently (suppress all command output)
# make -s build
```

### 4.8 Conditional Logic

Makefiles support basic conditional logic for handling different environments:

```makefile
# Check if a variable is set
ENV ?= development

run:
ifeq ($(ENV), production)
	GIN_MODE=release ./employee-api
else
	./employee-api
endif
```

### 4.9 Parallel Execution

Make can run independent targets in parallel, speeding up builds with multiple components:

```bash
# Run 'build-go', 'build-java', 'build-python' simultaneously
make -j3 build-go build-java build-python
```

This is particularly useful in CI/CD pipelines where build time matters.

### 4.10 File-Based Dependency Tracking

Make's original purpose was to avoid recompiling files that had not changed. It compares the timestamp of the **target file** against its **source files** — if the source is newer, it recompiles; if not, it skips.

```makefile
# Only recompile employee-api if main.go has changed since last build
employee-api: main.go
	go build -o employee-api
```

While this file-tracking feature is used less in modern polyglot projects (which use `.PHONY` targets instead), it remains valuable for C/C++ compilation and large Go projects with many files.

---

## 5. Make in OT-Microservices

Every service in OT-Microservices has a `Makefile`. Make is the unified interface for building and operating each service — regardless of whether it is written in Go, Java, or Python.

### 5.1 Employee API (Go) — Makefile Targets

```makefile
# ~/employee-api/Makefile (representative targets)

.PHONY: build run-migrations docker-build test clean

build:
	go build -o employee-api

run-migrations:
	# Creates the employee_info table in ScyllaDB
	go run migration/migration.go

test:
	go test ./...

docker-build:
	docker build -t employee-api:latest .

clean:
	rm -f employee-api
```

**Used in deployment:**
```bash
cd ~/employee-api
go mod tidy
go build -o employee-api
make run-migrations        # ← Creates employee_info table in ScyllaDB
```

### 5.2 Attendance API (Python) — Makefile Targets

```makefile
# ~/attendance-api/Makefile (representative targets)

.PHONY: run-migrations install test

install:
	poetry install

run-migrations:
	# Runs Liquibase to create the 'records' table in PostgreSQL
	liquibase --defaultsFile=liquibase.properties update

test:
	poetry run pytest
```

**Used in deployment:**
```bash
cd ~/attendance-api
poetry install
make run-migrations        # ← Creates records table in PostgreSQL via Liquibase
```

### 5.3 Salary API (Java) — Makefile Targets

```makefile
# ~/salary-api/Makefile (representative targets)

.PHONY: build test clean

build:
	mvn clean install -DskipTests

test:
	mvn test

clean:
	mvn clean
```

### 5.4 The Value of Make Across a Polyglot Project

Without Make, a new developer joining OT-Microservices would need to learn:
- `go build` syntax for the Employee API
- `mvn clean install` flags for the Salary API
- `poetry run gunicorn` arguments for the Attendance API
- `liquibase` commands for database migrations
- `npm run build` with environment variables for the Frontend

With Make, every service exposes the same interface:

```bash
make build            # Build this service (works in any service directory)
make test             # Run tests
make run-migrations   # Run database migrations
make clean            # Clean build artifacts
```

The implementation behind each target is different — but the interface is identical. This is Make's greatest value in a polyglot project.

---

## 6. Conclusion

Make is one of the oldest developer tools still in widespread use — and for good reason. Its simplicity, universality, and zero-dependency nature make it the ideal task runner for projects of any size, language, or complexity.

Key takeaways:

- Make reads a **`Makefile`** and executes named **targets** — each target is a named task wrapping one or more shell commands
- **Target dependencies** enforce correct execution order — `make deploy` can automatically run `build` and `test` first
- **Variables** and **environment variables** make Makefiles configurable without editing the file
- Always declare task targets as **`.PHONY`** to prevent conflicts with files of the same name
- Make works with **any language** — Go, Java, Python, JavaScript, shell scripts — making it ideal for polyglot projects
- In OT-Microservices, `make run-migrations` is a critical deployment step used in both the Employee API (ScyllaDB schema) and the Attendance API (PostgreSQL schema via Liquibase)

---

## 7. Contact Information

| Name | Role | Email |
|------|------|-------|
| Deepak | Author | deepak.nagar.snaatak@mygurukulam.co |

---

## 8. References

| Resource | Link |
|----------|------|
| GNU Make Official Documentation | https://www.gnu.org/software/make/manual/ |
| GNU Make Manual (PDF) | https://www.gnu.org/software/make/manual/make.pdf |
| Makefile Tutorial | https://makefiletutorial.com |
| OT-Microservices Employee API | https://github.com/OT-MICROSERVICES/employee-api |
| OT-Microservices Attendance API | https://github.com/OT-MICROSERVICES/attendance-api |
| OT-Microservices Salary API | https://github.com/OT-MICROSERVICES/salary-api |

---

*Author: Deepak | Sprint 0 | Infra-Titans | April 2026*
