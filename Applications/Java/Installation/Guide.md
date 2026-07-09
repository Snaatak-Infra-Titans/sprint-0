# Java JDK 21 Installation Guide (Ubuntu 24.04)

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



This guide provides a step-by-step approach to installing Java JDK 21 on Ubuntu 24.04. 

Java JDK 21 can be installed on Ubuntu 24.04 using the APT package manager, which is the most straightforward and recommended approach. APT handles dependency management automatically and ensures that you get a stable and well-tested version of OpenJDK directly from Ubuntu repositories. This method is ideal for beginners and for systems where simplicity, stability, and ease of maintenance are important.



---

## Prerequisites

Before installing Java, make sure your system is ready:

* Check Ubuntu version:

  ```bash
  lsb_release -a
  ```
<img width="465" height="152" alt="image" src="https://github.com/user-attachments/assets/72cc4819-207d-4bfa-aadf-7f4bf287d5d6" />

  
* Update system packages:

  ```bash
  sudo apt update && sudo apt upgrade -y
  ```
<img width="1855" height="810" alt="image" src="https://github.com/user-attachments/assets/b6c6985c-033e-4598-9e54-16278e26aa3b" />


---

## Installation Methods



Follow these steps to install Java JDK 21 using APT:

```bash
sudo apt install -y openjdk-21-jdk
```
<img width="852" height="140" alt="image" src="https://github.com/user-attachments/assets/a7fca427-b9bb-47e5-86a1-5cbdb112a631" />

Verify installation:

```bash
java -version
javac -version
```
<img width="852" height="140" alt="image" src="https://github.com/user-attachments/assets/0be5fa52-a3f0-4a83-bb97-1f11450bb878" />

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
<img width="852" height="140" alt="image" src="https://github.com/user-attachments/assets/8b4d422b-6b4f-4733-984c-58e671f9521c" />

Switch Java version:

```bash
sudo update-alternatives --config java
```

Switch compiler version:

```bash
sudo update-alternatives --config javac
```
<img width="1222" height="512" alt="image" src="https://github.com/user-attachments/assets/7b2850a6-e0da-4497-800f-626b084ae218" />

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
