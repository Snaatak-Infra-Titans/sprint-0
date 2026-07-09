# Poetry Documentation



## Document Information

| Author          | Created On | Version | L0 Reviewer  | L1 Reviewer  | L2 Reviewer     |
| --------------- | ---------- | ------- | ------------ | ------------ | --------------- |
| Versha Tripathi | 13-04-2026 | v1.0    | Prince Batra | Nikita Joshi | Piyush Upadhyay |

---

## Table of Contents

* [What is Poetry?](#what-is-poetry)
* [Why Use Poetry?](#why-use-poetry)
* [Key Features](#key-features)
* [Poetry vs pip](#poetry-vs-pip)
* [What is venv?](#what-is-venv)
* [Best Practices](#best-practices)
* [Conclusion](#conclusion)
* [Contact Information](#contact-information)
* [References](#references)

---

## What is Poetry?

* Modern Python tool for dependency management and packaging
* Uses a single `pyproject.toml` file for configuration, dependencies, and metadata
* Generates `poetry.lock` to ensure consistent and reproducible installations
* Automatically creates and manages virtual environments
* Eliminates need for multiple files like `requirements.txt`, `setup.py`
* Simplifies project setup and dependency handling

---

## Why Use Poetry?

* Resolves dependency conflicts before installation
* Provides reproducible builds using `poetry.lock`
* Removes manual virtual environment setup
* Centralizes all configuration in one file
* Simplifies packaging and publishing workflows
* Supports clean separation of development and production dependencies
* Improves collaboration in team environments

---

## Key Features

| Feature                | Description                                                                    |
| ---------------------- | ------------------------------------------------------------------------------ |
| Dependency Resolution  | Ensures all dependencies are compatible before installation using a SAT solver |
| Unified Config         | Uses a single `pyproject.toml` file for configuration and metadata             |
| Virtual Env Management | Automatically creates and manages project-specific virtual environments        |
| Reproducible Builds    | Uses `poetry.lock` to lock exact versions including transitive dependencies    |
| Dependency Groups      | Supports separation of dependencies like development and testing               |
| Built-in Publishing    | Provides commands for building and publishing packages without extra tools     |
| Python Version Pinning | Allows defining supported Python versions in configuration                     |
| Script Entrypoints     | Enables defining CLI scripts directly in `pyproject.toml`                      |

---

## Poetry vs pip

| Feature                 | pip                                      | Poetry                                            |
| ----------------------- | ---------------------------------------- | ------------------------------------------------- |
| Purpose                 | Package installer                        | Complete dependency management and packaging tool |
| Dependency Management   | Basic (no conflict resolution)           | Advanced (SAT solver for conflict resolution)     |
| Dependency Tracking     | `requirements.txt` (manual)              | `pyproject.toml` + `poetry.lock` (automatic)      |
| Virtual Environment     | Not included                             | Automatically managed                             |
| Reproducible Builds     | Limited                                  | Strong                                            |
| Dev/Prod Separation     | Manual                                   | Built-in                                          |
| Configuration           | Multiple files                           | Single file                                       |
| Packaging               | Requires extra tools (setuptools, twine) | Built-in                                          |
| Transitive Dependencies | Not tracked fully                        | Fully tracked                                     |

---

## What is venv?

* Built-in Python module for creating isolated environments
* Allows different projects to use different dependency versions
* Prevents conflicts between global and project-specific packages
* Creates a separate directory containing Python interpreter and libraries
* Requires manual activation and management
* Works well with `pip` for basic setups
* Lightweight and simple for small projects

---

## Best Practices

| Practice              | Description                                      |
| --------------------- | ------------------------------------------------ |
| Commit Lock File      | Always commit `pyproject.toml` and `poetry.lock` |
| In-Project Virtualenv | Store `.venv` inside project directory           |
| Separate Dependencies | Keep dev and prod dependencies separate          |
| Use Poetry Run        | Use `poetry run` instead of manual activation    |
| Pin Python Version    | Define Python version in `pyproject.toml`        |
| Regular Updates       | Keep dependencies updated                        |
| Validate Config       | Check configuration regularly                    |

---

## Conclusion

Poetry provides a modern and structured approach to Python project management by combining dependency handling, environment management, and packaging into one tool. Compared to `pip`, it offers better reliability, reproducibility, and scalability, making it ideal for real-world and team-based projects.

---

## Contact Information

| Name            | Email                                                                                   |
| --------------- | --------------------------------------------------------------------------------------- |
| Versha Tripathi | [versha.tripathi.snaatak@mygurukulam.co](mailto:versha.tripathi.snaatak@mygurukulam.co) |

---

## References

| # | Resource                               | Link                                                                               |
| - | -------------------------------------- | ---------------------------------------------------------------------------------- |
| 1 | Official Poetry Documentation          | [https://python-poetry.org/docs/](https://python-poetry.org/docs/)                 |
| 2 | Poetry GitHub Repository               | [https://github.com/python-poetry/poetry](https://github.com/python-poetry/poetry) |
| 3 | PEP 517 — Build System Interface       | [https://peps.python.org/pep-0517/](https://peps.python.org/pep-0517/)             |
| 4 | PEP 518 — pyproject.toml               | [https://peps.python.org/pep-0518/](https://peps.python.org/pep-0518/)             |
| 5 | uv — Ultra-fast Python package manager | [https://github.com/astral-sh/uv](https://github.com/astral-sh/uv)                 |
