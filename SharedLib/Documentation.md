
---

# **Shared Library Documentation (Jenkins)**

| Author        | Created on | Version   | Last updated by | Last edited on | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
| ------------- | ---------- | --------- | --------------- | -------------- | ------------ | ----------- | ----------- | ----------- |
| Gourav Sharma | 20-04-2026 | Version 1 | Gourav Sharma   | 20-04-2026     | Team         |             |             |             |

---

## **Table of Contents**

1. Introduction
2. What is Shared Library?
3. Why Shared Library is Important
4. Structure of Shared Library

   * 4.1 vars (Global Variables)
   * 4.2 src (Reusable Classes)
5. Workflow of Shared Library
6. Advantages
7. Disadvantages
8. Best Practices
9. Conclusion
10. FAQs
11. Contact Information
12. References

---

## **1. Introduction**

In modern DevOps, many projects use similar pipeline steps like build, test, deploy, etc. Writing the same code again and again in Jenkins pipelines is not efficient.

To solve this problem, Jenkins provides **Shared Libraries**, which allow us to reuse pipeline code across multiple projects.

---

## **2. What is Shared Library?**

A **Shared Library in Jenkins** is a reusable collection of Groovy scripts that can be shared across multiple Jenkins pipelines.

It helps to:

* Avoid duplicate code
* Standardize pipeline processes
* Improve maintainability

---

## **3. Why Shared Library is Important**

* Reduces code duplication
* Centralized pipeline logic
* Easy updates (change once, reflect everywhere)
* Improves CI/CD consistency
* Makes pipelines cleaner and shorter

Without shared libraries, pipelines become messy and hard to maintain.

---

## **4. Structure of Shared Library**

A Jenkins Shared Library has a fixed structure:

```
(root)
│
├── vars/
│   └── myFunction.groovy
│
├── src/
│   └── com/example/MyClass.groovy
│
├── resources/
│   └── config.yaml
```

---

### **4.1 vars (Global Variables / Functions)**

* Contains **simple reusable pipeline functions**
* Automatically available in Jenkins pipeline
* Used for **direct calling in Jenkinsfile**

#### Example:

```groovy
// vars/buildApp.groovy
def call() {
    echo "Building Application..."
}
```

#### Usage in Jenkinsfile:

```groovy
@Library('my-shared-lib') _
buildApp()
```

 Key Points:

* No need to import
* Easy to use
* Best for simple logic

---

### **4.2 src (Reusable Classes)**

* Contains **complex logic using Groovy classes**
* Follows **Java package structure**
* Needs to be imported before use

#### Example:

```groovy
// src/com/devops/Deploy.groovy
package com.devops

class Deploy {
    def deployApp() {
        println "Deploying Application..."
    }
}
```

#### Usage in Jenkinsfile:

```groovy
@Library('my-shared-lib') _
import com.devops.Deploy

def obj = new Deploy()
obj.deployApp()
```

 Key Points:

* Used for complex logic
* Supports OOP concepts
* Better structure and scalability

---

## **5. Workflow of Shared Library**

### Step-by-Step Flow:

1. Developer creates shared library repo
2. Adds `vars` and `src` code
3. Pushes code to Git
4. Configure library in Jenkins (Global config)
5. Jenkinsfile loads library using:

```groovy
@Library('library-name') _
```

6. Pipeline calls functions from `vars` or `src`
7. Jenkins executes reusable logic

---

## **6. Advantages**

* Code reusability
* Centralized management
* Cleaner Jenkinsfile
* Easy maintenance
* Promotes DevOps best practices
* Scalable for large projects

---

## **7. Disadvantages**

* Initial setup is complex
* Requires Groovy knowledge
* Debugging can be difficult
* Tight coupling if not designed properly

---

## **8. Best Practices**

* Keep functions small and reusable
* Use `vars` for simple logic, `src` for complex logic
* Follow proper naming conventions
* Maintain versioning of library
* Write documentation for each function
* Avoid hardcoding values
* Use parameters for flexibility
* Test library code before production

---

## **9. Conclusion**

Shared Libraries in Jenkins are a powerful way to **standardize CI/CD pipelines** and **reduce duplication**.

* Use **vars** → for simple reusable functions
* Use **src** → for complex and structured logic

By using shared libraries properly, teams can build **scalable, maintainable, and clean pipelines**.

---

## **10. FAQs**

**Q1. What is Jenkins Shared Library?**
Reusable pipeline code used across multiple projects.

**Q2. Difference between vars and src?**

* vars → simple functions
* src → complex classes

**Q3. When to use vars?**
When logic is simple and directly used in pipeline.

**Q4. When to use src?**
When logic is complex and requires structure.

---

## **11. Contact Information**

| Name          | Email ID                                                      |
| ------------- | ------------------------------------------------------------- |
| Gourav Sharma | [gourav.sharma.snaatak@mygurukulam.co](mailto:gourav.sharma.snaatak@mygurukulam.co) |

---

## **12. References**

| Link                                                                                                                     | Description           |
| ------------------------------------------------------------------------------------------------------------------------ | --------------------- |
| [https://www.jenkins.io/doc/book/pipeline/shared-libraries/](https://www.jenkins.io/doc/book/pipeline/shared-libraries/) | Jenkins Official Docs |
| [https://www.geeksforgeeks.org/jenkins-shared-library/](https://www.geeksforgeeks.org/jenkins-shared-library/)           | Shared Library Guide  |
| [https://www.jenkins.io/doc/book/pipeline/](https://www.jenkins.io/doc/book/pipeline/)                                   | Jenkins Pipeline Docs |

---



