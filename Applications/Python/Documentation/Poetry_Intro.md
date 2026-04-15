#  Poetry — Python Dependency Management & Packaging

> **"Poetry helps you declare, manage and install dependencies of Python projects, ensuring you have the right stack everywhere."**

---

##  Table of Contents

- [What is Poetry?](#what-is-poetry)
- [Why Use Poetry?](#why-use-poetry)
- [Key Features](#key-features)
- [Installation](#installation)
- [Getting Started](#getting-started)
- [Core Concepts](#core-concepts)
- [Common Commands](#common-commands)
- [Poetry vs pip vs venv](#poetry-vs-pip-vs-venv)
- [pyproject.toml Deep Dive](#pyprojecttoml-deep-dive)
- [poetry.lock File](#poetrylock-file)
- [Dependency Groups](#dependency-groups)
- [Publishing Packages](#publishing-packages)
- [Best Practices](#best-practices)
- [When NOT to Use Poetry](#when-not-to-use-poetry)

---

## What is Poetry?

**Poetry** is a modern Python tool for **dependency management** and **packaging**. It was created by Sébastien Eustace in 2018 and is designed to replace the fragmented ecosystem of `pip`, `setuptools`, `twine`, `venv`, and `requirements.txt` with a single, cohesive tool.

Poetry treats project configuration as a first-class citizen, using the standardized `pyproject.toml` file (PEP 517/518) as the single source of truth for your project.

```
Your Project
    └── pyproject.toml         ← single config file (replaces setup.py, requirements.txt, etc.)
    └── poetry.lock            ← deterministic lock file for reproducible installs
    └── .venv/                 ← auto-managed virtual environment
```

---

## Why Use Poetry?

Before Poetry, a typical Python project required juggling multiple tools and files:

| Problem (Old Way) | Solution (Poetry) |
|---|---|
| `requirements.txt` has no dependency resolution | Poetry uses a SAT solver for conflict-free resolution |
| `pip freeze` produces bloated, OS-specific locks | `poetry.lock` is clean, cross-platform, and human-readable |
| Manual `venv` creation and activation | Poetry auto-creates and manages virtualenvs |
| Separate `setup.py` / `setup.cfg` for packaging | Single `pyproject.toml` handles everything |
| No distinction between dev/prod deps | Native dependency groups (`[dev]`, `[test]`, etc.) |
| Publishing requires `twine` + `setuptools` separately | `poetry publish` handles it all in one command |

---

## Key Features

### 1.  Deterministic Dependency Resolution
Poetry uses a **dependency resolver** that ensures all packages are compatible with each other before installing. It prevents the classic "works on my machine" problem.

```bash
poetry add requests          # Resolves and locks the entire dependency graph
```

### 2.  Unified `pyproject.toml`
Everything lives in one file — metadata, dependencies, scripts, build config — following the PEP 517/518 standard.

### 3.  Automatic Virtual Environment Management
Poetry creates and manages a dedicated virtual environment per project automatically. No more `python -m venv .venv && source .venv/bin/activate`.

### 4.  Reproducible Builds with `poetry.lock`
The lock file captures the exact version of every package (including transitive dependencies), guaranteeing identical installs across all machines and CI environments.

### 5.  Dependency Groups
Cleanly separate production, development, test, and documentation dependencies:

```toml
[tool.poetry.dependencies]
requests = "^2.31.0"

[tool.poetry.group.dev.dependencies]
pytest = "^7.4"
black = "^23.0"
```

### 6.  Built-in Publishing
Build and publish packages to PyPI (or a private registry) without needing `twine` or `setuptools`:

```bash
poetry build
poetry publish
```

### 7.  Python Version Management
Specify which Python versions your project supports and Poetry will enforce it:

```toml
[tool.poetry.dependencies]
python = "^3.9"
```

### 8.  Script Entrypoints
Define CLI scripts directly in `pyproject.toml`:

```toml
[tool.poetry.scripts]
my-cli = "mypackage.cli:main"
```

---

## Installation

Poetry should be installed **outside** any virtual environment, using the official installer:

```bash
# macOS / Linux / WSL
curl -sSL https://install.python-poetry.org | python3 -

# Windows (PowerShell)
(Invoke-WebRequest -Uri https://install.python-poetry.org -UseBasicParsing).Content | python -
```

Verify installation:

```bash
poetry --version
# Poetry (version 1.8.x)
```

>  **Do not install Poetry via `pip install poetry`** inside a project's virtualenv. It should be a globally available tool.

---

## Getting Started

### Create a New Project

```bash
poetry new my-project
```

This generates:

```
my-project/
├── pyproject.toml
├── README.md
├── my_project/
│   └── __init__.py
└── tests/
    └── __init__.py
```

### Initialize Poetry in an Existing Project

```bash
cd existing-project
poetry init       # Interactive wizard to generate pyproject.toml
```

### Add Dependencies

```bash
poetry add requests                  # Add a production dependency
poetry add pytest --group dev        # Add a dev dependency
poetry add "django>=4.2,<5.0"        # Add with version constraints
poetry add git+https://github.com/user/repo.git  # Add from Git
```

### Install All Dependencies

```bash
poetry install                       # Install all deps (including dev)
poetry install --only main           # Install only production deps
```

### Run Commands Inside the Virtual Environment

```bash
poetry run python script.py
poetry run pytest
poetry shell                         # Spawn a shell inside the virtualenv
```

---

## Core Concepts

### Version Constraints

Poetry uses semantic versioning with intuitive constraint operators:

| Operator | Meaning | Example |
|---|---|---|
| `^1.2.3` | Compatible release (>=1.2.3, <2.0.0) | `^1.4` allows 1.4.x to 1.x.x |
| `~1.2.3` | Patch-level updates only (>=1.2.3, <1.3.0) | `~1.2` allows 1.2.x only |
| `>=1.2.3` | Greater than or equal to | Explicit lower bound |
| `*` | Any version | No constraint |
| `1.2.3` | Exact version | Pins exactly |

---

## Common Commands

```bash
# Dependency management
poetry add <package>                 # Add a dependency
poetry add <package> --group dev     # Add to a group
poetry remove <package>              # Remove a dependency
poetry update                        # Update all dependencies
poetry update <package>              # Update a specific package
poetry show                          # List installed packages
poetry show --tree                   # Show dependency tree

# Environment management
poetry install                       # Install from pyproject.toml + lock file
poetry shell                         # Activate virtual environment shell
poetry run <command>                 # Run command in virtual environment
poetry env info                      # Show virtualenv info
poetry env list                      # List all virtualenvs for this project
poetry env remove <python>           # Remove a virtualenv

# Build & Publish
poetry build                         # Build sdist and wheel
poetry publish                       # Publish to PyPI
poetry publish --repository testpypi # Publish to TestPyPI

# Lock file
poetry lock                          # Regenerate lock file without installing
poetry lock --no-update              # Refresh lock without updating versions

# Config
poetry config --list                 # Show all configuration
poetry config virtualenvs.in-project true   # Store .venv inside project folder
```

---

## Poetry vs pip vs venv

This is the most important comparison for understanding why Poetry exists.

### Feature Comparison

| Feature | `pip` + `venv` | `pip` + `requirements.txt` | **Poetry** |
|---|:---:|:---:|:---:|
| Virtual environment management | Manual | Manual | ✅ Automatic |
| Dependency resolution (conflict detection) | ❌ None | ❌ None | ✅ SAT solver |
| Lock file (reproducible installs) | ❌ | ⚠️ Partial (`pip freeze`) | ✅ `poetry.lock` |
| Separate dev/prod dependencies | ❌ | ⚠️ Multiple files | ✅ Groups |
| Single config file | ❌ | ❌ | ✅ `pyproject.toml` |
| Build & publish packages | ❌ Needs setuptools/twine | ❌ Needs setuptools/twine | ✅ Built-in |
| Transitive dependency tracking | ❌ | ❌ | ✅ |
| PEP 517/518 compliant | ⚠️ | ⚠️ | ✅ |
| Learning curve | Low | Low | Medium |
| Speed | Fast | Fast | Slower (resolver) |

---

### `pip` + `venv` — The Traditional Way

```bash
# Setup
python -m venv .venv
source .venv/bin/activate         # (Linux/macOS)
.venv\Scripts\activate            # (Windows)

# Install packages
pip install requests
pip install pytest

# Save dependencies (flat, no resolution)
pip freeze > requirements.txt

# Reproduce
pip install -r requirements.txt
```

**Problems:**
- `pip freeze` captures ALL packages (including transitive ones) with OS-specific versions
- No conflict detection — pip will install incompatible packages without warning
- No distinction between runtime and dev dependencies (unless you maintain multiple files)
- No packaging support built in
- Forgetting to activate the venv is a constant footgun

---

### `pip` — What It Is and What It Lacks

`pip` is Python's **package installer** — nothing more. It fetches packages from PyPI and installs them. It does NOT:
- Manage virtual environments
- Resolve dependency conflicts
- Lock transitive dependencies reliably
- Handle packaging/publishing

`pip` is a low-level building block. Tools like Poetry build on top of it.

---

### `venv` — What It Is and What It Lacks

`venv` is Python's **virtual environment creator**. It isolates your project's packages from the system Python. It does NOT:
- Know anything about your project's dependencies
- Track what you've installed
- Resolve conflicts
- Reproduce environments reliably across machines

---

### Poetry — The Unified Approach

```bash
# Setup (one command)
poetry new my-project
cd my-project

# Add dependencies (auto-resolves + locks)
poetry add requests
poetry add pytest --group dev

# Reproduce exactly (anywhere, any machine)
poetry install
```

Poetry wraps pip and venv into a coherent workflow, adds a proper resolver, and extends it with packaging capabilities.

---

### When to Use What

| Scenario | Recommended Tool |
|---|---|
| Quick script or one-off experiments | `pip` + `venv` |
| Learning Python basics | `pip` + `venv` |
| Simple projects with few dependencies | `pip` + `venv` |
| Team projects needing reproducibility | **Poetry** |
| Projects that will be published to PyPI | **Poetry** |
| Complex dependency graphs | **Poetry** |
| CI/CD pipelines needing deterministic builds | **Poetry** |
| Monorepos / multi-package setups | Consider `uv` or `hatch` |

---

## `pyproject.toml` Deep Dive

```toml
[tool.poetry]
name = "my-awesome-app"
version = "0.1.0"
description = "A brief description of the project"
authors = ["Jane Doe <jane@example.com>"]
license = "MIT"
readme = "README.md"
homepage = "https://example.com"
repository = "https://github.com/jane/my-awesome-app"
keywords = ["python", "example"]
classifiers = [
    "Programming Language :: Python :: 3",
    "License :: OSI Approved :: MIT License",
]

# Python version requirement
[tool.poetry.dependencies]
python = "^3.10"
requests = "^2.31.0"
pydantic = "^2.5.0"
sqlalchemy = { version = "^2.0", extras = ["asyncio"] }

# Optional dependencies (extras)
[tool.poetry.extras]
database = ["sqlalchemy"]

# Development dependencies
[tool.poetry.group.dev.dependencies]
pytest = "^7.4"
black = "^23.0"
ruff = "^0.1.0"
mypy = "^1.7"

# Documentation dependencies
[tool.poetry.group.docs.dependencies]
mkdocs = "^1.5"

# CLI scripts
[tool.poetry.scripts]
my-cli = "my_awesome_app.cli:main"

# Build system (required)
[build-system]
requires = ["poetry-core"]
build-backend = "poetry.core.masonry.api"
```

---

## `poetry.lock` File

The lock file is **auto-generated** by Poetry and should **always be committed to version control** (for applications). It records:

- The exact resolved version of every package
- Hashes for integrity verification
- The full dependency graph including transitive dependencies

```toml
# Example excerpt from poetry.lock
[[package]]
name = "requests"
version = "2.31.0"
description = "Python HTTP for Humans."
optional = false
python-versions = ">=3.7"
files = [
    {file = "requests-2.31.0-py3-none-any.whl", hash = "sha256:..."},
    {file = "requests-2.31.0.tar.gz", hash = "sha256:..."},
]

[package.dependencies]
certifi = ">=2017.4.17"
charset-normalizer = ">=2,<4"
idna = ">=2.5,<4"
urllib3 = ">=1.21.1,<3"
```

>  **Rule of thumb:** Commit `poetry.lock` for **applications** (ensures reproducibility). For **libraries**, you may optionally omit it so users get the freshest compatible versions.

---

## Dependency Groups

Groups let you organize dependencies by purpose and install only what's needed:

```bash
# Install everything
poetry install

# Install only production deps (exclude all groups)
poetry install --only main

# Install main + specific groups
poetry install --with docs,test

# Exclude specific groups
poetry install --without dev
```

```toml
[tool.poetry.group.test.dependencies]
pytest = "^7.4"
pytest-cov = "^4.1"
factory-boy = "^3.3"

[tool.poetry.group.lint.dependencies]
ruff = "^0.1"
mypy = "^1.7"
black = "^23.0"
```

---

## Publishing Packages

```bash
# 1. Configure PyPI credentials (one-time)
poetry config pypi-token.pypi your-api-token

# 2. Update version
poetry version patch        # 0.1.0 → 0.1.1
poetry version minor        # 0.1.0 → 0.2.0
poetry version major        # 0.1.0 → 1.0.0

# 3. Build distributions
poetry build
# Creates: dist/my-package-0.1.1.tar.gz
#          dist/my-package-0.1.1-py3-none-any.whl

# 4. Publish
poetry publish              # Publish to PyPI
poetry publish --dry-run    # Test without actually publishing
```

---

## Best Practices

```bash
#  Always commit poetry.lock (for apps)
git add pyproject.toml poetry.lock

#  Store virtualenv inside the project for Docker/CI clarity
poetry config virtualenvs.in-project true

#  Use dependency groups to keep production installs lean
poetry add pytest --group dev

#  Use `poetry run` in scripts instead of activating manually
poetry run pytest
poetry run python manage.py migrate

#  Pin Python version explicitly
# In pyproject.toml:
# python = "^3.11"

#  Regularly update dependencies
poetry update
poetry show --outdated

#  Use `poetry check` to validate pyproject.toml
poetry check
```

---

## When NOT to Use Poetry

Poetry is powerful but not always the right tool:

- **System-level scripts / small utilities**: `pip` + `venv` is simpler and sufficient
- **Conda-based data science environments**: Use `conda` + `conda-lock` instead
- **Very large monorepos**: Consider `uv` (faster resolver) or `hatch`
- **Teams heavily invested in `pip-tools`**: `pip-compile` + `pip-sync` may be adequate
- **Docker-only deployments with simple deps**: `requirements.txt` might be cleaner

---

## Quick Reference

```bash
poetry new <name>             # New project
poetry init                   # Init in existing project
poetry add <pkg>              # Add dependency
poetry add <pkg> --group dev  # Add dev dependency
poetry remove <pkg>           # Remove dependency
poetry install                # Install all dependencies
poetry update                 # Update dependencies
poetry show --tree            # Dependency tree
poetry run <cmd>              # Run in virtualenv
poetry shell                  # Activate virtualenv shell
poetry build                  # Build package
poetry publish                # Publish to PyPI
poetry env info               # Virtualenv info
poetry check                  # Validate pyproject.toml
poetry version <rule>         # Bump version (patch/minor/major)
```

---

## Further Reading

-  [Official Poetry Documentation](https://python-poetry.org/docs/)
-  [Poetry GitHub Repository](https://github.com/python-poetry/poetry)
-  [PEP 517 — Build System Interface](https://peps.python.org/pep-0517/)
-  [PEP 518 — pyproject.toml](https://peps.python.org/pep-0518/)
-  [uv — Ultra-fast Python package manager](https://github.com/astral-sh/uv) *(modern alternative)*

---

*Documentation generated for Poetry v1.8.x | Python 3.9+*
