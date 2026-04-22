# Common Stack | Applications | Java | Installation via Bash Script

---

## Author Table

| **Author** | **Created on** | **Version** | **Last updated by** | **Last Edited On** | **Pre Reviewer** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ---------- | -------------- | ----------- | ------------------- | ------------------ | ---------------- | --------------- | --------------- | --------------- |
| Ankita     | 17-04-2026     | v1.0        | Ankita              | 22-04-2026         | Team             | Komal Jaiswal   | Akshit Kapil    | Mahesh Kumar    |

---

## Table of Contents

1. [Introduction](#introduction)
2. [Purpose](#purpose)
3. [Why Use Bash Script for Installation](#why-use-bash-script-for-installation)
4. [Prerequisites](#prerequisites)
5. [Java Installation via Bash Script](#java-installation-via-bash-script)
6. [Script Explanation](#script-explanation)
7. [Verification](#verification)
8. [Use Cases](#use-cases)
9. [Best Practices](#best-practices)
10. [Contact Information](#contact-information)
11. [References](#references)

---

## Introduction

Java is a widely used, platform-independent programming language used for building web, enterprise, and cloud applications.

Installing Java manually on multiple systems can be repetitive and error-prone. Using a Bash script simplifies this process by automating installation steps.

---

## Purpose

This document explains how to install Java on Ubuntu using a Bash script. It helps automate the installation process, ensuring consistency and reducing manual effort.

---

## Why Use Bash Script for Installation

Using a Bash script provides several advantages:

* Automation of repetitive tasks
* Consistent installation across systems
* Faster setup in DevOps environments
* Easy integration with CI/CD pipelines

---

## Prerequisites

* Ubuntu 20.04 / 22.04 / 24.04
* sudo privileges
* Internet access

---

## Java Installation via Bash Script

Create a script file:

```bash
nano install-java.sh
```

Add the following content:

```bash
#!/bin/bash

# Update system packages
sudo apt update -y

# Install Java (OpenJDK)
sudo apt install openjdk-17-jdk -y

# Set JAVA_HOME
JAVA_PATH=$(readlink -f /usr/bin/java | sed "s:/bin/java::")
echo "export JAVA_HOME=$JAVA_PATH" >> ~/.bashrc

echo "export PATH=\$JAVA_HOME/bin:\$PATH" >> ~/.bashrc

# Reload environment
source ~/.bashrc

# Verify installation
java -version
```

Make the script executable:

```bash
chmod +x install-java.sh
```

Run the script:

```bash
./install-java.sh
```

---

## Script Explanation

* `apt update` → Updates package list
* `apt install openjdk-17-jdk` → Installs Java Development Kit
* `JAVA_HOME` → Sets environment variable
* `PATH` → Ensures Java commands are accessible
* `java -version` → Verifies installation

---

## Verification

Check Java version:

```bash
java -version
```

Check JAVA_HOME:

```bash
echo $JAVA_HOME
```

Expected Result:

* Java version should be displayed
* JAVA_HOME should point to Java installation directory

---

## Use Cases

* Automated server setup
* CI/CD pipeline initialization
* Cloud instance provisioning
* DevOps environment standardization

---

## Best Practices

* Use LTS versions of Java (e.g., Java 17)
* Keep system updated before installation
* Use scripts for repeatable setups
* Store scripts in version control

---

## Contact Information

| Name   | Email                                                                             |
| ------ | --------------------------------------------------------------------------------- |
| Ankita | [ankita.singh.snaatak@mygurukulam.co](mailto:ankita.singh.snaatak@mygurukulam.co) |

---

## References

| Topic             | Link                                                                                 |
| ----------------- | ------------------------------------------------------------------------------------ |
| OpenJDK Docs      | [https://openjdk.org/](https://openjdk.org/)                                         |
| Ubuntu Java Guide | [https://ubuntu.com/tutorials/install-jre](https://ubuntu.com/tutorials/install-jre) |
