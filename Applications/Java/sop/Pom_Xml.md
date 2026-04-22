# SOP: Common Stack | Java | Maven | `pom.xml` (Step-by-Step Installation Guide)

<p align="center">
  <strong><img width="225" height="225" alt="image" src="https://github.com/user-attachments/assets/04741644-b17b-4486-80ad-b7f287dd6ff7" />
</strong>
</p>

---

## Author Table

| Author      | Created On | Version | Last Updated By | Last Edited On | Pre Reviewer | L0 Reviewer | L1 Reviewer     |
| ----------- | ---------- | ------: | --------------- | -------------- | ------------ | ----------- | --------------- |
| Saransh Rai | 15-04-2026 |     2.0 | Saransh Rai     | 22-04-2026     | Team         | Anuj Jain   | Prashant Sharma |

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [Purpose](#2-purpose)
3. [Prerequisites](#3-prerequisites)
4. [Installation Steps](#4-installation-steps)
   4.1 [Step 1: Install Java](#41-step-1-install-java)
   4.2 [Step 2: Install Maven](#42-step-2-install-maven)
   4.3 [Step 3: Verify Installation](#43-step-3-verify-installation)
   4.4 [Step 4: Create Maven Project](#44-step-4-create-maven-project)
   4.5 [Step 5: Navigate to Project Directory](#45-step-5-navigate-to-project-directory)
   4.6 [Step 6: Understand `pom.xml`](#46-step-6-understand-pomxml)
   4.7 [Step 7: Add Dependencies](#47-step-7-add-dependencies)
   4.8 [Step 8: Build the Project](#48-step-8-build-the-project)
   4.9 [Step 9: Package the Application](#49-step-9-package-the-application)
5. [Validation](#5-validation)
6. [Troubleshooting](#6-troubleshooting)
7. [Best Practices](#7-best-practices)
8. [Conclusion](#8-conclusion)
9. [Contact Information](#9-contact-information)
10. [References](#10-references)

---

## 1. Introduction

This SOP explains how to install Java and Maven, create a Maven-based Java project, understand the role of `pom.xml`, add dependencies, and build/package the application in a standard Ubuntu/Linux environment.

---

## 2. Purpose

The purpose of this SOP is to provide a clear step-by-step installation guide to:

I. Install the required tools such as Java and Maven
II. Create a Maven-based Java project
III. Understand and configure the `pom.xml` file
IV. Build and package the Java application successfully

---

## 3. Prerequisites

Ensure the following before starting:

| S. No. | Requirement        | Details                                           |
| ------ | ------------------ | ------------------------------------------------- |
| 1      | Operating System   | Ubuntu / Linux system                             |
| 2      | Internet Access    | Required for installing packages and dependencies |
| 3      | Terminal Knowledge | Basic understanding of Linux terminal commands    |
| 4      | User Privileges    | `sudo` access required                            |

---

## 4. Installation Steps

### 4.1 Step 1: Install Java

Update package index and install Java:

```bash
sudo apt update
sudo apt install openjdk-17-jdk -y
```

Verify Java installation:

```bash
java -version
```

Expected result:

* Java version details should be displayed.

**Image Placeholder:** Add screenshot of Java installation command output here.

---

### 4.2 Step 2: Install Maven

Install Maven using APT:

```bash
sudo apt install maven -y
```

Expected result:

* Maven should be installed successfully without errors.

**Image Placeholder:** Add screenshot of Maven installation output here.

---

### 4.3 Step 3: Verify Installation

Run the following command to verify Maven installation:

```bash
mvn -version
```

Expected result:

* Maven version
* Java version
* Maven home path
* Java home path

**Image Placeholder:** Add screenshot of `mvn -version` output here.

---

### 4.4 Step 4: Create Maven Project

Generate a sample Maven project using the Maven archetype command:

```bash
mvn archetype:generate \
-DgroupId=com.example \
-DartifactId=demo-app \
-DarchetypeArtifactId=maven-archetype-quickstart \
-DinteractiveMode=false
```

Expected result:

* A new project folder named `demo-app` will be created.
* A default `pom.xml` file will be generated automatically.

**Image Placeholder:** Add screenshot of Maven project generation output here.

---

### 4.5 Step 5: Navigate to Project Directory

Move into the generated project directory:

```bash
cd demo-app
```

Expected result:

* Terminal should now point to the `demo-app` directory.

**Image Placeholder:** Add screenshot showing terminal inside `demo-app` directory here.

---

### 4.6 Step 6: Understand `pom.xml`

Open the `pom.xml` file using any text editor:

```bash
nano pom.xml
```

Important sections in `pom.xml`:

| Element        | Description                                        |
| -------------- | -------------------------------------------------- |
| `groupId`      | Represents the organization or package namespace   |
| `artifactId`   | Represents the project name                        |
| `version`      | Represents the project version                     |
| `dependencies` | Defines external libraries required by the project |
| `build`        | Used for build-related configurations and plugins  |

**Image Placeholder:** Add screenshot of the `pom.xml` file here.

---

### 4.7 Step 7: Add Dependencies

Example dependency block:

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

Purpose:

* This adds JUnit as a testing dependency for the project.

**Image Placeholder:** Add screenshot of updated `pom.xml` with dependency here.

---

### 4.8 Step 8: Build the Project

Compile the Maven project:

```bash
mvn compile
```

Expected result:

* Source files should compile successfully.
* Maven should show `BUILD SUCCESS` if compilation completes correctly.

**Image Placeholder:** Add screenshot of `mvn compile` output here.

---

### 4.9 Step 9: Package the Application

Package the application into a JAR file:

```bash
mvn package
```

Expected result:

* Maven should create a packaged `.jar` file inside the `target/` directory.
* Example output file: `target/demo-app-1.0-SNAPSHOT.jar`

**Image Placeholder:** Add screenshot of `mvn package` output here.

---

## 5. Validation

After packaging, confirm that the build artifact exists:

```bash
ls target/
```

Expected result:

* A `.jar` file should be visible in the `target/` folder.

| Validation Check  | Expected Result                  |
| ----------------- | -------------------------------- |
| Java installed    | `java -version` works            |
| Maven installed   | `mvn -version` works             |
| Project created   | `demo-app` folder exists         |
| Build completed   | `BUILD SUCCESS` displayed        |
| Package generated | `.jar` file present in `target/` |

**Image Placeholder:** Add screenshot of `ls target/` output here.

---

## 6. Troubleshooting

| Issue                       | Possible Cause                           | Resolution                                            |
| --------------------------- | ---------------------------------------- | ----------------------------------------------------- |
| `mvn: command not found`    | Maven is not installed or PATH issue     | Install Maven again using `sudo apt install maven -y` |
| Java version error          | Java not installed properly              | Verify with `java -version` and reinstall OpenJDK     |
| Build failed                | Syntax issue in `pom.xml` or source code | Recheck XML syntax and project code                   |
| Dependency download failure | Internet or repository access issue      | Check network connectivity and retry                  |
| Permission denied           | Insufficient privileges                  | Use `sudo` where required                             |

---

## 7. Best Practices

| S. No. | Best Practice                | Description                                          |
| ------ | ---------------------------- | ---------------------------------------------------- |
| 1      | Use the correct Java version | Ensure the Java version matches project requirements |
| 2      | Keep dependencies minimal    | Add only required libraries to reduce conflicts      |
| 3      | Use clean builds             | Prefer `mvn clean package` for fresh packaging       |
| 4      | Maintain readable `pom.xml`  | Keep the file organized and properly indented        |
| 5      | Verify after each major step | Validate Java, Maven, and build output step by step  |

---

## 8. Conclusion

This SOP provides a structured approach for installing Java and Maven, creating a Maven project, understanding `pom.xml`, and building/packageing the application. Following these steps helps standardize Java project setup and reduces build-related issues in development environments.

---

## 9. Contact Information

| Name        | Email                                                                           |
| ----------- | ------------------------------------------------------------------------------- |
| Saransh Rai | [saransh.rai.snaatak@mygurukulam.co](mailto:saransh.rai.snaatak@mygurukulam.co) |

---

## 10. References

| Topic                               | Link                                                     |
| ----------------------------------- | -------------------------------------------------------- |
| Apache Maven Official Documentation | [https://maven.apache.org/](https://maven.apache.org/)   |
| Maven Repository                    | [https://mvnrepository.com/](https://mvnrepository.com/) |
| OpenJDK Documentation               | [https://openjdk.org/](https://openjdk.org/)             |

