# Common Stack | Others | JQ | JQ Intro Documentation

> A lightweight, command-line JSON processor — slice it, filter it, map it, transform it.

---

## Table of Contents

- [What is JQ?](#what-is-jq)
- [Why JQ?](#why-jq)
- [Key Features](#key-features)

---

## What is JQ?

**jq** is a lightweight, zero-dependency, command-line tool for parsing, filtering, and transforming **JSON data**. It works as a stream processor — reading JSON as input, applying a filter expression, and writing transformed JSON as output.

Think of jq as the **`sed`, `awk`, and `grep` of JSON** — a sharp, composable tool that slots naturally into any Unix pipeline.

```bash
# Extract a single field from a JSON response
curl -s https://api.example.com/users/1 | jq '.name'
```

jq is written in portable C, ships as a single binary, and runs on Linux, macOS, and Windows with no runtime dependencies.

---

## Why JQ?

Modern infrastructure, APIs, and tooling produce JSON constantly — from REST APIs and log files to CLI outputs from tools like `kubectl`, `aws`, `docker`, and `terraform`. Without jq, working with this data at the terminal requires either verbose Python/Node one-liners or importing data into a full application just to extract a value.

**jq solves this by bringing JSON manipulation to the shell.**

| Without JQ | With JQ |
|---|---|
| `python3 -c "import json,sys; d=json.load(sys.stdin); print(d['status'])"` | `jq '.status'` |
| Parse → script → print, every time | Filter inline, in a pipeline |
| Context switch to an editor or REPL | Stay in the terminal |

### Common real-world use cases:

- **Querying API responses** — extract specific fields from `curl` or `httpie` output
- **Log analysis** — filter and format structured JSON logs (e.g. from Nginx, Fluentd, or CloudWatch)
- **CI/CD pipelines** — parse deployment outputs, extract image tags, check health statuses
- **Infrastructure tooling** — process `kubectl get pods -o json`, `aws ec2 describe-instances`, `terraform output -json`
- **Data transformation** — reshape JSON before piping it into another tool or writing it to a file
- **Scripting & automation** — replace verbose inline Python with readable, maintainable jq expressions

---

## Key Features

### 1. Identity & Field Access
Extract any field or nested value using simple dot notation.

```bash
echo '{"user": {"name": "Alice", "age": 30}}' | jq '.user.name'
# Output: "Alice"
```

---

### 2. Array Iteration & Slicing
Iterate over arrays or access elements by index.

```bash
echo '[1, 2, 3, 4, 5]' | jq '.[2]'       # single element → 3
echo '[1, 2, 3, 4, 5]' | jq '.[1:4]'     # slice → [2, 3, 4]
echo '[{"id":1},{"id":2}]' | jq '.[].id' # iterate → 1, 2
```

---

### 3. Pipes & Composition
Chain filters together using `|` — the same mental model as Unix pipes.

```bash
echo '{"items": [{"name": "foo"}, {"name": "bar"}]}' \
  | jq '.items | .[0] | .name'
# Output: "foo"
```

---

### 4. Object & Array Construction
Build new JSON structures from existing data.

```bash
echo '{"first": "John", "last": "Doe"}' \
  | jq '{fullName: (.first + " " + .last)}'
# Output: {"fullName": "John Doe"}
```

---

### 5. Built-in Functions
jq ships with a rich standard library of functions.

| Function | Description |
|---|---|
| `keys` | Returns the keys of an object as an array |
| `values` | Returns the values of an object as an array |
| `length` | Returns the length of a string, array, or object |
| `map(f)` | Applies filter `f` to every element of an array |
| `select(f)` | Keeps only elements where `f` is true |
| `has("key")` | Checks if an object has a given key |
| `type` | Returns the JSON type of the input |
| `sort`, `sort_by(f)` | Sorts arrays, optionally by a key |
| `group_by(f)` | Groups array elements by a computed key |
| `unique`, `unique_by(f)` | Deduplicates array elements |
| `to_entries` / `from_entries` | Converts between object and `[{key, value}]` form |
| `add` | Sums or concatenates all elements of an array |
| `del(path)` | Removes a field from an object |
| `env` | Exposes environment variables as a JSON object |

---

### 6. Filtering with `select`
Keep only the records that match a condition.

```bash
echo '[{"name":"Alice","age":30},{"name":"Bob","age":17}]' \
  | jq '[.[] | select(.age >= 18)]'
# Output: [{"name": "Alice", "age": 30}]
```

---

### 7. `map` for Array Transformation
Apply a transformation to every element in an array.

```bash
echo '[1, 2, 3, 4]' | jq 'map(. * 2)'
# Output: [2, 4, 6, 8]
```

---

### 8. Conditional Logic
jq supports `if / then / else / end` expressions for branching.

```bash
echo '{"score": 72}' \
  | jq 'if .score >= 60 then "pass" else "fail" end'
# Output: "pass"
```

---

### 9. String Interpolation
Embed values inside strings using `\(expr)` syntax.

```bash
echo '{"name": "Alice", "lang": "Go"}' \
  | jq '"Hello, \(.name)! You are writing \(.lang)."'
# Output: "Hello, Alice! You are writing Go."
```

---

### 10. Pretty-print & Compact Output
Control output formatting for both human reading and downstream tooling.

```bash
cat data.json | jq '.'        # pretty-print (default)
cat data.json | jq -c '.'     # compact, single-line output
cat data.json | jq -r '.name' # raw output (strips JSON string quotes)
```

---

### 11. Reading from Files & Multiple Inputs
jq can read directly from files and process multiple JSON documents in a single invocation.

```bash
jq '.status' response.json                  # read from file
jq -s '.[0].name, .[1].name' a.json b.json  # slurp multiple files into an array
```

---

### 12. Recursive Descent
The `..` operator recursively walks every node in a JSON tree — useful for deeply nested structures.

```bash
echo '{"a":{"b":{"c": 42}}}' | jq '.. | numbers'
# Output: 42
```

---

## References

- [jq Official Website](https://jqlang.github.io/jq/)
- [jq Manual (latest)](https://jqlang.github.io/jq/manual/)
- [jq GitHub Repository](https://github.com/jqlang/jq)
- [jq Playground (try online)](https://jqplay.org/)

---

*Last updated: April 2026*
