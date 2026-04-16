# SOP: Managing Java Projects with Maven (mvn)

> A step-by-step guide to build, test, package, and debug Java applications using Maven (`mvn`), including commonly used and troubleshooting commands.

---

| Author | Created on | Version | Last updated by | Last edited on | PRE Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
| ------ | ---------- | ------- | --------------- | -------------- | ------------ | ----------- | ----------- | ----------- |
| Gourav | 16-04-2026 | v1.0    | Gourav          | 16-04-2026     | -            | -           | -           | -           |

---

## Table of Contents

1. Purpose
2. What is Maven?
3. Maven Project Structure
4. Core Maven Commands

   * 4.1 Clean Project
   * 4.2 Compile Code
   * 4.3 Run Tests
   * 4.4 Package Application
   * 4.5 Install to Local Repository
   * 4.6 Run Application
5. Debugging & Troubleshooting Commands
6. Maven Lifecycle Explained
7. Maven in OT-Microservices
8. Troubleshooting Common Issues
9. Quick Reference
10. Conclusion

---

## 1. Purpose

This SOP explains how to manage Java applications using **Maven (`mvn`)**.

By the end of this document, you will be able to:

* Build Java applications using Maven
* Run tests and debug failures
* Package applications into `.jar` files
* Install dependencies locally
* Troubleshoot build failures

---

## 2. What is Maven?

Maven is a **build automation and dependency management tool** for Java projects.

It helps you:

* Download required libraries automatically
* Compile code
* Run tests
* Package applications
* Maintain a standard project structure

> **Tip:** Think of Maven as a “project manager” for Java applications.

---

## 3. Maven Project Structure

From your OT-Microservices project, the **salary-api** service is a Maven project 

### Key files:

```
salary-api/
├── pom.xml        ← Main configuration file
├── src/
│   ├── main/java  ← Application code
│   ├── main/resources
│   └── test/java  ← Test code
```

### Important:

* `pom.xml` → defines dependencies, plugins, build config
* `src/main/java` → main code
* `src/test/java` → test cases

---

## 4. Core Maven Commands

Basic syntax:

```bash
mvn <goal>
```

---

### 4.1 Clean Project

Removes old build files.

```bash
mvn clean
```

> Deletes the `target/` directory.

---

### 4.2 Compile Code

Compiles Java source code.

```bash
mvn compile
```

> Converts `.java` → `.class`

---

### 4.3 Run Tests

Executes all test cases.

```bash
mvn test
```

> Runs tests from `src/test/java`

---

### 4.4 Package Application

Creates a `.jar` file.

```bash
mvn package
```

Output:

```
target/salary-api.jar
```

---

### 4.5 Install to Local Repository

Installs package into local Maven repo (`~/.m2`)

```bash
mvn install
```

> Used when other projects depend on this project.

---

### 4.6 Run Application

For Spring Boot apps (like your salary-api):

```bash
mvn spring-boot:run
```

OR run jar:

```bash
java -jar target/salary-api.jar
```

---

## 5. Debugging & Troubleshooting Commands

These are VERY important in real DevOps work 

---

### Show Full Error Logs

```bash
mvn clean install -e
```

---

### Enable Debug Mode

```bash
mvn clean install -X
```

> Shows detailed logs (very verbose)

---

### Skip Tests (when tests are failing)

```bash
mvn clean install -DskipTests
```

---

### Check Dependency Tree

```bash
mvn dependency:tree
```

> Helps find dependency conflicts

---

### Download Dependencies Only

```bash
mvn dependency:resolve
```

---

### Force Update Dependencies

```bash
mvn clean install -U
```

> Useful when dependencies are corrupted

---

## 6. Maven Lifecycle Explained

Maven works in phases:

| Phase      | What it Does            |
| ---------- | ----------------------- |
| `validate` | Check project structure |
| `compile`  | Compile code            |
| `test`     | Run tests               |
| `package`  | Create jar/war          |
| `install`  | Save to local repo      |
| `deploy`   | Upload to remote repo   |

 When you run:

```bash
mvn install
```

It automatically runs:

```
validate → compile → test → package → install
```

---

## 7. Maven in OT-Microservices

In your project, only **salary-api** uses Maven 

### Steps to run it:

```bash
cd salary-api
mvn clean install
mvn spring-boot:run
```

---

## 8. Troubleshooting — Common Issues

| Problem              | Cause                 | Solution                    |
| -------------------- | --------------------- | --------------------------- |
| Build failed         | Code error            | Check logs with `-e`        |
| Dependency not found | Internet/repo issue   | Run `mvn clean install -U`  |
| Tests failing        | Bug in test or code   | Skip using `-DskipTests`    |
| Port already in use  | App already running   | Kill process or change port |
| Slow build           | Too many dependencies | Check `dependency:tree`     |

---

## 9. Quick Reference

| Command                         | What it Does              |
| ------------------------------- | ------------------------- |
| `mvn clean`                     | Remove old builds         |
| `mvn compile`                   | Compile code              |
| `mvn test`                      | Run tests                 |
| `mvn package`                   | Create jar                |
| `mvn install`                   | Install to local repo     |
| `mvn spring-boot:run`           | Run app                   |
| `mvn clean install -DskipTests` | Build without tests       |
| `mvn clean install -X`          | Debug mode                |
| `mvn dependency:tree`           | Show dependencies         |
| `mvn clean install -U`          | Force update dependencies |

---

## 10. Conclusion

Maven is essential for managing Java-based microservices.

**Key Takeaways:**

* `mvn clean install` is the most commonly used command
* Use `-X` and `-e` for debugging
* Use `dependency:tree` to debug conflicts
* Use `spring-boot:run` to start applications quickly

---

## 11. References

| Resource                 | Link                                                               |
| ------------------------ | ------------------------------------------------------------------ |
| Apache Maven Docs        | [https://maven.apache.org/guides](https://maven.apache.org/guides) |
| Maven Central Repo       | [https://search.maven.org](https://search.maven.org)               |
| Spring Boot Maven Plugin | [https://docs.spring.io](https://docs.spring.io)                   |

---

**Author: Gourav Sharma | Sprint 0 | Infra Titans | 14 April 2026

