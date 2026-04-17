# Poetry — Python Dependency Management & Packaging

---

## Document Information

| Author | Created On | Version | Last Updated By | Last Edited On | PRE Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|---|---|---|---|---|---|---|---|---|
| Versha Tripathi | 13-04-2026 | v1.0 | Versha Tripathi | 13-04-2026 | Team | - | - | - |

---

## Table of Contents

- [What is Poetry?](#what-is-poetry)
- [Why Use Poetry?](#why-use-poetry)
- [Key Features](#key-features)
- [System Requirements](#system-requirements)
- [Installation (Ubuntu 24.04)](#installation-ubuntu-2404)
- [Getting Started](#getting-started)
- [Version Constraints](#version-constraints)
- [Common Commands](#common-commands)
- [Poetry vs pip vs venv](#poetry-vs-pip-vs-venv)
- [When to Use What](#when-to-use-what)
- [Dependency Groups](#dependency-groups)
- [When NOT to Use Poetry](#when-not-to-use-poetry)
- [Best Practices](#best-practices)
- [Contact Information](#contact-information)
- [References](#references)

---

## What is Poetry?

Poetry is a modern Python tool for **dependency management** and **packaging**, using `pyproject.toml` as the single source of truth.

| File | Purpose |
|---|---|
| `pyproject.toml` | Single config file (replaces `setup.py`, `requirements.txt`) |
| `poetry.lock` | Deterministic lock file for reproducible installs |
| `.venv/` | Auto-managed virtual environment |

---

## Why Use Poetry?

| Problem (Old Way) | Solution (Poetry) |
|---|---|
| No dependency resolution in `requirements.txt` | SAT solver for conflict-free resolution |
| `pip freeze` produces bloated, OS-specific locks | Clean, cross-platform `poetry.lock` |
| Manual `venv` creation and activation | Auto-creates and manages virtualenvs |
| Separate `setup.py` / `setup.cfg` for packaging | Single `pyproject.toml` handles everything |
| No dev/prod dependency distinction | Native dependency groups |
| Publishing requires `twine` + `setuptools` | `poetry publish` handles it all |

---

## Key Features

| Feature | Description |
|---|---|
| Dependency Resolution | SAT solver ensures all packages are compatible before installing |
| Unified Config | Everything in one `pyproject.toml` (PEP 517/518) |
| Virtual Env Management | Auto-creates a dedicated venv per project |
| Reproducible Builds | `poetry.lock` captures exact versions including transitive deps |
| Dependency Groups | Separate `main`, `dev`, `test`, `docs` dependencies cleanly |
| Built-in Publishing | `poetry build` + `poetry publish` — no `twine` needed |
| Python Version Pinning | Enforce supported Python versions via `pyproject.toml` |
| Script Entrypoints | Define CLI scripts directly in `pyproject.toml` |

---

## System Requirements

| Requirement | Details |
|---|---|
| OS | Ubuntu 24.04 LTS (Noble Numbat) |
| Python | 3.12 (ships with Ubuntu 24.04) |
| curl | Pre-installed on Ubuntu 24.04 |

---

## Installation (Ubuntu 24.04)

| Step | Command |
|---|---|
| 1. Ensure Python 3.12 is available | `python3 --version` |
| 2. Install Poetry via official installer | `curl -sSL https://install.python-poetry.org \| python3 -` |
| 3. Add Poetry to PATH | `echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc && source ~/.bashrc` |
| 4. Verify installation | `poetry --version` |

> **Do not install Poetry via `pip install poetry`** — always use the official installer above.

---

## Getting Started

| Task | Command |
|---|---|
| Create new project | `poetry new my-project` |
| Init in existing project | `poetry init` |
| Add production dependency | `poetry add requests` |
| Add dev dependency | `poetry add pytest --group dev` |
| Add with version constraint | `poetry add "django>=4.2,<5.0"` |
| Add from Git | `poetry add git+https://github.com/user/repo.git` |
| Install all dependencies | `poetry install` |
| Install only production | `poetry install --only main` |
| Run a command in venv | `poetry run python script.py` |
| Activate venv shell | `poetry shell` |

---

## Version Constraints

| Operator | Meaning | Example |
|---|---|---|
| `^1.2.3` | Compatible release (`>=1.2.3, <2.0.0`) | `^1.4` allows `1.4.x` to `1.x.x` |
| `~1.2.3` | Patch-level only (`>=1.2.3, <1.3.0`) | `~1.2` allows `1.2.x` only |
| `>=1.2.3` | Greater than or equal to | Explicit lower bound |
| `*` | Any version | No constraint |
| `1.2.3` | Exact version | Pins exactly |

---

## Common Commands

| Category | Command | Description |
|---|---|---|
| **Dependencies** | `poetry add <pkg>` | Add a dependency |
| | `poetry add <pkg> --group dev` | Add to a group |
| | `poetry remove <pkg>` | Remove a dependency |
| | `poetry update` | Update all dependencies |
| | `poetry update <pkg>` | Update a specific package |
| | `poetry show` | List installed packages |
| | `poetry show --tree` | Show dependency tree |
| | `poetry show --outdated` | Show outdated packages |
| **Environment** | `poetry install` | Install from `pyproject.toml` + lock file |
| | `poetry shell` | Activate venv shell |
| | `poetry run <cmd>` | Run command in venv |
| | `poetry env info` | Show venv info |
| | `poetry env list` | List all venvs for project |
| | `poetry env remove <python>` | Remove a venv |
| **Build & Publish** | `poetry build` | Build sdist and wheel |
| | `poetry publish` | Publish to PyPI |
| | `poetry publish --repository testpypi` | Publish to TestPyPI |
| | `poetry publish --dry-run` | Test without publishing |
| **Lock File** | `poetry lock` | Regenerate lock file |
| | `poetry lock --no-update` | Refresh without updating versions |
| **Config** | `poetry config --list` | Show all configuration |
| | `poetry config virtualenvs.in-project true` | Store `.venv` inside project |
| **Versioning** | `poetry version patch` | `0.1.0 → 0.1.1` |
| | `poetry version minor` | `0.1.0 → 0.2.0` |
| | `poetry version major` | `0.1.0 → 1.0.0` |
| **Misc** | `poetry check` | Validate `pyproject.toml` |

---

## Poetry vs pip vs venv

| Feature | `pip` + `venv` | `pip` + `requirements.txt` | Poetry |
|---|:---:|:---:|:---:|
| Virtual environment management | Manual | Manual | ✅ Automatic |
| Dependency conflict detection | ❌ | ❌ | ✅ SAT solver |
| Lock file (reproducible installs) | ❌ | ⚠️ Partial | ✅ `poetry.lock` |
| Separate dev/prod dependencies | ❌ | ⚠️ Multiple files | ✅ Groups |
| Single config file | ❌ | ❌ | ✅ `pyproject.toml` |
| Build & publish packages | ❌ | ❌ | ✅ Built-in |
| Transitive dependency tracking | ❌ | ❌ | ✅ |
| PEP 517/518 compliant | ⚠️ | ⚠️ | ✅ |
| Learning curve | Low | Low | Medium |
| Speed | Fast | Fast | Slower (resolver) |

---

## When to Use What

| Scenario | Recommended Tool |
|---|---|
| Quick scripts / one-off experiments | `pip` + `venv` |
| Learning Python basics | `pip` + `venv` |
| Simple projects with few dependencies | `pip` + `venv` |
| Team projects needing reproducibility | **Poetry** |
| Projects published to PyPI | **Poetry** |
| Complex dependency graphs | **Poetry** |
| CI/CD pipelines needing deterministic builds | **Poetry** |
| Monorepos / multi-package setups | Consider `uv` or `hatch` |

---

## Dependency Groups

| Command | Effect |
|---|---|
| `poetry install` | Install everything |
| `poetry install --only main` | Production deps only |
| `poetry install --with docs,test` | Main + specific groups |
| `poetry install --without dev` | Exclude specific groups |

---

## When NOT to Use Poetry

| Scenario | Preferred Alternative |
|---|---|
| System-level scripts / small utilities | `pip` + `venv` |
| Conda-based data science environments | `conda` + `conda-lock` |
| Very large monorepos | `uv` or `hatch` |
| Teams heavily invested in `pip-tools` | `pip-compile` + `pip-sync` |
| Docker-only deployments with simple deps | `requirements.txt` |

---

## Best Practices

| Practice | Command / Note |
|---|---|
| Always commit lock file (for apps) | `git add pyproject.toml poetry.lock` |
| Store venv inside project | `poetry config virtualenvs.in-project true` |
| Keep prod installs lean | `poetry add pytest --group dev` |
| Use `poetry run` in scripts | `poetry run pytest` |
| Pin Python version explicitly | `python = "^3.12"` in `pyproject.toml` (Ubuntu 24.04 ships Python 3.12) |
| Regularly update deps | `poetry update && poetry show --outdated` |
| Validate config | `poetry check` |

---

## Contact Information

| Name | Email |
|---|---|
| Versha Tripathi | [versha.tripathi.snaatak@mygurukulam.co](mailto:versha.tripathi.snaatak@mygurukulam.co) |

---

## References

| # | Resource | Link |
|---|---|---|
| 1 | Official Poetry Documentation | [python-poetry.org/docs](https://python-poetry.org/docs/) |
| 2 | Poetry GitHub Repository | [github.com/python-poetry/poetry](https://github.com/python-poetry/poetry) |
| 3 | PEP 517 — Build System Interface | [peps.python.org/pep-0517](https://peps.python.org/pep-0517/) |
| 4 | PEP 518 — pyproject.toml | [peps.python.org/pep-0518](https://peps.python.org/pep-0518/) |
| 5 | uv — Ultra-fast Python package manager | [github.com/astral-sh/uv](https://github.com/astral-sh/uv) |
