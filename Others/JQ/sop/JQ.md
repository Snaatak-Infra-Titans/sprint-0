# SOP: Common Stack | Others | JQ | SOP for JQ

---

## Author Table

| **Author** | **Created on** | **Version** | **Last updated by** | **Last Edited On** | **Pre Reviewer** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ---------- | -------------- | ----------- | ------------------- | ------------------ | ---------------- | --------------- | --------------- | --------------- |
| Ankita     | 15-04-2026     | v1.0        | Ankita              | 15-04-2026         | Team             |                 |                 |                 |

---

## Table of Contents

1. [Overview](#overview)

2. [Purpose](#purpose)

3. [Prerequisites](#prerequisites)

4. [What is JQ?](#what-is-jq)

5. [Step-by-Step Implementation](#step-by-step-implementation)

6. [Common Operations](#common-operations)

7. [Working with Files](#working-with-files)

8. [Troubleshooting](#troubleshooting)

9. [Best Practices](#best-practices)

10. [FAQs](#faqs)

11. [Contact Information](#contact-information)

12. [References](#references)

13. [Introduction](#introduction)

14. [Purpose](#purpose)

15. [What is JQ?](#what-is-jq)

16. [Why JQ is Used](#why-jq-is-used)

17. [Basic Syntax](#basic-syntax)

18. [Core Concepts](#core-concepts)

19. [Common Operations](#common-operations)

20. [Working with Files](#working-with-files)

21. [Pipelines and Filters](#pipelines-and-filters)

22. [Troubleshooting](#troubleshooting)

23. [Best Practices](#best-practices)

24. [FAQs](#faqs)

25. [Contact Information](#contact-information)

26. [References](#references)

---

## Overview

JQ is a lightweight and powerful command-line tool used to process and manipulate JSON data.

It is commonly used in DevOps, automation scripts, and API handling where JSON is the standard data format.

JQ allows users to parse, filter, transform, and extract data from JSON files efficiently.

---

## Prerequisites

* Linux/Ubuntu system
* Basic command-line knowledge
* JQ installed on system

Install JQ:

```bash
sudo apt install jq
```

---

## What is JQ?

JQ is a lightweight and powerful command-line tool used to process and manipulate JSON data.

It is commonly used in DevOps, automation scripts, and API handling where JSON is the standard data format.

JQ allows users to parse, filter, transform, and extract data from JSON files efficiently.

---

## Purpose

This SOP provides a step-by-step guide to using JQ for processing JSON data.

It helps users understand how to extract, filter, and manipulate JSON efficiently in DevOps and automation workflows.

---

## What is JQ?

JQ is a JSON processor that works like `sed` or `awk`, but specifically for JSON data.

It allows users to:

* Extract specific fields from JSON
* Transform JSON structure
* Filter and query JSON data

---

## Why JQ is Used

JQ is widely used because:

* JSON is the standard format for APIs
* Easy to integrate in shell scripts
* Fast and lightweight
* Powerful filtering capabilities

---

## Basic Syntax

General format:

```bash
jq 'filter' file.json
```

Example:

```bash
jq '.name' file.json
```

---

## Step-by-Step Implementation

### Step 1: Read JSON File

```bash
jq '.' file.json
```

---

### Step 2: Extract Specific Field

```bash
jq '.name' file.json
```

---

### Step 3: Access Array Elements

```bash
jq '.skills[0]' file.json
```

---

### Step 4: Iterate Over Array

```bash
jq '.skills[]' file.json
```

---

### Step 5: Filter Data

```bash
jq '.users[] | select(.age > 25)' file.json
```

---

## Common Operations

### Extract Field

```bash
jq '.name' file.json
```

### Pretty Print JSON

```bash
jq '.' file.json
```

### Filter Data

```bash
jq '.users[] | select(.age > 25)' file.json
```

### Count Elements

```bash
jq '.users | length' file.json
```

---

## Working with Files

Read JSON file:

```bash
jq '.' data.json
```

Write output to file:

```bash
jq '.name' data.json > output.txt
```

---

## Pipelines and Filters

JQ supports chaining operations:

```bash
jq '.users[] | .name' file.json
```

This allows step-by-step transformation of JSON data.

---

## Troubleshooting

| Issue              | Cause                 | Solution         |
| ------------------ | --------------------- | ---------------- |
| Invalid JSON error | Incorrect JSON format | Validate JSON    |
| No output          | Wrong filter          | Check query path |
| Command not found  | JQ not installed      | Install jq       |

---

## Best Practices

* Always validate JSON before processing
* Use quotes properly in filters
* Test queries on small data first
* Use JQ in scripts for automation
* Keep commands readable and simple

---

## FAQs

**Q1: What is JQ used for?**
It is used to process and manipulate JSON data.

**Q2: Is JQ only for files?**
No, it can also process API responses.

**Q3: Is JQ fast?**
Yes, it is lightweight and efficient.

**Q4: Can JQ modify JSON?**
Yes, it can transform JSON structures.

---

## Contact Information

| Name   | Email                                                                             |
| ------ | --------------------------------------------------------------------------------- |
| Ankita | [ankita.singh.snaatak@mygurukulam.co](mailto:ankita.singh.snaatak@mygurukulam.co) |

---

## References

| Topic              | Link                                                                   |
| ------------------ | ---------------------------------------------------------------------- |
| JQ Official Docs   | [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/)       |
| JSON Documentation | [https://www.json.org/json-en.html](https://www.json.org/json-en.html) |
