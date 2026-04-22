# pom.xml - Documentation
<p align="center">
  <img src="https://img.shields.io/badge/maven-build--tool-blue" />
  <img src="https://img.shields.io/badge/java-configuration-green" />
  <img src="https://img.shields.io/badge/type-project--descriptor-orange" />
</p>

---

| Author       | Created On | Version | Last Updated By | Last Edited On | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer  |
| ------------ | ---------- | ------- | --------------- | -------------- | ------------ | ----------- | ----------- | ------------ |
| Mukesh Kharb | 15/04/2026 | 1.0     | Mukesh Kharb    | 15/04/2026     | Team         | Mohit Kumar | Faisal Khan | Mahesh Kumar |
---

## Table of Contents

* [Introduction](#introduction)
* [Why pom.xml](#why-pomxml)
* [Example pom.xml](Example-pom.xml)
* [Dependency Versioning](#dependency-versioning)
* [Workflow](#workflow)
* [Best Practices](#best-practices)
* [Troubleshooting](#troubleshooting)
* [FAQs](#faqs)
* [References](#references)
* [Contact Information](#contact-information)

---

## Introduction

POM.xml stands for Project Object Model. It is an XML file that acts as the central configuration file for projects built using the Apache Maven tool.

You can think of it as a blueprint or recipe for your project. It is placed in the root directory and defines everything Maven needs to build, manage, and deploy the application.

It controls:

* Project structure
* Dependencies
* Build lifecycle
* Plugin configurations

---

## Why pom.xml

| Benefit            | Description                                |
| ------------------ | ------------------------------------------ |
| Dependency Control | Automatically downloads required libraries |
| Build Automation   | Handles compile, test, package lifecycle   |
| Consistency        | Same configuration across all environments |
| Reproducibility    | Ensures stable builds with fixed versions  |

---

## Example pom.xml

```xml
<project>
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.example</groupId>
  <artifactId>demo-app</artifactId>
  <version>1.0.0</version>

  <dependencies>
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-web</artifactId>
      <version>3.0.0</version>
    </dependency>
  </dependencies>
</project>
```

| Element      | Purpose                 |
| ------------ | ----------------------- |
| groupId      | Organization identifier |
| artifactId   | Project name            |
| version      | Project version         |
| dependencies | External libraries      |

---

## Dependency Versioning

| Strategy      | Example   | Use Case           |
| ------------- | --------- | ------------------ |
| Exact Version | 1.0.0     | Production         |
| Latest        | RELEASE   | Development        |
| Range         | [1.0,2.0) | Controlled upgrade |

---

## Workflow


><img width="1000" height="auto" alt="ChatGPT Image Apr 22, 2026, 10_09_35 PM" src="https://github.com/user-attachments/assets/8c799217-392a-4653-adf0-06e3cac9428c" />


---

## Best Practices

* Use fixed versions for production
* Keep dependencies minimal
* Use dependency management for large projects
* Avoid unnecessary plugins

---

## Troubleshooting

| Issue                | Cause             | Solution                  |
| -------------------- | ----------------- | ------------------------- |
| Dependency not found | Wrong version     | Verify version            |
| Build failure        | Missing config    | Check pom.xml structure   |
| Version conflict     | Multiple versions | Use dependency management |

---
## FAQs

1. What is the purpose of pom.xml?

>It defines project configuration, dependencies, and build process for Maven-based applications.

2. Where is pom.xml located?

>It is placed in the root directory of the Maven project.

3. Can a project work without pom.xml?

>No, Maven requires pom.xml to understand how to build and manage the project.

4. How does Maven manage dependencies using pom.xml?

>Maven automatically downloads required libraries from repositories based on dependency definitions.

5. Why is versioning important in pom.xml?

>It ensures consistent builds and prevents conflicts between different dependency versions.

---
## References

| Resource      | Link                                                                                     |
| ------------- | ---------------------------------------------------------------------------------------- |
| Maven Docs    | [https://maven.apache.org/guides/index.html](https://maven.apache.org/guides/index.html) |
| POM Reference | [https://maven.apache.org/pom.html](https://maven.apache.org/pom.html)                   |

---

## Contact Information

| Name         | Email                                                                             |
| ------------ | --------------------------------------------------------------------------------- |
| Mukesh Kharb | [mukesh.Kharb.snaatak@mygurukulam.co](mailto:mukesh.Kharb.snaatak@mygurukulam.co) |

---
