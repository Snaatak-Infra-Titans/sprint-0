# Common Stack | Applications | Golang | Installation via Bash Script

<p align="center">
  <img src="https://softwebsolutions.b-cdn.net/wp-content/uploads/2020/10/golang-Programing.jpg" alt="GoLang" width="250"/>
</p>

---

## Author Table

| **Author** | **Created on** | **Version** | **Last updated by** | **Last Edited On** | **Pre Reviewer** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
| ---------- | -------------- | ----------- | ------------------- | ------------------ | ---------------- | --------------- | --------------- | --------------- |
| Ankita     | 17-04-2026     | v1.0        | Ankita              | 22-04-2026         | Team             | Komal Jaiswal   | Akshit Kapil    | Mahesh Kumar    |

---

## Table of Contents

1. [Introduction](#introduction)
2. [Purpose](#purpose)
3. [Why Use Bash Script for Installation](#why-use-bash-script-for-installation)
4. [Prerequisites](#prerequisites)
5. [Golang Installation via Bash Script](#golang-installation-via-bash-script)
6. [Script Explanation](#script-explanation)
7. [Verification](#verification)
8. [Use Cases](#use-cases)
9. [Best Practices](#best-practices)
10. [Contact Information](#contact-information)
11. [References](#references)

---

## Introduction

Golang (Go) is an open-source programming language developed by Google, designed for building fast, scalable, and efficient applications.

It is widely used in cloud-native development, microservices, and DevOps tools due to its performance and simplicity.

Installing Golang using a Bash script helps automate the setup process and ensures consistency across environments.

---

## Purpose

This document explains how to install Golang on Ubuntu using a Bash script, enabling automated and repeatable setup for development or production environments.

Please follow the link to learn more about Golang:  
[Golang Documentation](https://github.com/Snaatak-Infra-Titans/sprint-0/blob/SCRUM-32-shivam/Applications/Golang/Documentation/Golang_Intro.md)

---

## Why Use Bash Script for Installation

Using a Bash script provides several advantages:

* Automates repetitive installation steps
* Ensures consistent environment setup
* Saves time in multi-system deployments
* Integrates easily with CI/CD pipelines

---

## Prerequisites

* Ubuntu 20.04 / 22.04 / 24.04
* sudo privileges
* Internet access

---

## Golang Installation via Bash Script

Create a script file:

```bash
nano install-go.sh
```

Add the following content:

```bash
#!/bin/bash

# Update system packages
sudo apt update -y

# Download Go binary
wget https://go.dev/dl/go1.21.0.linux-amd64.tar.gz

# Remove any existing Go installation
sudo rm -rf /usr/local/go

# Extract Go
sudo tar -C /usr/local -xzf go1.21.0.linux-amd64.tar.gz

# Set environment variables
echo "export PATH=$PATH:/usr/local/go/bin" >> ~/.bashrc

# Reload environment
source ~/.bashrc

# Verify installation
go version
```

Make the script executable:

```bash
chmod +x install-go.sh
```

Run the script:

```bash
./install-go.sh
```
<img width="1226" height="1069" alt="image" src="https://github.com/user-attachments/assets/139586ce-40ee-40f2-8048-c39a9df79230" />

---

## Script Explanation

* `apt update` → Updates package list
* `wget` → Downloads Go binary
* `rm -rf /usr/local/go` → Removes old installation
* `tar` → Extracts Go to system directory
* `PATH` → Adds Go binary to system path
* `go version` → Verifies installation

---

## Verification

Check Go version:

```bash
go version
```

Check environment:

```bash
echo $PATH
```
<img width="956" height="189" alt="image" src="https://github.com/user-attachments/assets/d3e0c00e-c0e4-4780-98d7-0978ea88420e" />

Expected Result:

* Go version should be displayed
* Go binary path should be available in PATH

---

## Use Cases

* Setting up development environments
* Cloud-native application development
* CI/CD pipeline initialization
* Kubernetes and DevOps tooling

---

## Best Practices

* Use stable Go versions
* Keep Go updated
* Use version management tools if required
* Maintain scripts in version control

---

## Contact Information

| Name   | Email                                                                             |
| ------ | --------------------------------------------------------------------------------- |
| Ankita | [ankita.singh.snaatak@mygurukulam.co](mailto:ankita.singh.snaatak@mygurukulam.co) |

---

## References

| Topic            | Link                                       |
| ---------------- | ------------------------------------------ |
| Go Official Docs | [https://go.dev/doc/](https://go.dev/doc/) |
| Go Downloads     | [https://go.dev/dl/](https://go.dev/dl/)   |
