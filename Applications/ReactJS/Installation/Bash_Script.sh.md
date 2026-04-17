# ReactJS Documentation

<p align="center">
  <img width="120" src="https://upload.wikimedia.org/wikipedia/commons/a/a7/React-icon.svg" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Tool-ReactJS-blue?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Category-Frontend-green?style=for-the-badge" />
  <img src="https://img.shields.io/badge/DevOps-Automation-orange?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Architecture-Reference--Example-purple?style=for-the-badge" />
</p>

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
* [How to Run Scripts](#how-to-run-scripts)
* [Important Notes](#important-notes)
* [Best Practices](#best-practices)
* [Common Errors](#common-errors)
* [FAQs](#faqs)
* [Conclusion](#conclusion)
* [Contact Information](#contact-information)
* [References](#references)

---

<a id="introduction"></a>

## Introduction

ReactJS is a popular JavaScript library used to build modern, interactive user interfaces. It enables developers to create **Single Page Applications (SPA)** where the UI dynamically updates without reloading the page.

From a DevOps perspective, a React application is treated differently from backend services. It is:

* Built into static files
* Deployed as frontend assets
* Served via web servers like Nginx

In this document, we will focus on **React setup, execution, and upgrade lifecycle**, using OT-Microservices only as a reference example where needed.

---

<a id="understanding-react-setup"></a>

## Understanding React Setup

A React application requires the following components:

* **Node.js** → Runtime environment to execute JavaScript outside browser
* **npm (Node Package Manager)** → Used to install and manage dependencies
* **package.json** → Contains project metadata and dependency definitions
* **node_modules/** → Stores installed dependencies

When you run a React project, npm installs all required libraries defined in `package.json`.

---

<a id="architecture"></a>

## Architecture

A generic React project structure looks like this:

```
frontend/
 ├── package.json
 ├── node_modules/
 ├── public/
 ├── src/
 └── build/   (generated)
```

### Key Concepts

* React follows a **component-based architecture**
* UI is divided into reusable components
* Data flows using props and state
* Build process converts source code into optimized static files

### Example (OT-Micro Reference)

In OT-Microservices:

* React frontend communicates with multiple APIs
* Uses relative paths like `/api/v1/...`
* Nginx routes requests to backend services

---

<a id="workflow"></a>

## Workflow

### Development Workflow

1. Install Node.js and npm
2. Run `npm install`
3. Start development server using `npm start`
4. Access application in browser

### Production Workflow

1. Install dependencies
2. Build application using `npm run build`
3. Deploy static files
4. Serve using Nginx or similar web server

---

<a id="react-installation-script"></a>

## React Installation Script

This script installs dependencies and runs the application.

```bash
#!/bin/bash

echo "▶ Updating system"
sudo apt update && sudo apt upgrade -y

echo "▶ Installing Node.js"
curl -fsSL https://deb.nodesource.com/setup_16.x | sudo -E bash -
sudo apt install -y nodejs

echo "▶ Verifying installation"
node -v
npm -v

echo "▶ Navigating to project"
cd OT-Micro/frontend || exit

echo "▶ Installing dependencies"
npm install

echo "▶ Starting React app"
npm start
```

---

<a id="react-upgrade-script"></a>

## React Upgrade Script

This script updates dependencies and rebuilds the application.

```bash
#!/bin/bash

echo "▶ Pulling latest code"
git pull origin main

echo "▶ Navigating to project"
cd OT-Micro/frontend || exit

echo "▶ Installing updated dependencies"
npm install

echo "▶ Backup current build"
mv build build_backup_$(date +%F_%T) 2>/dev/null

echo "▶ Building new version"
npm run build

echo "▶ Reloading Nginx"
sudo systemctl reload nginx

echo "✅ Upgrade completed"
```

---

<a id="how-to-run-scripts"></a>

## How to Run Scripts

```bash
chmod +x script.sh
./script.sh
```

---

<a id="important-notes"></a>

## Important Notes

* Always run scripts from project root
* Ensure Node.js is installed before execution
* Do not manually modify node_modules
* Always test after build or upgrade

---

<a id="best-practices"></a>

## Best Practices

* Use `.env` files for configuration
* Avoid hardcoding API URLs
* Use consistent Node.js version
* Maintain clean dependency versions
* Integrate with CI/CD pipelines

---

<a id="common-errors"></a>

## Common Errors

| Error               | Cause               | Solution                        |
| ------------------- | ------------------- | ------------------------------- |
| npm not found       | Node missing        | Install Node.js                 |
| build fails         | dependency conflict | Delete node_modules & reinstall |
| blank UI            | incorrect build     | rebuild project                 |
| port already in use | conflict            | kill process                    |

---

<a id="faqs"></a>

## FAQs

### 1. What is ReactJS?

ReactJS is a JavaScript library used for building user interfaces, especially single-page applications where UI updates dynamically.

---

### 2. What is npm and why is it important?

npm is the package manager that installs all required dependencies for the React application.

---

### 3. What does `npm install` do?

It reads the `package.json` file and installs all required dependencies into `node_modules`.

---

### 4. What is the difference between `npm start` and `npm run build`?

* `npm start` runs development server
* `npm run build` creates optimized production files

---

### 5. Why do we need Node.js for React?

Node.js is required to run build tools and manage dependencies during development.

---

### 6. What is the build folder?

It contains optimized static files (HTML, CSS, JS) used for production deployment.

---

### 7. Why should we not edit node_modules?

Because it is auto-generated and managed by npm. Manual changes can break dependencies.

---

### 8. How do upgrades work in React?

Upgrades involve updating dependencies and rebuilding the application.

---

### 9. What happens if build fails?

Usually due to dependency conflicts or code issues. Fix errors and rebuild.

---

<a id="conclusion"></a>

## Conclusion

React applications are built once and deployed as static assets. Proper setup and upgrade practices ensure consistency, reliability, and smooth deployments in any environment.

---

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
