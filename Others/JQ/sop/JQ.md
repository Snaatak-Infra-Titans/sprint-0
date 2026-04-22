# SOP: Common Stack | Others | JQ | SOP for JQ

---

## Author Table

| **Author** | **Created on** | **Version** | **Last updated by** | **Last Edited On** | **Pre Reviewer** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ---------- | -------------- | ----------- | ------------------- | ------------------ | ---------------- | --------------- | --------------- | --------------- |
| Ankita     | 15-04-2026     | v1.1        | Ankita              | 22-04-2026         | Team             | Komal Jaiswal   | Akshit Kapil    | Mahesh Kumar    |

---

## Table of Contents

1. Overview
2. Purpose
3. Prerequisites
4. Step-by-Step Implementation
5. Common Operations
6. Validation
7. Troubleshooting
8. Best Practices
9. Contact Information
10. References

---

## Overview

JQ is a lightweight command-line tool used to process and manipulate JSON data.

It is widely used in DevOps workflows for handling API responses, configuration files, and automation scripts.

---

## Purpose

This SOP provides a step-by-step procedure to use JQ for reading, filtering, and transforming JSON data.

---

## Prerequisites

* Linux/Ubuntu system
* Basic command-line knowledge
* JQ installed

Install JQ:

```bash
sudo apt update
sudo apt install jq -y
```

---

## Step-by-Step Implementation

### Step 0: Verify Installation

```bash
jq --version
```

---

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

### Pretty Print JSON

```bash
jq '.' file.json
```

### Count Elements

```bash
jq '.users | length' file.json
```

### Extract Multiple Fields

```bash
jq '.users[] | {name, age}' file.json
```

---

## Validation

Verify output correctness:

```bash
jq '.name' file.json
```

Expected Result:

* Correct field value should be displayed
* No syntax errors

---

## Troubleshooting

| Issue              | Cause                 | Solution      |
| ------------------ | --------------------- | ------------- |
| Invalid JSON error | Incorrect JSON format | Validate JSON |
| No output          | Wrong filter          | Check query   |
| Command not found  | JQ not installed      | Install jq    |

---

## Best Practices

* Validate JSON before processing
* Keep filters simple and readable
* Test commands on sample data
* Use JQ in automation scripts

---

## Contact Information

| Name   | Email                                                                             |
| ------ | --------------------------------------------------------------------------------- |
| Ankita | [ankita.singh.snaatak@mygurukulam.co](mailto:ankita.singh.snaatak@mygurukulam.co) |

---

## References

| Topic            | Link                                                                   |
| ---------------- | ---------------------------------------------------------------------- |
| JQ Official Docs | [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/)       |
| JSON Docs        | [https://www.json.org/json-en.html](https://www.json.org/json-en.html) |
