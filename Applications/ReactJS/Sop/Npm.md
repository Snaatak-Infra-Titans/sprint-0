# SOP for npm installation - React JS

| Author           | Created on | Version | Last updated by | Last edited on | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer      |
|------------------|------------|---------|-----------------|----------------|--------------|-------------|-------------|------------------|
| Shivam Uniyal    | 15-04-2026 | v1.0    | Shivam Uniyal   | 22-04-2026     | Team         | Anuj Jain   | Prashant    | Piyush Upadhyay  |

---

## Table of Contents

1. Introduction  
2. Purpose  
3. Prerequisites  
4. System Requirements  
5. Software Overview  
6. Step-by-Step Installation  
7. Configuration  
8. Verification & Monitoring  
9. Troubleshooting  
10. FAQs  
11. Contact Information  
12. References  

---

## 1. Introduction

npm (Node Package Manager) is the default package manager for Node.js. It is used to install, manage, and update JavaScript libraries and dependencies required for building applications using React JS.

npm provides access to a large ecosystem of open-source packages and is an essential tool in modern frontend development workflows.

---

## 2. Purpose

The purpose of this SOP is to provide a structured and step-by-step guide for installing npm on Ubuntu and preparing the environment for React JS development.

This document ensures that users can install, verify, and use npm efficiently without errors.

---

## 3. Prerequisites

Before proceeding, ensure the following:

- Ubuntu 24.04 installed  
- Terminal access  
- Internet connectivity  
- Basic knowledge of Linux commands  

---

## 4. System Requirements

| Component | Minimum Requirement |
|----------|-------------------|
| CPU      | Dual Core          |
| RAM      | 4 GB               |
| Disk     | 10 GB free space   |
| OS       | Ubuntu 24.04       |

---

## 5. Software Overview

| Software | Description |
|----------|------------|
| Node.js  | JavaScript runtime required to run npm |
| npm      | Package manager used to install dependencies |

---

## 6. Step-by-Step Installation

### Step 1: Update System Packages

```bash
sudo apt update
```

---

### Step 2: Install Node.js and npm

```bash
sudo apt install nodejs npm -y
```

---

### Step 3: Verify Node.js Installation

```bash
node -v
```

---

### Step 4: Verify npm Installation

```bash
npm -v
```

---

### Step 5: Upgrade npm (Recommended)

```bash
sudo npm install -g npm@latest
```

---

### Step 6: Initialize a Project (Optional)

```bash
mkdir my-react-app
cd my-react-app
npm init -y
```

---

## 7. Configuration

No additional configuration is required for basic npm setup.

However, npm uses a `package.json` file to manage project dependencies. This file is created using:

```bash
npm init -y
```

It stores:
- Project name  
- Version  
- Dependencies  
- Scripts  

---

## 8. Verification & Monitoring

To verify npm is working correctly:

```bash
npm --version
```

Install a sample package:

```bash
npm install lodash
```

Check installed packages:

```bash
npm list
```

Successful installation confirms npm is working correctly.

---

## 9. Troubleshooting

| Issue | Possible Cause | Solution |
|------|---------------|----------|
| npm command not found | Node.js not installed | Install using `sudo apt install nodejs npm` |
| Permission denied | Lack of privileges | Use `sudo` or fix permissions |
| npm outdated | Older version installed | Run `sudo npm install -g npm@latest` |
| Network error | Internet issue | Check connectivity |

---

## 10. FAQs

**Q1. What is npm?**  
npm is a package manager used to install and manage JavaScript libraries.

**Q2. Is npm required for React JS?**  
Yes, npm is required to install React and its dependencies.

**Q3. How to check npm version?**  
```
npm -v
```

**Q4. What is package.json?**  
It is a file that stores project metadata and dependencies.

---

## 11. Contact Information

| Name           | Email ID |
|----------------|----------|
| Shivam Uniyal  | shivam.uniyal.snaatak@mygurukulam.co |

---

## 12. References

| Link | Description |
|------|------------|
| https://nodejs.org | Official Node.js website |
| https://docs.npmjs.com | npm documentation |
