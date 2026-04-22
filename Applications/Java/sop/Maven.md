

#  Maven Installation & Usage Guide (Ubuntu 24.04)

Build, manage, and debug Java projects using Apache Maven

---

##  Document Information

| Author | Created on | Version | Last updated by | Last edited on | PRE Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
| ------ | ---------- | ------- | --------------- | -------------- | ------------ | ----------- | ----------- | ----------- |
| Gourav | 15-04-2026 | v1.0    | Gourav          | 15-04-2026     | -            | -           | -           | -           |

---

##  Overview

This guide explains:

* ✅ Maven Installation (APT)
* ✅ Project Build Lifecycle
* ✅ Commonly Used Commands
* ✅ Debugging Commands

---

##  What is Maven?

Apache Maven is a:

* Build automation tool
* Dependency manager
* Project structure standardizer

---

##  Maven Basics

| Component    | Purpose                              |
| ------------ | ------------------------------------ |
| `pom.xml`    | Project configuration file           |
| Dependencies | External libraries                   |
| Plugins      | Extend Maven functionality           |
| Repository   | Stores dependencies (local + remote) |

>  Everything in Maven is controlled via `pom.xml`

---

##  Prerequisites

### Check Java Installed

```bash
java -version
```

>  Maven requires Java (JDK 8 or above)

---

### Install Java (if not installed)

```bash
sudo apt install -y openjdk-17-jdk
```

---

### Update System

```bash
sudo apt update && sudo apt upgrade -y
```

> 📸 *Add screenshot here*

---

##  Installation

### Method A: Install via APT (Recommended)

```bash
sudo apt install -y maven
```

---

### Verify Installation

```bash
mvn -version
```

> 📸 *Add screenshot here*

---

## 📂 Maven Project Structure

```bash
project/
├── pom.xml
└── src/
    ├── main/java
    └── test/java
```

---

## 🔄 Maven Build Lifecycle

| Phase    | Purpose                   |
| -------- | ------------------------- |
| validate | Check project correctness |
| compile  | Compile source code       |
| test     | Run unit tests            |
| package  | Create JAR/WAR            |
| verify   | Run checks                |
| install  | Install to local repo     |
| deploy   | Upload to remote repo     |

---

##  Commonly Used Commands

### Clean Project

```bash
mvn clean
```

---

### Compile Code

```bash
mvn compile
```

---

### Run Tests

```bash
mvn test
```

---

### Package Application

```bash
mvn package
```

👉 Output: `.jar` or `.war` file in `target/`

---

### Install to Local Repository

```bash
mvn install
```

---

### Skip Tests

```bash
mvn clean install -DskipTests
```

---

### Run Specific Test

```bash
mvn -Dtest=TestClassName test
```

---

### Check Dependencies

```bash
mvn dependency:tree
```

---

### Download Dependencies Only

```bash
mvn dependency:resolve
```

---

##  Running a Spring Boot App (Example)

```bash
mvn spring-boot:run
```

---

##  Useful Maven Options

| Option | Meaning         |
| ------ | --------------- |
| `-X`   | Debug mode      |
| `-q`   | Quiet mode      |
| `-e`   | Show errors     |
| `-D`   | Define property |
| `-o`   | Offline mode    |

---

##  Debugging Commands

### Enable Debug Logs

```bash
mvn clean install -X
```

---

### Show Full Error Stack

```bash
mvn clean install -e
```

---

### Check Dependency Conflicts

```bash
mvn dependency:tree
```

---

### Force Update Dependencies

```bash
mvn clean install -U
```

---

### Check Effective POM

```bash
mvn help:effective-pom
```

---

### Check Environment Info

```bash
mvn help:system
```

---

## 🔄 Local Repository

Default location:

```bash
~/.m2/repository
```

---

### Clear Local Cache

```bash
rm -rf ~/.m2/repository
```

---

##  Common Issues

### mvn: command not found

```bash
sudo apt install -y maven
```

---

### JAVA_HOME not set

```bash
echo $JAVA_HOME
```

Set it:

```bash
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
```

---

### Dependency Not Downloading

```bash
mvn clean install -U
```

---

### Build Failure

```bash
mvn clean install -e -X
```

---

##  Quick Commands

| Task            | Command                  |
| --------------- | ------------------------ |
| Install Maven   | `sudo apt install maven` |
| Check version   | `mvn -version`           |
| Build project   | `mvn clean install`      |
| Skip tests      | `-DskipTests`            |
| Debug mode      | `-X`                     |
| Show errors     | `-e`                     |
| Dependency tree | `mvn dependency:tree`    |

---

## 🎉 Done!

You have successfully:

* Installed Maven
* Understood lifecycle phases
* Used common commands
* Learned debugging techniques

---

**Author:** Gourav Sharma | Sprint 0 | OT-Microservices 

