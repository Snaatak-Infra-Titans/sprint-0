<p align="center">
  <img width="360" height="140" alt="image" src="https://github.com/user-attachments/assets/1fdb1672-143e-4330-91f6-47d374993813" />
  <br/>
</p>


<h1 align="center">Common Stack | Applications | Node.js | NPM Documentation</h1>

<p align="center">

---

## Author Table

| **Author**  | **Created on** | **Version** | **Last updated by** | **Last Edited On** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ----------- | -------------- | ----------- | ------------------- | ------------------ | --------------- | --------------- | --------------- |
| Saransh Rai | 19-04-2026     | 1.1         | Saransh Rai         | 19-04-2026         |  Anuj Jain      | Prashant Sharma | Piyush Upadhyay |

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [Purpose](#2-purpose)
3. [What is NPM](#3-what-is-npm)
4. [Why NPM](#4-why-npm)
5. [Key Features](#5-key-features)
6. [Workflow](#6-workflow)
7. [Commands](#7-commands)
8. [Use Cases](#8-use-cases)
9. [Conclusion](#9-conclusion)
10. [References](#10-references)

---

## 1. Introduction

NPM (Node Package Manager) is the default package manager for Node.js. It allows developers to install, manage, and share reusable JavaScript packages (libraries and tools).

---

## 2. Purpose

This document explains:

* What NPM is
* Why it is used
* Key features and workflow
* Common commands and use cases

---

## 3. What is NPM

NPM consists of three main components:

### Registry

* A large public database of JavaScript packages
* Developers can publish and share their packages

### CLI (Command Line Interface)

* Tool to interact with NPM
* Used for installing, updating, and managing packages

### package.json

* Configuration file for a project
* Stores metadata and dependencies

### Example package.json

```json
{
  "name": "my-app",
  "version": "1.0.0",
  "dependencies": {
    "express": "^4.18.0"
  }
}
```

---

## 4. Why NPM

* Simplifies dependency management
* Enables code reuse through packages
* Speeds up development using pre-built libraries
* Provides version control for dependencies
* Supports automation through scripts

---

## 5. Key Features

### 1. Dependency Management

```bash
npm install <package-name>
```

Automatically resolves dependencies.

### 2. Version Control

* Supports semantic versioning (SemVer)
* Ensures compatibility across environments

### 3. Script Automation

```json
"scripts": {
  "start": "node app.js",
  "test": "jest"
}
```

Run scripts:

```bash
npm run start
```

### 4. Package Publishing

* Publish and share reusable packages

### 5. Global & Local Installation

```bash
npm install -g <package>
npm install <package>
```

### 6. Security & Auditing

```bash
npm audit
```

---

## 6. Workflow

1. Initialize the project using `npm init`
2. Install required packages using `npm install`
3. Manage dependencies in `package.json`
4. Run scripts using `npm run <script>`
5. Update or remove packages when needed

---

## 7. Commands

| **Command**                  | **Description**            |
| ---------------------------- | -------------------------- |
| npm init                     | Initialize a new project   |
| npm install                  | Install all dependencies   |
| npm install <package-name>   | Install a specific package |
| npm uninstall <package-name> | Remove a package           |
| npm update                   | Update packages            |
| npm run <script>             | Run defined scripts        |

---

## 8. Use Cases

| **Use Case**          | **Description**                             |
| --------------------- | ------------------------------------------- |
| Backend Development   | Install Express and other backend libraries |
| Frontend Development  | Install React and related packages          |
| Script Automation     | Run build, test, and start scripts          |
| Dependency Management | Manage and update project dependencies      |

---

## 9. Conclusion

NPM plays a critical role in the JavaScript ecosystem by enabling efficient dependency management, automation of development workflows, and easy reuse of code through packages. It helps developers build scalable and maintainable applications while ensuring consistency across different environments.

---

## 10. References

| **Topic**                  | **Link**                                                 |
| -------------------------- | -------------------------------------------------------- |
| NPM Official Documentation | [https://docs.npmjs.com/](https://docs.npmjs.com/)       |
| Node.js Documentation      | [https://nodejs.org/en/docs](https://nodejs.org/en/docs) |
