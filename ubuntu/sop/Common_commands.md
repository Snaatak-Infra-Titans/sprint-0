# SOP: Common Linux Commands

## Document Details

| Author  | Created On     | Version | Last Updated By | Last Edited On | L0 Reviewer  | L1 Reviewer  | L2 Reviewer   |
|---------|----------------|---------|------------------|----------------|--------------|--------------|---------------|
| Deepak  | 14 April 2026     | v1.1    | Deepak           | 22 April 2026     | Mohit Kumar         | Faisal Khan       | Mahesh Kumar            |


## Table of Contents

1. [Purpose](#1-purpose)
2. [Terminal](#2-terminal)
3. [Navigation](#3-navigation)
4. [File Operations](#4-file-operations)
5. [Viewing Files](#5-viewing-files)
6. [Monitoring](#6-monitoring)
7. [Search](#7-search)
8. [Networking](#8-networking)
9. [Processes](#9-processes)
10. [Pipes & Redirection](#10-pipes--redirection)
11. [sudo](#11-sudo)
12. [Shortcuts](#12-shortcuts)
13. [Ubuntu Command Best Practices](#13-ubuntu-command-best-practices)
14. [Conclusion](#13-conclusion)
15. [References](#14-references)


## 1. Purpose

Quick reference for essential Linux commands.


## 2. Terminal

Command-line interface to interact with system.

Example:

```
user@host:~$
```

| Part | Meaning |
|------|--------|
| user | Username |
| host | Machine name |
| ~ | Home directory |
| $ | Normal user |


## 3. Navigation

```
pwd
ls -lah
cd folder
cd ..
cd ~
```

| Command | Meaning |
|---------|--------|
| pwd | Current directory |
| ls | List files |
| cd | Change directory |


## 4. File Operations

```
mkdir dir
touch file.txt
cp a b
mv old new
rm file
```

| Command | Meaning |
|---------|--------|
| mkdir | Create folder |
| touch | Create file |
| cp | Copy |
| mv | Move/Rename |
| rm | Delete |


## 5. Viewing Files

```
cat file
less file
head file
tail -f file
```

| Command | Meaning |
|---------|--------|
| cat | Print file |
| less | View large file |
| head | First lines |
| tail | Last lines |



## 6. Monitoring

```
df -h
free -h
top
```

| Command | Meaning |
|---------|--------|
| df | Disk usage |
| free | Memory |
| top | Processes |


## 7. Search

```
grep "text" file
find / -name file
```

| Command | Meaning |
|---------|--------|
| grep | Search text |
| find | Search files |


## 8. Networking

```
curl http://localhost
ping google.com
ss -tlnp
```

| Command | Meaning |
|---------|--------|
| curl | HTTP request |
| ping | Connectivity |
| ss | Open ports |


## 9. Processes

```
ps aux
kill PID
pkill name
```

| Command | Meaning |
|---------|--------|
| ps | List processes |
| kill | Stop process |
| pkill | Kill by name |


## 10. Pipes & Redirection

```
ps aux | grep nginx
echo hi > file
```

| Symbol | Meaning |
|--------|--------|
| \| | Pipe |
| > | Write |
| >> | Append |


## 11. sudo

```
sudo command
```

| Command | Meaning |
|---------|--------|
| sudo | Run as admin |


## 12. Shortcuts

| Shortcut | Meaning |
|----------|--------|
| Ctrl + C | Stop |
| Ctrl + L | Clear |
| ↑ ↓ | History |
| !! | Repeat last |

## 13. Ubuntu Command Best Practices

| Practice | Example | Why |
|----------|---------|-----|
| Verify location | pwd, ls -lah | Avoid wrong operations |
| Safe deletion | rm -i, avoid rm -rf | Prevent data loss |
| Use shortcuts | TAB, history | Save time, reduce errors |
| Care with sudo | sudo apt update | Avoid system damage |
| Use help | man, --help | Correct usage |
| Test before run | --dry-run | Prevent failures |
| Monitor & logs | top, tail -f log | Debug issues |


## 14. Conclusion

Essential Linux commands for daily usage.


## 15. References

| Description | Link |
|-------------|------|
| Official Ubuntu manual pages for Linux commands | [Ubuntu Man Pages](https://manpages.ubuntu.com) |
| Collection of commonly used Linux commands with explanations | [Linux Command Library](https://linuxcommandlibrary.com) |
| Tool to understand shell commands | [Explain Shell](https://explainshell.com) |


## Author


| Name   | Contact                                  |
|--------|------------------------------------------|
| Deepak | deepak.nagar.snaatak@mygurukulam.co      |
