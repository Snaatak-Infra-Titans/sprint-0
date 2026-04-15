# SOP: pom.xml (Step-by-Step Installation Guide)

## Author Table

| Author  | Created on | Version | Last updated by | Last Edited On | Pre Reviewer | L0 Reviewer | L1 Reviewer |
| ------- | ---------- | ------- | --------------- | -------------- | ------------ | ----------- | ----------- |
| Saransh | 15-04-2026 | 2.0     | -               | -              | -            | -           | -           |

---

## Table of Contents

1. [Scope](#1-scope)
2. [Purpose](#2-purpose)
3. [Prerequisites](#3-prerequisites)
4. [Installation Steps](#4-installation-steps)

   * [Step 1: Install Java](#step-1-install-java)
   * [Step 2: Install Maven](#step-2-install-maven)
   * [Step 3: Verify Installation](#step-3-verify-installation)
   * [Step 4: Create Maven Project](#step-4-create-maven-project)
   * [Step 5: Navigate to Project](#step-5-navigate-to-project)
   * [Step 6: Understand pom.xml](#step-6-understand-pomxml)
   * [Step 7: Add Dependencies](#step-7-add-dependencies)
   * [Step 8: Build the Project](#step-8-build-the-project)
   * [Step 9: Package the Application](#step-9-package-the-application)
5. [Validation](#5-validation)
6. [Troubleshooting](#6-troubleshooting)
7. [Best Practices](#7-best-practices)
8. [Contact Information](#8-contact-information)
9. [References](#9-references)

---

## 1. Scope

This SOP covers the **installation and setup of a Maven-based Java project using pom.xml**, including project creation, dependency management, and build execution.

---

## 2. Purpose

The purpose of this SOP is to provide a **clear step-by-step installation guide** to:

* Install required tools (Java & Maven)
* Create a Maven project
* Understand and configure `pom.xml`
* Build and package the application

---

## 3. Prerequisites

Ensure the following before starting:

* Ubuntu / Linux system
* Internet connection
* Basic terminal knowledge
* Sudo access

---

## 4. Installation Steps

### Step 1: Install Java

```bash
sudo apt update
sudo apt install openjdk-17-jdk -y
```

Verify:

```bash
java -version
```

---

### Step 2: Install Maven

```bash
sudo apt install maven -y
```

---

### Step 3: Verify Installation

```bash
mvn -version
```

Expected:

* Maven version
* Java version

---

### Step 4: Create Maven Project

```bash
mvn archetype:generate \
-DgroupId=com.example \
-DartifactId=demo-app \
-DarchetypeArtifactId=maven-archetype-quickstart \
-DinteractiveMode=false
```

Output:

* New project folder created (`demo-app`)
* Default `pom.xml` generated

---

### Step 5: Navigate to Project

```bash
cd demo-app
```

---

### Step 6: Understand pom.xml

Open file:

```bash
nano pom.xml
```

Key sections:

* `groupId` → organization name
* `artifactId` → project name
* `version` → project version
* `dependencies` → libraries

---

### Step 7: Add Dependencies

Example:

```xml
<dependencies>
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.13.2</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```

---

### Step 8: Build the Project

```bash
mvn compile
```

---

### Step 9: Package the Application

```bash
mvn package
```

Output:

```bash
target/demo-app-1.0.0.jar
```

---

## 5. Validation

Check if build is successful:

```bash
ls target/
```

Expected:

* `.jar` file present

---

## 6. Troubleshooting

| Issue            | Solution                  |
| ---------------- | ------------------------- |
| mvn not found    | Install Maven             |
| Java error       | Check `java -version`     |
| Build failed     | Check `pom.xml` syntax    |
| Dependency issue | Check internet connection |

---

## 7. Best Practices

* Use correct Java version
* Keep dependencies minimal
* Always run `mvn clean package`
* Maintain clean `pom.xml`

---

## 8. Contact Information

| Name    | Email                                                                           |
| ------- | ------------------------------------------------------------------------------- |
| Saransh | [saransh.rai.snaatak@mygurukulam.co](mailto:saransh.rai.snaatak@mygurukulam.co) |

---

## 9. References

* [https://maven.apache.org/](https://maven.apache.org/)
* [https://mvnrepository.com/](https://mvnrepository.com/)

---

## Notes

This SOP focuses only on **installation and basic setup of pom.xml** as per requirement: *Step by step installation guide*.

For advanced topics (plugins, multi-module, CI/CD), refer separate documentation.
