# SOP: Common Stack | Others | JQ | SOP for JQ

---

## Author Table

| **Author** | **Created on** | **Version** | **Last updated by** | **Last Edited On** | **Pre Reviewer** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ---------- | -------------- | ----------- | ------------------- | ------------------ | ---------------- | --------------- | --------------- | --------------- |
| Ankita     | 15-04-2026     | v1.1        | Ankita              | 22-04-2026         | Team             | Komal Jaiswal   | Akshit Kapil    | Mahesh Kumar    |

---

## Table of Contents

1. [Overview](#overview)
2. [Purpose](#purpose)
3. [Prerequisites](#prerequisites)
4. [Step-by-Step Implementation](#step-by-step-implementation)
5. [Common Operations](#common-operations)
6. [Validation](#validation)
7. [Troubleshooting](#troubleshooting)
8. [Best Practices](#best-practices)
9. [Contact Information](#contact-information)
10. [References](#references)

---

## Overview

JQ is a lightweight command-line tool used to process and manipulate JSON data.

It is widely used in DevOps workflows for handling API responses, configuration files, and automation scripts.

---

## Purpose

This SOP provides a step-by-step procedure to use JQ for reading, filtering, and transforming JSON data.

Note: Please follow the link to learn more about JQ:  
[JQ Documentation](https://github.com/Snaatak-Infra-Titans/sprint-0/blob/SCRUM-4O-versha/Others/JQ/Documentation/Intro.md)

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
<img width="866" height="497" alt="image" src="https://github.com/user-attachments/assets/e5619fbb-720a-4648-bda3-036528f61ba9" />
<img width="866" height="497" alt="image" src="https://github.com/user-attachments/assets/370079b9-5d43-438d-9975-c17a5dbe8aca" />
---

## Step-by-Step Implementation

### Step 0: Verify Installation

```bash
jq --version
```
<img width="866" height="167" alt="image" src="https://github.com/user-attachments/assets/d022c0b3-65ef-4d5b-a78c-baeb78843f9e" />

---

### Step 1: Read JSON File

```bash
jq '.' file.json
```
<img width="866" height="563" alt="image" src="https://github.com/user-attachments/assets/53e9ec00-9592-4cc3-beb1-9cfb5fe1535d" />

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
<img width="866" height="409" alt="image" src="https://github.com/user-attachments/assets/37cf796d-3ca2-431d-9dc8-4e01db868fff" />

---

## Common Operations

### Pretty Print JSON

```bash
jq '.' file.json
```
<img width="866" height="563" alt="image" src="https://github.com/user-attachments/assets/d653578c-c257-4537-a101-ac5aa3564eec" />

### Count Elements

```bash
jq '.users | length' file.json
```

### Extract Multiple Fields

```bash
jq '.users[] | {name, age}' file.json
```
<img width="866" height="387" alt="image" src="https://github.com/user-attachments/assets/53f3827d-aabd-49eb-9693-88fac0b0f74b" />

---

## Validation

Verify output correctness:

```bash
jq '.name' file.json
```
<img width="866" height="167" alt="image" src="https://github.com/user-attachments/assets/a4a57761-d2a3-4ad5-a820-44e9659d9747" />

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
