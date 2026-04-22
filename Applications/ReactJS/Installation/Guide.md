#  React JS Installation Guide (Ubuntu 24.04)

Install React JS (Frontend Framework) in a simple and beginner-friendly way

---
| Author | Created on | Version | Last updated by | Last edited on | PRE Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
| ------ | ---------- | ------- | --------------- | -------------- | ------------ | ----------- | ----------- | ----------- |
| Gourav | 16-04-2026 | v1.0    | Gourav          | 16-04-2026     | -            | -           | -           | -           |

---

##  Overview

This guide explains how to install and run React JS using:

* Node.js (Required)
* npm (Node Package Manager)
* Create React App / Vite

---

##  Why React JS?

* Component-based architecture
* Fast performance (Virtual DOM)
* Reusable UI components
* Widely used in frontend development

---

## React Basics

| Component  | Purpose                         |
| ---------- | ------------------------------- |
| Node.js    | Runs JavaScript outside browser |
| npm        | Installs packages               |
| React      | Frontend library                |
| Vite / CRA | Tool to create React apps       |

> Always install **Node.js + npm** before React

---

##  Prerequisites

### Check Ubuntu Version

```bash
lsb_release -a
```

---

### Update System

```bash
sudo apt update && sudo apt upgrade -y
```

---

##  Installation

## Step 1: Install Node.js & npm

```bash
sudo apt install -y nodejs npm
```

---

## Step 2: Verify Installation

```bash
node -v
npm -v
```

---

##  Recommended: Install Latest Node.js (Using NodeSource)

```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs
```

---

## Step 3: Create React App

### Method A: Using Vite (Fast & Recommended)

```bash
npm create vite@latest my-react-app
cd my-react-app
npm install
```

---

### Select Options

* Framework → React
* Variant → JavaScript (or TypeScript)

---

## Step 4: Run React App

```bash
npm run dev
```

 Open browser:

```
http://localhost:5173
```

---

##  Method B: Using Create React App (CRA)

```bash
npx create-react-app my-app
cd my-app
npm start
```

 Open browser:

```
http://localhost:3000
```

---

##  Project Structure (From Your OT-Microservices)

Your React app exists inside:

```
frontend/
```

Key files:

* `package.json` → dependencies
* `public/index.html` → main HTML
* `src/index.js` → entry point
* `src/App.react.js` → main component
* Components:

  * `EmployeeForm.js`
  * `AttendanceList.js`
  * `HomePage.react.js`

 This confirms your project already uses **React frontend**.

---

##  Useful Commands

| Task                 | Command                     |
| -------------------- | --------------------------- |
| Install dependencies | `npm install`               |
| Run project          | `npm run dev` / `npm start` |
| Build project        | `npm run build`             |
| Stop server          | `Ctrl + C`                  |

---

##  Verify Setup

```bash
node -v
npm -v
npm run dev
```

---

##  VS Code Setup

```bash
sudo snap install code --classic
```

### Install Extensions

```bash
code --install-extension dsznajder.es7-react-js-snippets
code --install-extension esbenp.prettier-vscode
```

---

##  Troubleshooting

### npm not found

```bash
sudo apt install npm
```

---

### Permission Issues

```bash
sudo chown -R $USER:$USER ~/.npm
```

---

### Port already in use

```bash
sudo lsof -i :3000
kill -9 <PID>
```

---

##  Quick Commands

| Task            | Command                       |
| --------------- | ----------------------------- |
| Install Node    | `sudo apt install nodejs npm` |
| Create App      | `npm create vite@latest`      |
| Run App         | `npm run dev`                 |
| Install package | `npm install <package>`       |
| Build           | `npm run build`               |

---

## Contact Information

| Name   | Email                                                                             |
| ------ | --------------------------------------------------------------------------------- |
| gourav sharma | [gourav.sharma.snaatak@mygurukulam.co](mailto:gourav.sharma.snaatak@mygurukulam.co) |


---
