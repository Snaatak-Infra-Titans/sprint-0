# JQ Intro Documentation

## Document Information

| Author          | Created On | Version | L0 Reviewer  | L1 Reviewer  | L2 Reviewer     |
| --------------- | ---------- | ------- | ------------ | ------------ | --------------- |
| Versha Tripathi | 13-04-2026 | v1.0    | Prince Batra | Nikita Joshi | Piyush Upadhyay |


---





## Table of Contents

* [What is JQ?](#what-is-jq)
* [Why JQ?](#why-jq)
* [Key Features](#key-features)
* [Built-in Functions](#built-in-functions)
* [Conclusion](#conclusion)
* [Contact Information](#contact-information)
* [References](#references)

---

## What is JQ?

**jq** is a lightweight command-line tool used to **parse, filter, and transform JSON data**.

It works like a pipeline:

* Takes JSON as input
* Applies a filter
* Outputs the result
* Written in C
* Single binary (no dependencies)
* Works on Linux, macOS, and Windows

---

## Why JQ?

Many modern tools and APIs return JSON. Without jq, extracting data can be slow and complex.

### Without jq:

* Requires writing a script (e.g., Python) to parse JSON
* Involves importing libraries and handling input manually
* Longer and more complex command for simple tasks
* Less readable and harder to use in quick CLI operations

### With jq:

* Directly extracts data using simple filters
* No need for additional scripting or setup
* Short, clean, and easy-to-read commands
* Faster and more efficient for command-line usage

### Where jq is useful:

* API responses (`curl`)
* Logs (JSON logs)
* CI/CD pipelines
* Kubernetes (`kubectl`)
* AWS CLI outputs
* Automation scripts

---

## Key Features

### 1. Access Fields

Extract specific values from JSON using keys.

### 2. Work with Arrays

Retrieve, slice, or loop through array elements easily.

### 3. Use Pipes

Chain multiple operations step-by-step for cleaner data processing.

### 4. Create New JSON

Build custom JSON structures from existing data.

### 5. Filter Data

Select only the data that meets certain conditions.

### 6. Transform Arrays

Modify or apply operations to all elements in an array.

### 7. Conditions

Apply logic (if-else) to control output based on values.

### 8. Format Output

Display JSON in readable, compact, or raw formats as needed.



---




## Conclusion

**jq** is a simple yet powerful tool that makes working with JSON much easier directly from the command line. Instead of writing long scripts, you can quickly extract, filter, and transform data using short and readable commands.

For beginners, starting with basic filters like field access and `select()` is enough to handle most everyday tasks. As you practice more, jq becomes an essential tool for **DevOps, automation, and data processing workflows**.



---
## Contact Information

| Name            | Email                                                                                   |
| :-------------- | :-------------------------------------------------------------------------------------- |
| Versha Tripathi | [versha.tripathi.snaatak@mygurukulam.co](mailto:versha.tripathi.snaatak@mygurukulam.co) |

---



## References

* jq Official Website: [https://jqlang.github.io/jq/](https://jqlang.github.io/jq/)
* jq Manual: [https://jqlang.github.io/jq/manual/](https://jqlang.github.io/jq/manual/)
* GitHub Repo: [https://github.com/jqlang/jq](https://github.com/jqlang/jq)
* Playground: [https://jqplay.org/](https://jqplay.org/)

---

<div align="center"></div>
