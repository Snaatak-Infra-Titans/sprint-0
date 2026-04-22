# Common Stack | Applications | Java | Installation via Bash Script

---

## Author Table

| **Author** | **Created on** | **Version** | **Last updated by** | **Last Edited On** | **Pre Reviewer** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ---------- | -------------- | ----------- | ------------------- | ------------------ | ---------------- | --------------- | --------------- | --------------- |
| Ankita     | 17-04-2026     | v1.0        | Ankita              | 22-04-2026         | Team             | Komal Jaiswal   | Akshit Kapil    | Mahesh Kumar    |

---

## Table of Contents

1. Introduction
2. Purpose
3. Why Use Bash Script for Installation
4. Prerequisites
5. Java Installation via Bash Script
6. Script Explanation
7. Verification
8. Troubleshooting (JAVA_HOME Not Set)
9. Use Cases
10. Best Practices
11. Contact Information
12. References

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
<img width="1786" height="1179" alt="image" src="https://github.com/user-attachments/assets/935d34ed-6a26-4778-801b-f4d9f2a20c64" />

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
<img width="936" height="189" alt="image" src="https://github.com/user-attachments/assets/daf49860-da46-4900-b00a-067b114e6dc1" />

Check JAVA_HOME:

```bash
echo $JAVA_HOME
```
<img width="936" height="167" alt="image" src="https://github.com/user-attachments/assets/5cb1a3f4-a952-4404-b6fd-517ed3d66386" />

Expected Result:

* Java version should be displayed
* JAVA_HOME should point to Java installation directory

---

## Troubleshooting (JAVA_HOME Not Set)

If the expected result is NOT achieved, follow the steps below to manually find and set `JAVA_HOME`.
<img width="936" height="167" alt="image" src="https://github.com/user-attachments/assets/010b6f65-063d-4f66-9f6e-50e59c683197" />

### Step 1: Find Java Path

```bash
readlink -f $(which java)
```

### Step 2: Set JAVA_HOME Manually

```bash
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
export PATH=$JAVA_HOME/bin:$PATH
```

### Step 3: Verify

```bash
echo $JAVA_HOME
```
<img width="876" height="255" alt="image" src="https://github.com/user-attachments/assets/bf4152f9-c357-4110-ad3f-1709a34b7c2f" />

### Recommended Best Practice (Dynamic Method)

Instead of hardcoding the path, use:

```bash
export JAVA_HOME=$(dirname $(dirname $(readlink -f $(which java))))
echo $JAVA_HOME
```
<img width="876" height="189" alt="image" src="https://github.com/user-attachments/assets/ba08b18f-95a4-4ce3-85cc-54daddaff037" />

This method automatically detects the correct Java installation path.

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
* Prefer dynamic JAVA_HOME detection instead of hardcoding paths

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
