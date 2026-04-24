# JQ — Command-Line JSON Processor

## Document Information

| Author          | Created On | Version | L0 Reviewer  | L1 Reviewer  | L2 Reviewer     |
| --------------- | ---------- | ------- | ------------ | ------------ | --------------- |
| Versha Tripathi | 13-04-2026 | v1.0    | Prince Batra | Nikita Joshi | Piyush Upadhyay |


---

## Introduction

If you’ve ever worked with APIs, logs, or tools like `kubectl`, `aws`, or `docker`, you’ve probably seen **JSON data everywhere**. But reading or extracting useful information from raw JSON can be messy.

That’s where **jq** helps.

It lets you quickly **pick, filter, and reshape JSON data directly in your terminal**, without writing long scripts. Even simple commands can save a lot of time and effort.

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

> Think of jq as the **`grep` or `awk` for JSON**.

```bash
curl -s https://api.example.com/users/1 | jq '.name'
```

* Written in C
* Single binary (no dependencies)
* Works on Linux, macOS, and Windows

---

## Why JQ?

Many modern tools and APIs return JSON. Without jq, extracting data can be slow and complex.

### Without jq

```bash
python3 -c "import json,sys; d=json.load(sys.stdin); print(d['status'])"
```

### With jq

```bash
jq '.status'
```

### Where jq is useful:

* API responses (`curl`)
* Logs (JSON logs)
* CI/CD pipelines
* Kubernetes (`kubectl`)
* AWS CLI outputs
* Automation scripts

---

## Key Features (Simplified)

### 1. Access Fields

```bash
jq '.user.name'
```

### 2. Work with Arrays

```bash
jq '.[0]'      # first element  
jq '.[1:3]'    # slice  
jq '.[].id'    # loop
```

### 3. Use Pipes

```bash
jq '.items | .[0] | .name'
```

### 4. Create New JSON

```bash
jq '{fullName: (.first + " " + .last)}'
```

### 5. Filter Data

```bash
jq '.[] | select(.age > 18)'
```

### 6. Transform Arrays

```bash
jq 'map(. * 2)'
```

### 7. Conditions

```bash
jq 'if .score > 50 then "pass" else "fail" end'
```

### 8. Format Output

```bash
jq '.'   # pretty  
jq -c    # compact  
jq -r    # raw
```

---

## Built-in Functions (Quick View)

| Function     | Purpose           |
| :----------- | :---------------- |
| `length`     | Count items       |
| `keys`       | Get object keys   |
| `map()`      | Modify arrays     |
| `select()`   | Filter data       |
| `sort_by()`  | Sort values       |
| `unique`     | Remove duplicates |
| `has("key")` | Check key exists  |
| `type`       | Show data type    |
| `add`        | Sum values        |
| `del()`      | Remove fields     |

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
