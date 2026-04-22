# SOP for npm installation - React JS

| Author           | Created on | Version | Last updated by | Last edited on | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer      |
|------------------|------------|---------|-----------------|----------------|--------------|-------------|-------------|------------------|
| Shivam Uniyal    | 15-04-2026 | v1.0    | Shivam Uniyal   | 22-04-2026     | Team         | Anuj Jain   | Prashant    | Piyush Upadhyay  |

---

## Table of Contents

1. [Introduction](#1-introduction)  
2. [Purpose](#2-purpose)  
3. [Prerequisites](#3-prerequisites)  
4. [System Requirements](#4-system-requirements)  
5. [Software Overview](#5-software-overview)  
6. [Step-by-Step Installation](#6-step-by-step-installation)  
7. [Verification & Monitoring](#7-verification--monitoring)  
8. [Troubleshooting](#8-troubleshooting)  
9. [FAQs](#9-faqs)  
10. [Conclusion](#10-conclusion)  
11. [Contact Information](#11-contact-information)  
12. [References](#12-references)

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
<img width="1114" height="266" alt="Screenshot 2026-04-22 at 8 01 31 PM" src="https://github.com/user-attachments/assets/95b1d137-ce73-48d3-a832-f8ac3a2daea9" />

---

### Step 3: Verify Node.js Installation

```bash
node -v
```
<img width="912" height="96" alt="Screenshot" src="https://github.com/user-attachments/assets/cfa243e2-03ec-4884-a590-d17eca5b4ffe" />

---

### Step 4: Verify npm Installation

```bash
npm -v
```
<img width="912" height="96" alt="Screenshot 2026-04-22 at 8 07 40 PM" src="https://github.com/user-attachments/assets/28f78ee4-e209-47c3-abad-16fa617d226a" />

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

## 7. Verification & Monitoring

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

## 8. Troubleshooting

| Issue | Possible Cause | Solution |
|------|---------------|----------|
| npm command not found | Node.js not installed | Install using `sudo apt install nodejs npm` |
| Permission denied | Lack of privileges | Use `sudo` or fix permissions |
| npm outdated | Older version installed | Run `sudo npm install -g npm@latest` |
| Network error | Internet issue | Check connectivity |

---

## 9. FAQs

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

## 10. Conclusion

This SOP provides a clear and structured approach to installing and using npm for React JS development. Following these steps ensures a smooth setup and helps manage project dependencies efficiently.

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
