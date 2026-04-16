# NPM Documentation

## Author Table

| **Author**  | **Email**                                                                       |
| ----------- | ------------------------------------------------------------------------------- |
| Saransh Rai | [saransh.rai.snaatak@mygurukulam.co](mailto:saransh.rai.snaatak@mygurukulam.co) |

## 1. Introduction

NPM (Node Package Manager) is the default package manager for Node.js. It allows developers to install, manage, and share reusable JavaScript packages (libraries and tools).

---

## 2. Why NPM?

NPM is widely used in modern development because:

* Simplifies dependency management
* Enables code reuse through packages
* Speeds up development using pre-built libraries
* Provides version control for dependencies
* Supports automation through scripts

---

## 3. What is NPM?

NPM consists of three main components:

### 1. Registry

* A large public database of JavaScript packages
* Developers can publish and share their packages

### 2. CLI (Command Line Interface)

* Tool to interact with NPM
* Used for installing, updating, and managing packages

### 3. package.json

* Configuration file for a project
* Stores metadata and dependencies

Example:

```
{
  "name": "my-app",
  "version": "1.0.0",
  "dependencies": {
    "express": "^4.18.0"
  }
}
```

---

## 4. Key Features of NPM

### 1. Dependency Management

* Install packages easily using:

  ```bash
  npm install <package-name>
  ```
* Automatically resolves dependencies

### 2. Version Control

* Supports semantic versioning (SemVer)
* Ensures compatibility across environments

### 3. Script Automation

* Define scripts in package.json

  ```json
  "scripts": {
    "start": "node app.js",
    "test": "jest"
  }
  ```
* Run using:

  ```bash
  npm run start
  ```

### 4. Package Publishing

* Developers can publish their own packages
* Share reusable code with the community

### 5. Global & Local Installation

* Global:

  ```bash
  npm install -g <package>
  ```
* Local:

  ```bash
  npm install <package>
  ```

### 6. Security & Auditing

* Check vulnerabilities using:

  ```bash
  npm audit
  ```

---

## 5. Use Case of NPM

NPM is commonly used in JavaScript and Node.js projects to install libraries, manage project dependencies, and run development scripts.

Example use cases:

* Installing Express for backend development
* Installing React-related packages for frontend development
* Running scripts like `start`, `build`, and `test`
* Managing project versions and dependency updates

---

## 6. Basic Workflow

1. Initialize the project using `npm init`
2. Install required packages using `npm install`
3. Manage project details in `package.json`
4. Run scripts using `npm run <script>`
5. Update or remove packages when needed

---

## 7. Basic Commands

| Command                      | Description                                 |
| ---------------------------- | ------------------------------------------- |
| npm init                     | Initialize a new project                    |
| npm install                  | Install all dependencies                    |
| npm install <package-name>   | Install a specific package (single library) |
| npm uninstall <package-name> | Remove a package                            |
| npm update                   | Update packages                             |
| npm run <script>             | Run defined scripts                         |

---

## 8. Conclusion

NPM is an essential tool in the JavaScript ecosystem that helps developers manage dependencies, automate workflows, and build scalable applications efficiently.

---
