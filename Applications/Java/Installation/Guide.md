# Java JDK 21 Installation Guide (Ubuntu 24.04)

> Install Java JDK 21 (LTS) on Ubuntu 24.04 in a simple and beginner-friendly way.

---

## Document Information

| Author | Created On | Version | Last Updated By | Last Edited On | PRE Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|---|---|---|---|---|---|---|---|---|
| Versha Tripathi | 13-04-2026 | v1.0 | Versha Tripathi | 13-04-2026 | Team | - | - | - |

---

## Table of Contents

- [Overview](#overview)
- [Why Java 21?](#why-java-21)
- [Java Basics](#java-basics)
- [Prerequisites](#prerequisites)
- [Installation Methods](#installation-methods)
  - [Method A: APT (Recommended)](#method-a-apt-recommended)
  - [Method B: Eclipse Temurin](#method-b-eclipse-temurin)
  - [Method C: SDKMAN](#method-c-sdkman)
- [Set JAVA_HOME](#set-java_home)
- [Managing Multiple Java Versions](#managing-multiple-java-versions)
- [Verify Setup](#verify-setup)
- [First Java Program](#first-java-program)
- [IDE Setup](#ide-setup)
- [Common Issues & Fixes](#common-issues--fixes)
- [Quick Command Reference](#quick-command-reference)
- [Contact Information](#contact-information)
- [References](#references)

---

## Overview

| Installation Method | Description | Recommended For |
|---|---|---|
| APT | Ubuntu's built-in package manager | Beginners, quick setup |
| Eclipse Temurin | Official OpenJDK build by Adoptium | Production environments |
| SDKMAN | Version manager for multiple SDKs | Managing multiple Java versions |

---

## Why Java 21?

| Reason | Detail |
|---|---|
| LTS Release | Long-Term Support — stable and production-ready |
| Security Support | Updates guaranteed until **2031** |
| Virtual Threads | Lightweight concurrency (Project Loom) |
| Pattern Matching | Cleaner `instanceof` and `switch` expressions |
| Records | Concise immutable data classes |

---

## Java Basics

| Component | Purpose |
|---|---|
| JVM | Runs compiled Java programs |
| JRE | JVM + standard libraries |
| JDK | JRE + compiler + development tools |

> Always install the **JDK** for development.

---

## Prerequisites

| Step | Command |
|---|---|
| Check Ubuntu version | `lsb_release -a` |
| Check system architecture | `uname -m` |
| Check disk space | `df -h /` |
| Check available memory | `free -h` |
| Update system packages | `sudo apt update && sudo apt upgrade -y` |

---

## Installation Methods

### Method A: APT (Recommended)

| Step | Command |
|---|---|
| Install JDK 21 | `sudo apt install -y openjdk-21-jdk` |
| Verify Java | `java -version` |
| Verify compiler | `javac -version` |

---

### Method B: Eclipse Temurin

| Step | Command |
|---|---|
| Install dependencies | `sudo apt install -y wget apt-transport-https gpg` |
| Add GPG key | `wget -qO - https://packages.adoptium.net/artifactory/api/gpg/key/public \| gpg --dearmor \| sudo tee /etc/apt/trusted.gpg.d/adoptium.gpg > /dev/null` |
| Add repository | `echo "deb https://packages.adoptium.net/artifactory/deb noble main" \| sudo tee /etc/apt/sources.list.d/adoptium.list` |
| Update package list | `sudo apt update` |
| Install Temurin 21 | `sudo apt install -y temurin-21-jdk` |
| Verify | `java -version` |

---

### Method C: SDKMAN

| Step | Command |
|---|---|
| Install SDKMAN | `curl -s "https://get.sdkman.io" \| bash` |
| Initialise SDKMAN | `source "$HOME/.sdkman/bin/sdkman-init.sh"` |
| List available Java versions | `sdk list java` |
| Install Java 21 | `sdk install java 21.0.3-tem` |
| Set as default | `sdk default java 21.0.3-tem` |
| Verify | `java -version` |

---

## Set JAVA_HOME

| Step | Command |
|---|---|
| Find Java path | `readlink -f $(which java)` |
| Open bashrc | `nano ~/.bashrc` |
| Add JAVA_HOME (append to file) | `export JAVA_HOME=/usr/lib/jvm/java-21-openjdk-amd64` |
| Add to PATH (append to file) | `export PATH=$JAVA_HOME/bin:$PATH` |
| Apply changes | `source ~/.bashrc` |
| Verify | `echo $JAVA_HOME` |

---

## Managing Multiple Java Versions

| Step | Command |
|---|---|
| Install Java 17 | `sudo apt install -y openjdk-17-jdk` |
| Switch Java version | `sudo update-alternatives --config java` |
| Switch compiler version | `sudo update-alternatives --config javac` |

---

## Verify Setup

| Check | Command |
|---|---|
| Java runtime version | `java -version` |
| Java compiler version | `javac -version` |
| Java binary location | `which java` |
| JAVA_HOME value | `echo $JAVA_HOME` |

---

## First Java Program

| Step | Command / Code |
|---|---|
| Create file | `nano HelloWorld.java` |
| Compile | `javac HelloWorld.java` |
| Run (standard) | `java HelloWorld` |
| Run (shortcut, Java 11+) | `java HelloWorld.java` |

**HelloWorld.java:**
```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

---

## IDE Setup

| IDE | Install Command |
|---|---|
| IntelliJ IDEA Community | `sudo snap install intellij-idea-community --classic` |
| VS Code | `sudo snap install code --classic` |
| VS Code Java Extension Pack | `code --install-extension vscjava.vscode-java-pack` |

---

## Common Issues & Fixes

| Issue | Fix |
|---|---|
| `java: command not found` | `export PATH=/usr/lib/jvm/java-21-openjdk-amd64/bin:$PATH` |
| `javac: command not found` | `sudo apt install -y openjdk-21-jdk` |
| Wrong Java version active | `sudo update-alternatives --config java` |
| `UnsupportedClassVersionError` | `javac --release 17 HelloWorld.java` |

---

## Quick Command Reference

| Task | Command |
|---|---|
| Install Java 21 | `sudo apt install -y openjdk-21-jdk` |
| Check Java version | `java -version` |
| Check compiler version | `javac -version` |
| Compile a file | `javac HelloWorld.java` |
| Run a program | `java HelloWorld` |
| Set JAVA_HOME | `export JAVA_HOME=/usr/lib/jvm/java-21-openjdk-amd64` |
| Switch Java version | `sudo update-alternatives --config java` |

---

## Contact Information

| Name | Email |
|---|---|
| Versha Tripathi | [versha.tripathi.snaatak@mygurukulam.co](mailto:versha.tripathi.snaatak@mygurukulam.co) |

---

## References

| # | Resource | Link |
|---|---|---|
| 1 | Ubuntu 24.04 LTS Release Notes | [ubuntu.com/blog/ubuntu-24-04-lts-noble-numbat-released](https://ubuntu.com/blog/ubuntu-24-04-lts-noble-numbat-released) |
| 2 | OpenJDK 21 Official Site | [openjdk.org/projects/jdk/21](https://openjdk.org/projects/jdk/21) |
| 3 | Eclipse Temurin (Adoptium) | [adoptium.net](https://adoptium.net/) |
| 4 | SDKMAN Official Documentation | [sdkman.io](https://sdkman.io/) |
| 5 | Java 21 New Features | [openjdk.org/jeps](https://openjdk.org/jeps/0) |
| 6 | Ubuntu APT Package Manager Docs | [manpages.ubuntu.com/apt](https://manpages.ubuntu.com/manpages/noble/man8/apt.8.html) |
