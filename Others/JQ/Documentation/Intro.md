<div align="center">

# JQ — Command-Line JSON Processor

### *Common Stack · Others · JQ · Intro Documentation*

> *A lightweight, zero-dependency tool to slice, filter, map and transform JSON — right from your terminal.*

![Platform](https://img.shields.io/badge/Platform-Linux%20%7C%20macOS%20%7C%20Windows-blue?style=flat-square)
![Language](https://img.shields.io/badge/Written%20in-C-lightgrey?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)
![Version](https://img.shields.io/badge/Doc%20Version-v1.0-orange?style=flat-square)

</div>

---

## Document Information

| Author | Created On | Version | Last Updated By | Last Edited On | PRE Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|:---|:---|:---:|:---|:---|:---:|:---:|:---:|:---:|
| Versha Tripathi | 13-04-2026 | v1.0 | Versha Tripathi | 13-04-2026 | Team | — | — | — |

---

## Table of Contents

- [What is JQ?](#what-is-jq)
- [Why JQ?](#why-jq)
- [Key Features](#key-features)
- [Built-in Functions](#built-in-functions)
- [Contact Information](#contact-information)
- [References](#references)

---

## What is JQ?

**jq** is a lightweight, zero-dependency, command-line tool for **parsing, filtering, and transforming JSON data**. It works as a stream processor — reading JSON as input, applying a filter expression, and writing transformed JSON as output.

> Think of jq as the **`sed`, `awk`, and `grep` of JSON** — a sharp, composable tool that slots naturally into any Unix pipeline.

```bash
curl -s https://api.example.com/users/1 | jq '.name'
```

jq is written in portable C, ships as a **single binary**, and runs on Linux, macOS, and Windows with no runtime dependencies.

---

## Why JQ?

Modern infrastructure, APIs, and tooling produce JSON constantly — from REST APIs and log files to CLI outputs from `kubectl`, `aws`, `docker`, and `terraform`. **jq brings JSON manipulation directly to the shell.**

| Without JQ | With JQ |
|:---|:---|
| `python3 -c "import json,sys; d=json.load(sys.stdin); print(d['status'])"` | `jq '.status'` |
| Parse → script → print, every time | Filter inline, in a pipeline |
| Context switch to an editor or REPL | Stay in the terminal |

**Common real-world use cases:**

| Use Case | Description |
|:---|:---|
| Querying API responses | Extract specific fields from `curl` or `httpie` output |
| Log analysis | Filter structured JSON logs from Nginx, Fluentd, CloudWatch |
| CI/CD pipelines | Parse deployment outputs, extract image tags, check health status |
| Infrastructure tooling | Process `kubectl get pods -o json`, `aws ec2 describe-instances` |
| Data transformation | Reshape JSON before piping into another tool or file |
| Scripting & automation | Replace verbose inline Python with readable jq expressions |

---

## Key Features

### 1. Identity & Field Access
Extract any field or nested value using simple dot notation.
```bash
echo '{"user": {"name": "Alice", "age": 30}}' | jq '.user.name'
# Output: "Alice"
```

### 2. Array Iteration & Slicing
Iterate over arrays or access elements by index.
```bash
echo '[1, 2, 3, 4, 5]' | jq '.[2]'       # single element → 3
echo '[1, 2, 3, 4, 5]' | jq '.[1:4]'     # slice → [2, 3, 4]
echo '[{"id":1},{"id":2}]' | jq '.[].id' # iterate → 1, 2
```

### 3. Pipes & Composition
Chain filters together using `|` — the same mental model as Unix pipes.
```bash
echo '{"items": [{"name": "foo"}, {"name": "bar"}]}' \
  | jq '.items | .[0] | .name'
# Output: "foo"
```

### 4. Object & Array Construction
Build new JSON structures from existing data.
```bash
echo '{"first": "John", "last": "Doe"}' \
  | jq '{fullName: (.first + " " + .last)}'
# Output: {"fullName": "John Doe"}
```

### 5. Filtering with `select`
Keep only the records that match a condition.
```bash
echo '[{"name":"Alice","age":30},{"name":"Bob","age":17}]' \
  | jq '[.[] | select(.age >= 18)]'
# Output: [{"name": "Alice", "age": 30}]
```

### 6. `map` for Array Transformation
Apply a transformation to every element in an array.
```bash
echo '[1, 2, 3, 4]' | jq 'map(. * 2)'
# Output: [2, 4, 6, 8]
```

### 7. Conditional Logic
jq supports `if / then / else / end` expressions for branching.
```bash
echo '{"score": 72}' \
  | jq 'if .score >= 60 then "pass" else "fail" end'
# Output: "pass"
```

### 8. String Interpolation
Embed values inside strings using `\(expr)` syntax.
```bash
echo '{"name": "Alice", "lang": "Go"}' \
  | jq '"Hello, \(.name)! You are writing \(.lang)."'
# Output: "Hello, Alice! You are writing Go."
```

### 9. Pretty-print & Compact Output
Control output formatting for both human reading and downstream tooling.
```bash
cat data.json | jq '.'        # pretty-print (default)
cat data.json | jq -c '.'     # compact, single-line output
cat data.json | jq -r '.name' # raw output (strips JSON string quotes)
```

### 10. Reading from Files & Multiple Inputs
jq can read directly from files and process multiple JSON documents in a single invocation.
```bash
jq '.status' response.json                  # read from file
jq -s '.[0].name, .[1].name' a.json b.json  # slurp multiple files into an array
```

### 11. Recursive Descent
The `..` operator recursively walks every node in a JSON tree — useful for deeply nested structures.
```bash
echo '{"a":{"b":{"c": 42}}}' | jq '.. | numbers'
# Output: 42
```

---

## Built-in Functions

| Function | Description |
|:---|:---|
| `keys` | Returns object keys as an array |
| `values` | Returns object values as an array |
| `length` | Length of a string, array, or object |
| `map(f)` | Applies filter `f` to every array element |
| `select(f)` | Keeps only elements where `f` is true |
| `has("key")` | Checks if an object has a given key |
| `type` | Returns the JSON type of the input |
| `sort` / `sort_by(f)` | Sorts arrays, optionally by a key |
| `group_by(f)` | Groups array elements by a computed key |
| `unique` / `unique_by(f)` | Deduplicates array elements |
| `to_entries` / `from_entries` | Converts between object and `[{key, value}]` form |
| `add` | Sums or concatenates all array elements |
| `del(path)` | Removes a field from an object |
| `env` | Exposes environment variables as a JSON object |

---

## Contact Information

| Name | Email |
|:---|:---|
| Versha Tripathi | [versha.tripathi.snaatak@mygurukulam.co](mailto:versha.tripathi.snaatak@mygurukulam.co) |

---

## References

| # | Resource | Link |
|:---:|:---|:---|
| 1 | jq Official Website | [jqlang.github.io/jq](https://jqlang.github.io/jq/) |
| 2 | jq Manual (latest) | [jqlang.github.io/jq/manual](https://jqlang.github.io/jq/manual/) |
| 3 | jq GitHub Repository | [github.com/jqlang/jq](https://github.com/jqlang/jq) |
| 4 | jq Playground (try online) | [jqplay.org](https://jqplay.org/) |

---

<div align="center">

*Documentation maintained by the Common Stack Team · v1.0 · 13-04-2026*

</div>
