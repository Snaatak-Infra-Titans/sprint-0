# Java JDK 21 Installation Guide (Ubuntu 24.04)

> Install Java JDK 21 (LTS) on Ubuntu 24.04 in a simple and beginner-friendly way.

## Introduction

This guide provides a step-by-step approach to installing Java JDK 21 on Ubuntu 24.04. It is designed for beginners as well as developers who want a clean and reliable setup. The document focuses on using Ubuntu’s built-in package manager (APT), which is the simplest and most recommended method for installing Java. By following this guide, you will be able to install Java, configure environment variables, verify the installation, and manage different Java versions if required.

---

## Document Information

| Author          | Created On | Version | L0 Reviewer  | L1 Reviewer  | L2 Reviewer     |
| --------------- | ---------- | ------- | ------------ | ------------ | --------------- |
| Versha Tripathi | 13-04-2026 | v1.0    | Prince Batra | Nikita Joshi | Piyush Upadhyay |

---

## Table of Contents

* [Overview](#overview)
* [Prerequisites](#prerequisites)
* [Installation Methods](#installation-methods)
* [Set JAVA_HOME](#set-java_home)
* [Managing Multiple Java Versions](#managing-multiple-java-versions)
* [Verify Setup](#verify-setup)
* [Common Issues & Fixes](#common-issues--fixes)
* [Quick Command Reference](#quick-command-reference)
* [Conclusion](#conclusion)
* [Contact Information](#contact-information)
* [References](#references)

---

## Overview

Java JDK 21 can be installed on Ubuntu 24.04 using the APT package manager, which is the most straightforward and recommended approach. APT handles dependency management automatically and ensures that you get a stable and well-tested version of OpenJDK directly from Ubuntu repositories. This method is ideal for beginners and for systems where simplicity, stability, and ease of maintenance are important.



---

## Prerequisites

Before installing Java, make sure your system is ready:

* Check Ubuntu version:

  ```bash
  lsb_release -a
  ```
* Update system packages:

  ```bash
  sudo apt update && sudo apt upgrade -y
  ```


---

## Installation Methods



Follow these steps to install Java JDK 21 using APT:

```bash
sudo apt install -y openjdk-21-jdk
```

Verify installation:

```bash
java -version
javac -version
```

---

## Set JAVA_HOME

| Step                           | Command                                               |
| ------------------------------ | ----------------------------------------------------- |
| Find Java path                 | `readlink -f $(which java)`                           |
| Open bashrc                    | `nano ~/.bashrc`                                      |
| Add JAVA_HOME (append to file) | `export JAVA_HOME=/usr/lib/jvm/java-21-openjdk-amd64` |
| Add to PATH (append to file)   | `export PATH=$JAVA_HOME/bin:$PATH`                    |
| Apply changes                  | `source ~/.bashrc`                                    |
| Verify                         | `echo $JAVA_HOME`                                     |

---

## Managing Multiple Java Versions

If multiple Java versions are installed, you can switch between them using the alternatives system.

Install another version (example Java 17):

```bash
sudo apt install -y openjdk-17-jdk
```

Switch Java version:

```bash
sudo update-alternatives --config java
```

Switch compiler version:

```bash
sudo update-alternatives --config javac
```

---

## Verify Setup

* Check Java runtime version:

  ```bash
  java -version
  ```
* Check Java compiler version:

  ```bash
  javac -version
  ```
* Check Java binary location:

  ```bash
  which java
  ```
* Verify JAVA_HOME:

  ```bash
  echo $JAVA_HOME
  ```

---

## Common Issues & Fixes

| Issue                          | Fix                                                        |
| ------------------------------ | ---------------------------------------------------------- |
| `java: command not found`      | `export PATH=/usr/lib/jvm/java-21-openjdk-amd64/bin:$PATH` |
| `javac: command not found`     | `sudo apt install -y openjdk-21-jdk`                       |
| Wrong Java version active      | `sudo update-alternatives --config java`                   |
| `UnsupportedClassVersionError` | `javac --release 17 HelloWorld.java`                       |

---

## Quick Command Reference

| Task                   | Command                                               |
| ---------------------- | ----------------------------------------------------- |
| Install Java 21        | `sudo apt install -y openjdk-21-jdk`                  |
| Check Java version     | `java -version`                                       |
| Check compiler version | `javac -version`                                      |
| Compile a file         | `javac HelloWorld.java`                               |
| Run a program          | `java HelloWorld`                                     |
| Set JAVA_HOME          | `export JAVA_HOME=/usr/lib/jvm/java-21-openjdk-amd64` |
| Switch Java version    | `sudo update-alternatives --config java`              |

---

## Conclusion

Installing Java JDK 21 on Ubuntu 24.04 using APT is the simplest and most efficient approach, especially for beginners. It ensures a stable setup with minimal configuration effort. By properly setting environment variables and verifying the installation, you can quickly start developing Java applications. Managing multiple Java versions is also straightforward using built-in tools, making this setup flexible for different project requirements.

---

## Contact Information

| Name            | Email                                                                                   |
| --------------- | --------------------------------------------------------------------------------------- |
| Versha Tripathi | [versha.tripathi.snaatak@mygurukulam.co](mailto:versha.tripathi.snaatak@mygurukulam.co) |

---

## References

| # | Resource                        | Link                                                                                                                             |
| - | ------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| 1 | Ubuntu 24.04 LTS Release Notes  | [https://ubuntu.com/blog/ubuntu-24-04-lts-noble-numbat-released](https://ubuntu.com/blog/ubuntu-24-04-lts-noble-numbat-released) |
| 2 | OpenJDK 21 Official Site        | [https://openjdk.org/projects/jdk/21](https://openjdk.org/projects/jdk/21)                     
| 3 | Java 21 New Features            | [https://openjdk.org/jeps/0](https://openjdk.org/jeps/0)                                                                         |
| 4 | Ubuntu APT Package Manager Docs | [https://manpages.ubuntu.com/manpages/noble/man8/apt.8.html](https://manpages.ubuntu.com/manpages/noble/man8/apt.8.html)         |

---
