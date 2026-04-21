# Documentation - requirements.txt (Python)

---

## Author Table

| Author       | Created on | Version | Last updated by | Last edited on | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
| ------------ | ---------- | ------- | --------------- | -------------- | ------------ | ----------- | ----------- | ----------- |
| Mukesh Kharb | 2026-04-15 | 1.0     | Mukesh Kharb    | 2026-04-15     | Team         | Mohit Kumar |Faisal Khan  | Mahesh Kumar|            

---

## Table of Contents

* [Introduction](#introduction)
* [Why requirements.txt](#why-requirementstxt)
* [Use Cases](#use-cases)
* [Structure & Examples](#structure--examples)
* [Versioning Explained](#versioning-explained)
* [Workflow](#workflow)
* [Real Project Example](#real-project-example)
* [Best Practices](#best-practices)
* [Commands](#commands)
* [Troubleshooting](#troubleshooting)
* [References](#references)

---

<a id="introduction"></a>

## Introduction

In Python development, projects often depend on external libraries to perform specific tasks. For example, libraries like `Beautiful Soup` are not included in Python by default and must be installed separately.

As projects grow, the number of such dependencies increases, making manual installation time-consuming and error-prone.

To solve this problem, Python uses a `requirements.txt` file. This file contains a list of all the packages and libraries required for a project, allowing them to be installed in a single command.

It ensures:

* Consistent environments across systems
* Faster project setup
* Easier collaboration among developers

---

<a id="why-requirementstxt"></a>

## Why requirements.txt

> [!NOTE]
> Focus: reproducibility, setup speed, deployment reliability, and environment consistency.

### Key Benefits

* **Reproducibility:** Ensures that all developers and environments use the exact same dependency versions, eliminating "it works on my machine" issues.

* **Ease of Setup:** Allows installation of all required libraries using a single command instead of installing them individually.

* **Deployment Support:** Cloud platforms and tools such as Heroku, Docker, and AWS Elastic Beanstalk rely on this file to automatically install dependencies during deployment.

* **Consistency:** Maintains a clean, well-defined environment and serves as documentation of all project dependencies.

---

<a id="use-cases"></a>

## Use Cases

### 1. Developer Onboarding

When a new developer joins a project, setting up the environment manually can be complex and error-prone.

With `requirements.txt`, the setup becomes straightforward:

```bash
pip install -r requirements.txt
```

Outcome:

* Eliminates manual installation steps
* Ensures all developers use identical versions
* Reduces onboarding time significantly

---

### 2. CI/CD Pipelines

In automated pipelines, dependencies must be installed consistently for build and testing stages.

Typical flow:

```text
Code Commit → Build Trigger → Install Dependencies → Run Tests → Deploy
```

Use of `requirements.txt` ensures:

* Reproducible builds
* Stable test execution
* No dependency-related pipeline failures

---

### 3. Production Deployment

In production environments, stability is critical. Installing incorrect versions can break applications.

Using `requirements.txt`:

* Guarantees tested versions are deployed
* Prevents runtime failures
* Ensures environment parity between staging and production

Example:

```bash
pip install -r requirements.txt
```

---

### 4. Microservices Architecture

In microservices-based systems, each service may have its own dependencies.

`requirements.txt` helps:

* Maintain isolated dependency sets per service
* Avoid conflicts between services
* Simplify independent deployments

---

### 5. Team Collaboration

When multiple developers work on the same project, dependency mismatches can lead to inconsistent behavior.

With `requirements.txt`:

* All contributors follow the same dependency structure
* Bugs due to version mismatch are minimized
* Code sharing becomes seamless

---

<a id="structure--examples"></a>

## Structure & Examples

Below is an example of a `requirements.txt` file demonstrating various supported formats:

```groovy
# ===============================
# BASIC DEPENDENCIES
# ===============================
pytest
pytest-cov
beautifulsoup4

# ===============================
# VERSION PINNING
# ===============================
docopt == 0.6.1
requests[security] >= 2.8.1, == 2.8.* ; python_version < "2.7"

# ===============================
# INSTALL FROM URL (REMOTE PACKAGE)
# ===============================
urllib3 @ https://github.com/urllib3/urllib3/archive/refs/tags/1.26.8.zip

# ===============================
# INCLUDE OTHER FILES
# ===============================
-r other-requirements.txt
-c constraints.txt

# ===============================
# LOCAL FILE INSTALLATION
# ===============================
./downloads/numpy-1.9.2-cp34-none-win32.whl

# ===============================
# DIRECT URL INSTALL
# ===============================
http://wxpython.org/Phoenix/snapshot-builds/wxPython_Phoenix-3.0.3.dev1820+49a8884-cp34-none-win_amd64.whl
```

### Explanation

#### 1. Basic Dependencies

* These are simple package names without version constraints
* Installed using latest compatible version
* Example:

  ```
  pytest
  beautifulsoup4
  ```
* Use Case: Quick setup in development environments

---

#### 2. Version Pinning

* Defines exact or conditional versions
* Prevents unexpected upgrades
* Example:

  ```
  docopt == 0.6.1
  requests[security] >= 2.8.1, == 2.8.*
  ```
* Use Case: Production environments where stability is critical

---

#### 3. Install from URL

* Installs packages directly from remote repositories or archives
* Example:

  ```
  urllib3 @ https://github.com/urllib3/urllib3/archive/refs/tags/1.26.8.zip
  ```
* Use Case: When package is not available on PyPI or using custom builds

---

#### 4. Include Other Requirement Files (-r)

* Allows splitting dependencies into multiple files
* Example:

  ```
  -r other-requirements.txt
  ```
* Use Case: Large projects (base, dev, prod separation)

---

#### 5. Constraints File (-c)

* Restricts versions without forcing installation
* Example:

  ```
  -c constraints.txt
  ```
* Use Case: Controlling dependency versions globally

---

#### 6. Local File Installation

* Installs packages from local system
* Example:

  ```
  ./downloads/numpy.whl
  ```
* Use Case: Offline environments or pre-built binaries

---

#### 7. Direct URL Installation

* Installs package from hosted file URL
* Example:

  ```
  http://example.com/package.whl
  ```
---

<a id="versioning-explained"></a>

## Versioning Explained

| Symbol | Meaning         |
| ------ | --------------- |
| ==     | Exact version   |
| >=     | Minimum version |
| <=     | Maximum version |
| !=     | Exclude version |

### Example

```
flask>=2.0,<3.0
```

✔ Allows safe upgrades
❌ Blocks breaking versions

---
<a id="workflow"></a>
## Workflow
### End-to-End Dependency Workflow

> <img width="600" height="auto" alt="Untitled design" src="https://github.com/user-attachments/assets/8d45d21a-c02b-4228-b456-dc255867c233" />

---
<a id="real-project-example"></a>
## Real Project Example (Flask Microservice)

### Project Structure

```text
app/
 ├── app.py
 ├── requirements.txt
 └── config.py
```

### requirements.txt

```txt
# Core Web Framework
flask==2.3.2

# Database
psycopg2-binary==2.9.9

# Caching
redis==4.5.0

# API Docs
flasgger==0.9.7

# Monitoring
prometheus-flask-exporter==0.22.0
```

### Installation Flow

```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

### Execution

```bash
python app.py
```
---

<a id="best-practices"></a>

## Best Practices

### Dependency Management

* Always pin exact versions for production (`==`)
* Use version ranges (`>=,<`) only in development
* Avoid unversioned dependencies

### Environment Management

* Always use virtual environments (`venv`)
* Do not install dependencies globally

### File Organization

* Maintain separate files:

  * `requirements.txt` (production)
  * `requirements-dev.txt` (development tools)

### Security Practices

* Regularly audit dependencies for vulnerabilities
* Avoid installing from untrusted sources

### CI/CD Integration

* Always install dependencies using requirements.txt in pipeline
* Never rely on pre-installed packages

### Maintenance

* Remove unused dependencies
* Periodically update and test versions

---

## Commands

### Installation

```bash
pip install -r requirements.txt
```

Installs all dependencies listed in the file.

---

### Generate requirements.txt

```bash
pip freeze > requirements.txt
```

Exports currently installed packages with versions.

---

### List Installed Packages

```bash
pip list
```

Displays all installed packages and versions.

---

### Remove Package

```bash
pip uninstall <package>
```

Removes a specific dependency.

---

### Upgrade Package

```bash
pip install --upgrade <package>
```

Upgrades package to latest version.

---

## Troubleshooting

> [!WARNING]
> Most issues stem from environment mismatch or incorrect version constraints—validate your venv and pinned versions first.

| Issue                           | Possible Cause              | Detailed Explanation                                       | Solution                                                |
| ------------------------------- | --------------------------- | ---------------------------------------------------------- | ------------------------------------------------------- |
| ModuleNotFoundError             | Missing dependency          | Package not listed or not installed in environment         | Run `pip install -r requirements.txt`                   |
| Version Conflict                | Incompatible versions       | Two packages require different versions of same dependency | Adjust version constraints manually                     |
| Works locally but not in server | Environment mismatch        | Different dependency versions across environments          | Use exact version pinning (`==`)                        |
| pip install fails               | Network or repository issue | Unable to fetch packages from PyPI                         | Check internet / use mirror                             |
| Permission denied               | No sudo / virtual env issue | Installing globally without permissions                    | Use virtual environment                                 |
| Broken dependencies             | Interrupted installation    | Incomplete install state                                   | Run `pip install --force-reinstall -r requirements.txt` |
| Import errors after install     | Wrong Python environment    | Using system Python instead of venv                        | Activate correct environment                            |

---

## References

* [https://www.freecodecamp.org/news/python-requirementstxt-explained/](https://www.freecodecamp.org/news/python-requirementstxt-explained/)
* [https://pip.pypa.io/en/stable/reference/requirements-file-format/](https://pip.pypa.io/en/stable/reference/requirements-file-format/)
* [https://medium.com/@agusmahari/what-is-requirements-txt-and-why-is-it-important-for-python-a4535523e2e9](https://medium.com/@agusmahari/what-is-requirements-txt-and-why-is-it-important-for-python-a4535523e2e9)

---

## Summary

* `requirements.txt` is a critical component in Python projects that ensures all dependencies are explicitly defined and consistently managed across different environments.

* It eliminates common issues such as *"it works on my machine"* by enforcing reproducibility through version-controlled dependencies.

* The file simplifies project setup by allowing developers to install all required libraries using a single command, significantly reducing onboarding time.

* It plays a key role in DevOps workflows, as CI/CD pipelines rely on it to install dependencies during automated builds and deployments.

* Proper versioning strategies (`==`, `>=`, ranges) help control dependency behavior, prevent breaking changes, and maintain application stability.

* Advanced syntax (such as including other files, installing from URLs, and editable installs) enables flexibility for complex and large-scale projects.

* Using `requirements.txt` promotes better collaboration by ensuring all team members work with the same dependency structure.

* It supports production-grade practices such as environment isolation, dependency auditing, and controlled upgrades.

* In modern architectures like microservices, each service maintains its own `requirements.txt`, ensuring independence and avoiding cross-service conflicts.

* Overall, `requirements.txt` serves as both a **technical tool** and a **documentation artifact**, capturing the exact dependency state required to run an application reliably.

---
