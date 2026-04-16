# ReactJS Documentation

<p align="center">
  <img width="120" src="https://upload.wikimedia.org/wikipedia/commons/a/a7/React-icon.svg" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Tool-ReactJS-blue?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Category-Frontend-green?style=for-the-badge" />
  <img src="https://img.shields.io/badge/DevOps-Automation-orange?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Architecture-OT--Microservices-purple?style=for-the-badge" />
</p>

---

| Author       | Created on | Version | Last updated by | Last edited on | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
| ------------ | ---------- | ------- | --------------- | -------------- | ------------ | ----------- | ----------- | ----------- |
| Mukesh Kharb | 2026-04-16 | 1.0     | Mukesh Kharb    | 2026-04-16     | Team         |             |             |             |

---

## Table of Contents

* [Introduction](#introduction)
* [Understanding React Setup](#understanding-react-setup)
* [Architecture](#architecture)
* [Workflow](#workflow)
* [React Installation Script](#react-installation-script)
* [React Upgrade Script](#react-upgrade-script)
* [Important Notes](#important-notes)
* [Best Practices](#best-practices)
* [FAQs](#faqs)
* [Conclusion](#conclusion)
* [Contact Information](#contact-information)
* [References](#references)

---

<a id="introduction"></a>

## Introduction

Setting up React applications manually again and again can become repetitive and error-prone, especially when working in a microservices environment where multiple frontend applications exist.

To simplify this, we use Bash scripts to automate the process. These scripts help in creating applications, managing versions, and ensuring that every developer follows the same setup process.

This document explains everything in a simple and practical way so that even beginners can understand and use it.

---

<a id="understanding-react-setup"></a>

## Understanding React Setup

A React application needs a few basic things to run properly:

* Node.js (runtime to execute JavaScript outside browser)
* npm (package manager to install libraries)
* React and ReactDOM (core libraries)

Instead of setting everything manually, we use tools like `create-react-app` which quickly prepares a working project.

---

<a id="architecture"></a>

## Architecture

In OT-Microservices, frontend applications are structured like this:

```
OT-Microservices/
 ├── frontend/
 │    ├── attendance-ui/
 │    ├── dashboard-ui/
 │    └── admin-ui/
```

Each folder is a separate React application. This means:

* Each app runs independently
* Each app can have its own React version
* Changes in one app do not affect others

---

<a id="workflow"></a>

## Workflow

1. Developer runs the installation script
2. Script creates a new React application
3. Required React version is installed
4. Developer starts working on the app
5. If needed, upgrade script is used later

---

<a id="react-installation-script"></a>

## React Installation Script

This script creates a new React application and installs a specific React version.

```bash
#!/bin/bash

APP_NAME=$1
REACT_VERSION=$2
BASE_DIR="$(pwd)/frontend"

if [ -z "$APP_NAME" ] || [ -z "$REACT_VERSION" ]; then
  echo "Usage: ./install.sh <app-name> <react-version>"
  exit 1
fi

mkdir -p "$BASE_DIR"
cd "$BASE_DIR"

npx create-react-app "$APP_NAME"
cd "$APP_NAME"

npm install react@$REACT_VERSION react-dom@$REACT_VERSION

echo "React app created with version $REACT_VERSION"
```

---

<a id="react-upgrade-script"></a>

## React Upgrade Script

This script is used when you already have a React project and want to change its version.

```bash
#!/bin/bash

APP_NAME=$1
REACT_VERSION=$2
BASE_DIR="$(pwd)/frontend"

if [ -z "$APP_NAME" ] || [ -z "$REACT_VERSION" ]; then
  echo "Usage: ./upgrade.sh <app-name> <react-version>"
  exit 1
fi

cd "$BASE_DIR/$APP_NAME"

npm install react@$REACT_VERSION react-dom@$REACT_VERSION

echo "React version updated to $REACT_VERSION"
```

---

<a id="how-to-run-scripts"></a>

## How to Run Scripts

Follow these steps to execute the Bash scripts correctly:

### Step 1: Create Script File

Create a file for installation or upgrade:

```bash
touch install.sh
```

Paste the installation script into this file.

---

### Step 2: Give Execute Permission

```bash
chmod +x install.sh
```

This makes the script executable.

---

### Step 3: Run the Script

```bash
./install.sh attendance-ui 18.2.0
```

This will:

* Create a new React app
* Install React version 18.2.0

---

### Running Upgrade Script

```bash
chmod +x upgrade.sh
./upgrade.sh attendance-ui 17.0.2
```

This will update the existing project to the given version.

---
<a id="important-notes"></a>

> [!IMPORTANT]
> - Always run scripts from the root directory of your project to ensure correct folder creation.
> - Make sure Node.js and npm are installed before running the scripts.
> - Do not run the installation script multiple times with the same app name unless the folder is removed.
> - Always specify the correct React version to avoid unexpected behavior.
> - Ensure you have an active internet connection during execution.
> - Avoid manually modifying node_modules as it can break dependency management.

---

## Key Points to Understand

* The script takes input from the user (app name and version)
* `npx` runs tools without installing them globally
* `create-react-app` creates the project structure
* `npm install` installs required versions of React
* Each project keeps its own dependencies

These points are important to understand how automation is working behind the scenes.

---

<a id="common-errors"></a>

## Common During Script Execution

| Error Message                | Reason                                  | Solution                                             |
| ---------------------------- | --------------------------------------- | ---------------------------------------------------- |
| Permission denied            | Script does not have execute permission | Run `chmod +x script.sh`                             |
| command not found: npx       | Node.js is not installed or not in PATH | Install Node.js and restart terminal                 |
| npm: command not found       | npm is missing                          | Install Node.js (npm comes with it)                  |
| create-react-app not working | Network issue or npm registry problem   | Check internet connection and retry                  |
| Folder already exists        | App directory already present           | Remove folder or use different app name              |
| Cannot cd into directory     | Incorrect path or app not created       | Verify folder structure and rerun script             |
| Version not changing         | Cached dependencies or lock file        | Delete node_modules and package-lock.json, reinstall |

---

<a id="best-practices"></a>

## Best Practices

* Always use exact React versions (avoid using ^ symbol)
* Keep Node version consistent using .nvmrc
* Do not modify node_modules manually
* Test application after upgrading React

---

<a id="faqs"></a>

## FAQs

**Q: What is npx?**
>A: npx is a tool that allows you to run Node packages without installing them globally. It keeps your system clean.

**Q: What is create-react-app?**
>A: It is a tool that sets up a complete React project with all necessary configuration.

**Q: What is npm install doing?**
>A: It downloads and installs libraries (like React) into your project.

**Q: Why do we install react and react-dom together?**
>A: React handles logic and UI, while react-dom is responsible for rendering it in the browser.

**Q: Can different apps use different React versions?**
>A: Yes, each project has its own dependencies.

**Q: What happens if I run script again?**
>A: It may overwrite or fail depending on folder state, so always check before running.

---

<a id="conclusion"></a>

## Conclusion

Using simple Bash scripts makes React setup fast, consistent, and easy to manage. It removes manual effort and helps maintain uniformity across multiple frontend applications.

---

<a id="contact-information"></a>

## Contact Information

| Name         | Email                                                                             |
| ------------ | --------------------------------------------------------------------------------- |
| Mukesh Kharb | [mukesh.Kharb.snaatak@mygurukulam.co](mailto:mukesh.Kharb.snaatak@mygurukulam.co) |

---

<a id="references"></a>

## References

* [https://react.dev](https://react.dev)
* [https://vitejs.dev](https://vitejs.dev)
* [https://nodejs.org](https://nodejs.org)

---
