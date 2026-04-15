# Common Stack | Applications | Java | SOP for pom.xml

## Author Table

| Author  | Created on | Version | Last updated by | Last Edited On | Pre Reviewer | L0 Reviewer | L1 Reviewer |
| ------- | ---------- | ------- | --------------- | -------------- | ------------ | ----------- | ----------- |
| Saransh | 15-04-2026 | 1.0     | -               | -              | -            | -           | -           |

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [Purpose](#2-purpose)
3. [What is pom.xml](#3-what-is-pomxml)
4. [Why pom.xml is Important](#4-why-pomxml-is-important)
5. [Prerequisites](#5-prerequisites)
6. [Basic Structure of pom.xml](#6-basic-structure-of-pomxml)
7. [Step-by-Step Setup Guide](#7-step-by-step-setup-guide)

   * [Step 1: Install Java](#step-1-install-java)
   * [Step 2: Install Maven](#step-2-install-maven)
   * [Step 3: Verify Installation](#step-3-verify-installation)
   * [Step 4: Create a Maven Project](#step-4-create-a-maven-project)
   * [Step 5: Understand the Default pom.xml](#step-5-understand-the-default-pomxml)
   * [Step 6: Add Dependencies](#step-6-add-dependencies)
   * [Step 7: Add Build Plugins](#step-7-add-build-plugins)
   * [Step 8: Build the Project](#step-8-build-the-project)
   * [Step 9: Run Tests](#step-9-run-tests)
   * [Step 10: Package the Application](#step-10-package-the-application)
8. [Sample pom.xml](#8-sample-pomxml)
9. [Commonly Used Sections in pom.xml](#9-commonly-used-sections-in-pomxml)
10. [Troubleshooting](#10-troubleshooting)
11. [Best Practices](#11-best-practices)
12. [Use Cases](#12-use-cases)
13. [Contact Information](#13-contact-information)
14. [References](#14-references)

---

## 1. Introduction

`pom.xml` is the main configuration file used in **Maven-based Java projects**. It defines project details, dependencies, plugins, build settings, and packaging instructions. Whenever Maven builds a Java project, it reads this file to understand how the application should be compiled, tested, and packaged.

---

## 2. Purpose

This document provides a step-by-step guide to understand and use `pom.xml` in Java projects. It explains what it is, why it is important, how to create and modify it, and how to use it during project setup and build operations.

---

## 3. What is pom.xml

`pom.xml` stands for **Project Object Model**. It is an XML file placed at the root of a Maven project.

It usually contains:

* Project name and version
* Group ID and Artifact ID
* Dependencies required by the project
* Plugins needed for build and packaging
* Java version configuration
* Repository information if required

In simple words, `pom.xml` is the **instruction file** for Maven.

---

## 4. Why pom.xml is Important

`pom.xml` is important because it helps in:

* Managing project dependencies automatically
* Standardizing project structure
* Running builds in a consistent way
* Reducing manual JAR handling
* Supporting testing, packaging, and deployment
* Making collaboration easier for teams

Without `pom.xml`, Maven cannot understand how to build the Java project.

---

## 5. Prerequisites

Before working with `pom.xml`, ensure the following are installed:

* Ubuntu / Linux system
* Java JDK 8 or above
* Maven
* Internet connectivity to download dependencies
* Basic understanding of Java project structure

---

## 6. Basic Structure of pom.xml

A simple `pom.xml` looks like this:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">

    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>demo-app</artifactId>
    <version>1.0.0</version>
    <packaging>jar</packaging>

    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

</project>
```

### Meaning of main tags

* `<modelVersion>`: Maven model version
* `<groupId>`: Organization or company name
* `<artifactId>`: Project name
* `<version>`: Project version
* `<packaging>`: Output type such as `jar` or `war`
* `<properties>`: Common settings like Java version

---

## 7. Step-by-Step Setup Guide

### Step 1: Install Java

Update the package list:

```bash
sudo apt update
```

Install Java:

```bash
sudo apt install openjdk-17-jdk -y
```

Check version:

```bash
java -version
```

Expected output should show installed JDK version.

---

### Step 2: Install Maven

Install Maven using apt:

```bash
sudo apt install maven -y
```

---

### Step 3: Verify Installation

Check Maven version:

```bash
mvn -version
```

This command confirms:

* Maven is installed
* Java is linked properly
* Maven home path is available

---

### Step 4: Create a Maven Project

Use Maven archetype to generate a project:

```bash
mvn archetype:generate -DgroupId=com.example -DartifactId=demo-app -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

Move into the project directory:

```bash
cd demo-app
```

You will see a generated `pom.xml` file in the project root.

---

### Step 5: Understand the Default pom.xml

Open the file:

```bash
nano pom.xml
```

A default file generally contains:

* Project coordinates
* A sample dependency section
* Default packaging type

This is the file you will modify based on your project needs.

---

### Step 6: Add Dependencies

Dependencies are libraries required by your project.

Example: Add JUnit dependency.

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

Example: Add Spring Boot dependency.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
    <version>3.2.5</version>
</dependency>
```

After saving the file, Maven downloads these dependencies during build.

---

### Step 7: Add Build Plugins

Plugins are used for build-related tasks.

Example: Maven Compiler Plugin

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.11.0</version>
            <configuration>
                <source>17</source>
                <target>17</target>
            </configuration>
        </plugin>
    </plugins>
</build>
```

This plugin tells Maven which Java version to use for compilation.

---

### Step 8: Build the Project

Run:

```bash
mvn compile
```

This command:

* Reads `pom.xml`
* Downloads dependencies
* Compiles Java source code

---

### Step 9: Run Tests

Run:

```bash
mvn test
```

This executes unit tests defined in the project.

---

### Step 10: Package the Application

Run:

```bash
mvn package
```

This creates the final build artifact inside the `target/` directory.

Examples:

* `demo-app-1.0.0.jar`
* `demo-app-1.0.0.war`

To clean old build files and rebuild:

```bash
mvn clean package
```

---

## 8. Sample pom.xml

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">

    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>demo-app</artifactId>
    <version>1.0.0</version>
    <packaging>jar</packaging>

    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.13.2</version>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.11.0</version>
                <configuration>
                    <source>17</source>
                    <target>17</target>
                </configuration>
            </plugin>
        </plugins>
    </build>

</project>
```

---

## 9. Commonly Used Sections in pom.xml

### 1. Dependencies

Used to add required libraries.

### 2. Properties

Used to define reusable values such as Java version.

### 3. Build

Used to configure plugins and build settings.

### 4. Repositories

Used when dependencies are hosted outside Maven Central.

Example:

```xml
<repositories>
    <repository>
        <id>custom-repo</id>
        <url>https://repo.example.com/maven2</url>
    </repository>
</repositories>
```

### 5. Parent

Used in multi-module or framework-based projects such as Spring Boot.

---

## 10. Troubleshooting

| Issue                      | Possible Cause               | Solution                                                       |
| -------------------------- | ---------------------------- | -------------------------------------------------------------- |
| `mvn: command not found`   | Maven not installed          | Install Maven using `sudo apt install maven -y`                |
| Java version mismatch      | Wrong JDK version            | Check `java -version` and update `pom.xml` compiler properties |
| Dependency download failed | Internet or repository issue | Check internet connection and repository URL                   |
| Build failed               | Syntax error in `pom.xml`    | Validate XML format and closing tags                           |
| Package not created        | Compilation/test failure     | Run `mvn compile` or `mvn test` and fix errors                 |

---

## 11. Best Practices

* Keep dependency versions organized
* Use only required dependencies
* Avoid duplicate dependency entries
* Use properties for Java version and reusable values
* Run `mvn clean package` for fresh builds
* Keep `pom.xml` clean and properly formatted
* Review plugin versions before production usage

---

## 12. Use Cases

`pom.xml` is commonly used in:

* Java application builds
* Spring Boot projects
* Web applications using WAR packaging
* Enterprise Maven-based projects
* CI/CD pipelines using Jenkins, GitHub Actions, or GitLab CI

---

## 13. Contact Information

| Name    | Email Address                                                                   |
| ------- | ------------------------------------------------------------------------------- |
| Saransh | [saransh.rai.snaatak@mygurukulam.co](mailto:saransh.rai.snaatak@mygurukulam.co) |

---

## 14. References

| Topic                        | Link                                                                   |
| ---------------------------- | ---------------------------------------------------------------------- |
| Maven Official Documentation | [https://maven.apache.org/guides/](https://maven.apache.org/guides/)   |
| Maven POM Reference          | [https://maven.apache.org/pom.html](https://maven.apache.org/pom.html) |
| Maven Central Repository     | [https://mvnrepository.com/](https://mvnrepository.com/)               |
| OpenJDK Documentation        | [https://openjdk.org/](https://openjdk.org/)                           |

---

## Notes

This SOP is intended for beginners who want to understand how `pom.xml` works and how it is used in a Java Maven project. It can also be used as a demo document for Pre Reviewer and L0 Reviewer discussion.
