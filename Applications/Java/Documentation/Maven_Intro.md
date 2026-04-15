# Maven — Documentation

| Author | Created On | Version | Last Updated By | Last Edited On | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|--------|------------|---------|-----------------|----------------|--------------|-------------|-------------|-------------|
| Deepak | April 2026 | v1.0 | Deepak | April 2026 | | | | |

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [What is Maven?](#2-what-is-maven)
3. [Why Maven?](#3-why-maven)
4. [Key Features](#4-key-features)
5. [Local Repository and Remote Repository](#5-local-repository-and-remote-repository)
6. [Maven in OT-Microservices](#6-maven-in-ot-microservices)
7. [Conclusion](#7-conclusion)
8. [Contact Information](#8-contact-information)
9. [References](#9-references)

---

## 1. Introduction

Building a Java application involves more than just writing code. You need to download third-party libraries, compile source files in the right order, run tests, package everything into a deployable artifact, and repeat this reliably across every developer's machine and every CI/CD pipeline.

Doing all of this manually — tracking library versions, managing classpaths, writing custom build scripts — is error-prone and does not scale. **Maven** solves this by providing a standardized, declarative way to define, build, test, and package Java projects.

> **In the context of OT-Microservices:** Maven is used to build the **Salary API** — a Java Spring Boot application. The command `mvn clean install -DskipTests` compiles the source code and packages it into a runnable JAR file.

---

## 2. What is Maven?

**Apache Maven** is an open-source **build automation and dependency management tool** for Java projects. It is maintained by the Apache Software Foundation and is the most widely used build tool in the Java ecosystem.

| Attribute | Detail |
|-----------|--------|
| **Full Name** | Apache Maven |
| **Developed By** | Apache Software Foundation |
| **First Released** | 2004 |
| **Language** | Written in Java |
| **License** | Apache License 2.0 |
| **Config File** | `pom.xml` (Project Object Model) |
| **Install Command** | `sudo apt install -y maven` (Ubuntu) |
| **Version Check** | `mvn --version` |

Maven is built around a central idea: instead of writing instructions for *how* to build your project, you declare *what* your project is — its dependencies, its structure, its packaging format — and Maven figures out the how.

This is called a **declarative** build model, as opposed to the **imperative** model used by older tools like Apache Ant.

### 2.1 What Does Maven Actually Do?

Maven handles three major concerns in a Java project:

| Concern | What Maven Does |
|---------|-----------------|
| **Dependency Management** | Downloads required libraries (JARs) from the internet automatically |
| **Build Lifecycle** | Compiles code, runs tests, packages artifacts in a defined order |
| **Project Standardization** | Enforces a standard directory structure across all projects |

---

## 3. Why Maven?

### 3.1 The Problem Before Maven

Before Maven, Java projects were typically built using **Apache Ant** or custom shell scripts. These approaches had significant drawbacks:

| Problem | Impact |
|---------|--------|
| **Manual JAR management** | Developers downloaded library JARs manually and committed them to version control, making repositories bloated and version conflicts common |
| **No standard structure** | Every project had its own folder layout — `src/`, `source/`, `java/` — making it hard to onboard new developers |
| **Build scripts were imperative** | Ant scripts described every step manually. Changing one thing often broke the entire script |
| **No transitive dependency resolution** | If Library A depended on Library B, you had to manually find and download Library B yourself |
| **Not reproducible** | "Works on my machine" was a common problem because each developer's environment differed |

### 3.2 How Maven Fixes Each Problem

| Problem | Maven's Solution |
|---------|-----------------|
| Manual JAR management | Declare dependencies in `pom.xml` — Maven downloads them automatically |
| No standard structure | Maven enforces a universal directory layout every project follows |
| Imperative build scripts | Declarative `pom.xml` — describe what you need, not how to build it |
| No transitive dependencies | Maven resolves the full dependency tree automatically |
| Not reproducible | Same `pom.xml` produces the same build on any machine with Maven installed |

### 3.3 Maven vs Other Java Build Tools

| Tool | Type | Strengths | When to Choose |
|------|------|-----------|----------------|
| **Maven** | Declarative XML | Convention over configuration, huge ecosystem, well understood | Standard enterprise Java, Spring Boot projects |
| **Gradle** | Declarative DSL (Groovy/Kotlin) | Faster incremental builds, more flexible | Android development, large multi-module projects |
| **Ant** | Imperative XML | Full control over every step | Legacy projects that already use Ant |
| **sbt** | Scala build tool | Native Scala support | Scala projects |

Maven is the default choice for **Spring Boot** projects (including the OT-Microservices Salary API) because Spring Initializr generates Maven projects by default and Spring's documentation is written assuming Maven.

---

## 4. Key Features

### 4.1 Convention Over Configuration

Maven defines a **standard project structure** that every Maven project follows. Because the structure is the same everywhere, Maven knows where to find source files, test files, and resources without being told:

```
project-root/
├── pom.xml                        ← Project definition and dependencies
├── src/
│   ├── main/
│   │   ├── java/                  ← Application source code (.java files)
│   │   └── resources/             ← Config files (application.yml, etc.)
│   └── test/
│       ├── java/                  ← Test source code
│       └── resources/             ← Test config files
└── target/                        ← Generated by Maven (compiled classes, JAR)
    ├── classes/                   ← Compiled .class files
    └── salary-0.1.0-RELEASE.jar   ← Final packaged artifact
```

The `target/` directory is always generated — never committed to version control. It is the output of a Maven build.

### 4.2 The Build Lifecycle

Maven defines a standard **build lifecycle** — an ordered sequence of phases. When you run a phase, Maven automatically runs all phases before it in the correct order.

The default lifecycle has these key phases:

| Phase | What It Does |
|-------|-------------|
| `validate` | Checks the project structure and `pom.xml` are correct |
| `compile` | Compiles all `.java` source files into `.class` bytecode |
| `test` | Runs unit tests using a test framework (JUnit, TestNG) |
| `package` | Packages compiled classes into a JAR or WAR file |
| `verify` | Runs integration tests and checks package quality |
| `install` | Copies the JAR into the local repository (`~/.m2`) |
| `deploy` | Uploads the JAR to a remote repository (Nexus, Artifactory) |

**Example:** Running `mvn install` automatically triggers `validate → compile → test → package → verify → install` in that order. You never need to call each phase individually.

```bash
# Most common Maven commands

# Compile only
mvn compile

# Compile and run tests
mvn test

# Compile, test, and package into a JAR
mvn package

# Full build + install to local repo (most commonly used)
mvn install

# Full build, skip tests (used when tests need a running DB)
mvn clean install -DskipTests

# Delete the target/ folder and rebuild from scratch
mvn clean install
```

### 4.3 Dependency Management via pom.xml

The `pom.xml` (Project Object Model) is the heart of every Maven project. It is an XML file that declares everything Maven needs to know about your project.

**A simplified example of the Salary API's pom.xml:**

```xml
<project>
    <modelVersion>4.0.0</modelVersion>

    <!-- Project identity -->
    <groupId>com.opstree.microservice</groupId>
    <artifactId>salary</artifactId>
    <version>0.1.0-RELEASE</version>
    <packaging>jar</packaging>

    <!-- Parent: inherits Spring Boot defaults -->
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.7.0</version>
    </parent>

    <!-- Dependencies: what libraries this project needs -->
    <dependencies>

        <!-- Spring Boot Web (REST API support) -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>

        <!-- Spring Data Cassandra (ScyllaDB/Cassandra support) -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-cassandra</artifactId>
        </dependency>

        <!-- JUnit for testing -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>

    </dependencies>

    <!-- Build plugins -->
    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

</project>
```

Each `<dependency>` block tells Maven: "I need this library." Maven handles downloading it, finding its own dependencies, and adding everything to the classpath.

### 4.4 Transitive Dependency Resolution

This is one of Maven's most powerful features. When you declare a dependency, Maven automatically resolves that library's dependencies — and their dependencies — recursively.

**Example:**
You declare `spring-boot-starter-web`. Maven automatically resolves and downloads:
- `spring-webmvc`
- `spring-core`
- `spring-context`
- `jackson-databind` (JSON parsing)
- `tomcat-embed-core` (embedded web server)
- ...and dozens more

You declared 1 dependency. Maven resolved ~50. Without this, you would need to manually track and download every transitive dependency yourself.

### 4.5 Dependency Scopes

Not all dependencies are needed in all situations. Maven uses **scopes** to control when a dependency is available:

| Scope | Available During | Example Use Case |
|-------|-----------------|------------------|
| `compile` (default) | Compile, test, runtime | Core application libraries |
| `test` | Test only | JUnit, Mockito — not included in final JAR |
| `provided` | Compile and test only | Servlet API (provided by the app server at runtime) |
| `runtime` | Test and runtime only | JDBC drivers — not needed at compile time |

### 4.6 Plugins

Maven's functionality is extended through **plugins**. Every phase in the lifecycle is actually executed by a plugin. Some important plugins:

| Plugin | Purpose |
|--------|---------|
| `maven-compiler-plugin` | Controls Java version for compilation |
| `spring-boot-maven-plugin` | Packages Spring Boot apps into executable fat JARs |
| `maven-surefire-plugin` | Runs unit tests during the `test` phase |
| `maven-jar-plugin` | Controls how the JAR file is created |
| `jacoco-maven-plugin` | Generates code coverage reports |

### 4.7 Multi-Module Projects

Maven supports **multi-module projects** — a single parent `pom.xml` that manages multiple sub-projects (modules). Each module has its own `pom.xml` but inherits common configuration from the parent.

This is common in large enterprise applications where you have separate modules for `core`, `api`, `service`, and `repository` layers.

---

## 5. Local Repository and Remote Repository

Understanding how Maven stores and retrieves dependencies is essential for diagnosing build failures and working in environments without internet access.

### 5.1 How Maven Finds Dependencies

When Maven encounters a `<dependency>` in `pom.xml`, it follows this lookup order:

```
1. Check Local Repository (~/.m2/repository)
        │
        ├── Found? → Use it immediately (no network needed)
        │
        └── Not Found?
                │
                ▼
        2. Check Remote Repository (Maven Central or configured repo)
                │
                ├── Found? → Download it → Store in Local Repo → Use it
                │
                └── Not Found? → BUILD FAILURE: dependency not found
```

### 5.2 Local Repository

The **local repository** is a folder on your own machine where Maven caches every dependency it has ever downloaded.

| Attribute | Detail |
|-----------|--------|
| **Default Location** | `~/.m2/repository/` (home directory) |
| **Purpose** | Cache downloaded JARs so they are not re-downloaded on every build |
| **Structure** | Mirrors the `groupId/artifactId/version` structure of `pom.xml` |
| **Populated By** | Maven automatically on first build, or via `mvn install` for local projects |

**Directory structure example:**

```
~/.m2/repository/
└── org/
    └── springframework/
        └── boot/
            └── spring-boot-starter-web/
                └── 2.7.0/
                    ├── spring-boot-starter-web-2.7.0.jar
                    ├── spring-boot-starter-web-2.7.0.pom
                    └── spring-boot-starter-web-2.7.0.jar.sha1
```

**Important behaviors:**

- On the **first build** of a project on a new machine, Maven downloads all dependencies — this can take several minutes and requires internet access
- On **subsequent builds**, Maven uses the cached JARs from `~/.m2` — builds are fast and work offline
- Running `mvn install` on your own project places its JAR into `~/.m2`, making it available to other local projects that depend on it
- The local repo can be cleared with `rm -rf ~/.m2/repository` to force a full re-download (useful for fixing corrupted cache)

### 5.3 Remote Repository

The **remote repository** is a server on the internet (or your company's internal network) that hosts Maven artifacts. When a dependency is not in the local repository, Maven downloads it from a remote repository.

#### 5.3.1 Maven Central

**Maven Central** is the default, official remote repository for the Java ecosystem.

| Attribute | Detail |
|-----------|--------|
| **URL** | https://repo.maven.apache.org/maven2 |
| **Maintained By** | Sonatype on behalf of the Maven community |
| **Contents** | Virtually every open-source Java library ever published |
| **Access** | Public, no authentication required |
| **Usage** | Maven uses it automatically — no configuration needed |

When you declare `spring-boot-starter-web` in your `pom.xml`, Maven downloads it from Maven Central without any additional configuration.

#### 5.3.2 Other Public Remote Repositories

Some libraries are not on Maven Central and require additional repository configuration:

| Repository | URL | Common Use |
|------------|-----|-----------|
| **Spring Releases** | https://repo.spring.io/release | Spring milestone and release builds |
| **JBoss Repository** | https://repository.jboss.org | JBoss and WildFly libraries |
| **Google Android** | https://maven.google.com | Android libraries |
| **Sonatype Snapshots** | https://oss.sonatype.org/content/repositories/snapshots | Snapshot (pre-release) builds |

To use a non-Central repository, declare it in `pom.xml`:

```xml
<repositories>
    <repository>
        <id>spring-releases</id>
        <url>https://repo.spring.io/release</url>
    </repository>
</repositories>
```

#### 5.3.3 Private / Internal Remote Repository

In enterprise environments, companies host their **own internal Maven repository** using tools like **Nexus Repository Manager** or **JFrog Artifactory**. This serves several purposes:

| Purpose | Explanation |
|---------|-------------|
| **Security** | Vet and approve libraries before they enter the company's builds |
| **Availability** | Builds don't fail if Maven Central is down or slow |
| **Private artifacts** | Store proprietary internal JARs that can't be published to Maven Central |
| **Proxy and cache** | Act as a proxy for Maven Central — download once, serve internally forever |
| **Air-gapped environments** | Build servers with no internet access pull from the internal repo instead |

```
Developer Machine
      │  mvn install
      ▼
Internal Nexus/Artifactory (company network)
      │  not cached? fetch from Maven Central
      ▼
Maven Central (internet)
```

To configure Maven to use an internal repository, you edit `~/.m2/settings.xml`:

```xml
<settings>
    <mirrors>
        <mirror>
            <id>internal-nexus</id>
            <mirrorOf>central</mirrorOf>
            <url>http://nexus.company.internal/repository/maven-public/</url>
        </mirror>
    </mirrors>
    <servers>
        <server>
            <id>internal-nexus</id>
            <username>your-username</username>
            <password>your-password</password>
        </server>
    </servers>
</settings>
```

### 5.4 Repository Summary

```
pom.xml declares:
  <dependency> spring-boot-starter-web 2.7.0

Maven checks:
  1. ~/.m2/repository/org/springframework/boot/spring-boot-starter-web/2.7.0/
        └── EXISTS? → Use cached JAR ✅

  2. Not found locally → query Remote Repository
        ├── Maven Central (default)
        ├── Configured repos in pom.xml
        └── Internal Nexus/Artifactory (if settings.xml configured)
              └── Found? → Download → Cache in ~/.m2 → Use ✅
              └── Not Found? → BUILD FAILURE ❌
```

---

## 6. Maven in OT-Microservices

In the OT-Microservices project, Maven is used exclusively to build the **Salary API** (Java Spring Boot).

### 6.1 Project Structure

```
salary-api/
├── pom.xml                                      ← Maven project definition
├── src/
│   └── main/
│       ├── java/com/opstree/microservice/salary/
│       │   ├── SalaryApplication.java           ← Entry point
│       │   ├── contollers/                      ← REST controllers
│       │   ├── model/                           ← Data model (Employee.java)
│       │   ├── repository/                      ← Spring Data repositories
│       │   └── service/                         ← Business logic
│       └── resources/
│           └── application.yml                  ← DB config, server port
└── target/
    └── salary-0.1.0-RELEASE.jar                 ← Built by Maven
```

### 6.2 The Build Command

```bash
cd ~/salary-api

# Clean previous build artifacts, compile, test, and package
# -DskipTests: skip tests because they require a live ScyllaDB connection
mvn clean install -DskipTests
```

| Part | Meaning |
|------|---------|
| `clean` | Delete the `target/` directory — start from zero |
| `install` | Run the full lifecycle: compile → test → package → install to `~/.m2` |
| `-DskipTests` | Skip the test phase (tests need a running database) |

### 6.3 Running the Built Artifact

Maven packages the Salary API as an **executable fat JAR** — a single `.jar` file containing the application code, all dependencies, and an embedded Tomcat server.

```bash
# Run the packaged JAR directly — no application server needed
nohup java -jar target/salary-0.1.0-RELEASE.jar > ~/salary.log 2>&1 &
```

This works because the `spring-boot-maven-plugin` in `pom.xml` packages everything into one self-contained file.

### 6.4 What Maven Downloads for the Salary API

On first build, Maven downloads all declared dependencies into `~/.m2`. Key ones for the Salary API:

| Dependency | Purpose |
|------------|---------|
| `spring-boot-starter-web` | REST API support with embedded Tomcat |
| `spring-boot-starter-data-cassandra` | ScyllaDB/Cassandra integration |
| `spring-boot-starter-actuator` | Health check endpoints (`/actuator/health`) |
| `spring-boot-starter-test` | JUnit and Mockito for testing |

---

## 7. Conclusion

Maven brings order, reproducibility, and standardization to Java project builds. By declaring dependencies and project metadata in `pom.xml`, developers eliminate the manual, error-prone work of managing libraries and build steps.

Key takeaways:

- Maven is a **declarative build tool** — describe what your project needs, not how to build it
- The **`pom.xml`** is the single source of truth for dependencies, plugins, and build configuration
- **Transitive dependency resolution** means you declare one library and Maven downloads its entire dependency tree
- The **local repository** (`~/.m2`) caches downloaded JARs so builds are fast and work offline after the first run
- **Maven Central** is the default public remote repository — virtually every open-source Java library is there
- **Internal repositories** (Nexus, Artifactory) are used in enterprise environments for security, caching, and private artifacts
- In OT-Microservices, `mvn clean install -DskipTests` builds the Salary API JAR that is run directly with `java -jar`

---

## 8. Contact Information

| Name | Role | Email |
|------|------|-------|
| Deepak | Author | — |

---

## 9. References

| Resource | Link |
|----------|------|
| Apache Maven Official Documentation | https://maven.apache.org/guides/ |
| Maven Central Repository | https://search.maven.org |
| POM Reference | https://maven.apache.org/pom.html |
| Maven Build Lifecycle | https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html |
| Maven Repository Guide | https://maven.apache.org/guides/introduction/introduction-to-repositories.html |
| Spring Boot Maven Plugin | https://docs.spring.io/spring-boot/docs/current/maven-plugin/reference/htmlsingle/ |
| OT-Microservices Salary API | https://github.com/OT-MICROSERVICES/salary-api |

---

*Author: Deepak | Sprint 0 | OT-Microservices | April 2026*
