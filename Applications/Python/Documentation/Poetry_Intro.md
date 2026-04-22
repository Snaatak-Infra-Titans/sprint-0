# Poetry — Python Dependency Management & Packaging

---

## Document Information

| Author | Created On | Version | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|--------|------------|---------|-------------|-------------|-------------|
| Versha Tripathi | 13-04-2026 | v1.0 | Prince Batra | Nikita Joshi | Piyush Upadhyay |

---

## Table of Contents

- [What is Poetry?](#what-is-poetry)
- [Why Use Poetry?](#why-use-poetry)
- [Key Features](#key-features)
- [Poetry vs pip vs venv](#poetry-vs-pip-vs-venv)
- [Best Practices](#best-practices)
- [Conclusion](#conclusion)
- [Contact Information](#contact-information)
- [References](#references)

---

## What is Poetry?

Poetry is a modern Python tool designed to simplify dependency management and packaging by providing a unified and structured approach. Instead of relying on multiple configuration files like `requirements.txt`, `setup.py`, and `setup.cfg`, Poetry uses a single file called `pyproject.toml` to manage project configuration, dependencies, and metadata. It also generates a `poetry.lock` file to ensure consistent and reproducible installations across different environments. Additionally, Poetry automatically creates and manages virtual environments for each project, eliminating the need for manual setup and reducing configuration overhead.

---

## Why Use Poetry?

Poetry helps overcome many limitations of traditional Python tooling by introducing a more reliable and maintainable workflow. It ensures proper dependency resolution before installation, preventing version conflicts that commonly occur with `pip`. It produces clean and cross-platform lock files instead of environment-specific outputs like `pip freeze`. Poetry also removes the need to manually create and activate virtual environments and consolidates all configuration into a single file. It simplifies packaging and publishing processes with built-in commands and allows developers to organize dependencies more effectively, especially in team-based or production-grade projects.

---

## Key Features

| Feature | Description |
|---|---|
| Dependency Resolution | Ensures all dependencies are compatible before installation using a SAT solver |
| Unified Config | Uses a single `pyproject.toml` file for configuration and metadata |
| Virtual Env Management | Automatically creates and manages project-specific virtual environments |
| Reproducible Builds | Uses `poetry.lock` to lock exact versions including transitive dependencies |
| Dependency Groups | Supports separation of dependencies like development and testing |
| Built-in Publishing | Provides commands for building and publishing packages without extra tools |
| Python Version Pinning | Allows defining supported Python versions in configuration |
| Script Entrypoints | Enables defining CLI scripts directly in `pyproject.toml` |

---

## Poetry vs pip vs venv

| Feature | pip | venv | Poetry |
|--------|-----|------|--------|
| Purpose | Package installer | Virtual environment manager | Complete dependency management and packaging tool |
| Dependency Management | Basic (no conflict resolution) | Not applicable | Advanced (SAT solver for conflict resolution) |
| Dependency Tracking | requirements.txt (manual) | Not applicable | pyproject.toml + poetry.lock (automatic and structured) |
| Virtual Environment | Not included | Creates and manages environments | Automatically creates and manages environments |
| Reproducible Builds | Limited | Limited | Strong (via poetry.lock) |
| Dev/Prod Dependency Separation | Manual (multiple files) | Not applicable | Built-in dependency groups |
| Ease of Use | Simple | Simple | Moderate learning curve |
| Configuration Management | Multiple files | Not applicable | Single file (pyproject.toml) |
| Packaging Support | Requires setuptools/twine | Not applicable | Built-in packaging and publishing |
| Transitive Dependencies | Not tracked explicitly | Not applicable | Fully tracked |
| Python Version Management | Not enforced | Not enforced | Can be defined in pyproject.toml |
| Best Use Case | Quick installs, small scripts | Isolated environments | Medium to large projects, team collaboration |

---

## Best Practices

| Practice | Description |
|---|---|
| Commit Lock File | Always commit `pyproject.toml` and `poetry.lock` to ensure reproducibility |
| In-Project Virtualenv | Store `.venv` inside the project directory for better portability |
| Separate Dependencies | Keep development dependencies separate from production dependencies |
| Use Poetry Run | Execute commands using `poetry run` instead of manual environment activation |
| Pin Python Version | Define supported Python version explicitly in `pyproject.toml` |
| Regular Updates | Keep dependencies updated and check for outdated packages regularly |
| Validate Configuration | Use validation commands to ensure configuration correctness |

---

## Conclusion

Poetry provides a modern and streamlined approach to managing Python projects by combining dependency management, virtual environment handling, and packaging into a single tool. While traditional tools like `pip` and `venv` are suitable for simpler use cases, Poetry offers a more structured and scalable solution for real-world applications. Its ability to ensure reproducibility, resolve dependency conflicts, and centralize configuration makes it an essential tool for teams and developers working on complex or production-ready Python projects.

---

## Contact Information

| Name | Email |
|---|---|
| Versha Tripathi | [versha.tripathi.snaatak@mygurukulam.co](mailto:versha.tripathi.snaatak@mygurukulam.co) |

---

## References

| # | Resource | Link |
|---|---|---|
| 1 | Official Poetry Documentation | https://python-poetry.org/docs/ |
| 2 | Poetry GitHub Repository | https://github.com/python-poetry/poetry |
| 3 | PEP 517 — Build System Interface | https://peps.python.org/pep-0517/ |
| 4 | PEP 518 — pyproject.toml | https://peps.python.org/pep-0518/ |
| 5 | uv — Ultra-fast Python package manager | https://github.com/astral-sh/uv |

---
