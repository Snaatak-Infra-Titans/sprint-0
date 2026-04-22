# Maven — Introduction

## Document Details

| Author  | Created On     | Version | Last Updated By | Last Edited On | L0 Reviewer  | L1 Reviewer  | L2 Reviewer   |
|---------|----------------|---------|------------------|----------------|--------------|--------------|---------------|
| Deepak  | 14 April 2026  | v1.1    | Deepak           | 22 April 2026  | Mohit Kumar  | Faisal Khan  | Mahesh Kumar  |

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [What is Maven?](#2-what-is-maven)
3. [Why Maven?](#3-why-maven)
4. [Key Features](#4-key-features)
5. [Local & Remote Repository](#5-local--remote-repository)
6. [Conclusion](#6-conclusion)



## 1. Introduction

Maven is a tool used to build and manage Java projects.

It simplifies dependency management, build process, and project structure.



## 2. What is Maven?

Maven is a **build automation and dependency management tool**.

| Attribute | Meaning |
|-----------|--------|
| Type | Build Tool |
| Language | Java |
| Config File | pom.xml |
| Use | Build, test, package applications |

## 3. Why Maven?

Before Maven:
- Manual dependency handling  
- No standard project structure  
- Complex build scripts  

Maven solves this:

| Problem | Solution |
|---------|----------|
| Manual JARs | Auto download dependencies |
| No structure | Standard layout |
| Complex scripts | Declarative configuration |
| Dependency conflicts | Automatic resolution |



## 4. Key Features

| Feature | Description |
|---------|------------|
| Dependency Management | Auto downloads libraries |
| Build Lifecycle | Standard build phases |
| Convention | Standard project structure |
| Plugins | Extend functionality |
| Reproducibility | Same build everywhere |



## 5. Local & Remote Repository

Maven stores and fetches dependencies using repositories.

### Local Repository

| Attribute | Detail |
|-----------|--------|
| Location | ~/.m2/repository |
| Purpose | Cache dependencies |
| Benefit | Faster builds |

### Remote Repository

| Type | Description |
|------|------------|
| Maven Central | Default public repository |
| Private Repo | Company internal (Nexus/Artifactory) |

### Flow

Local → Remote → Download → Cache → Use

<img width="900" height="300" alt="ChatGPT Image Apr 22, 2026, 11_17_12 PM" src="https://github.com/user-attachments/assets/24430ef9-5bf5-4ff4-9199-f8806df06e54" />




## 6. Conclusion

Maven simplifies Java builds by automating dependencies and standardizing projects.



## 7. References

| Description | Link |
|-------------|------|
| Official Maven documentation | [Maven Docs](https://maven.apache.org) |
| Maven Central repository | [Maven Central](https://search.maven.org) |
| Maven lifecycle guide | [Build Lifecycle](https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html) |


## Contact Information


| Name   | Contact                                  |
|--------|------------------------------------------|
| Deepak | deepak.nagar.snaatak@mygurukulam.co      |

