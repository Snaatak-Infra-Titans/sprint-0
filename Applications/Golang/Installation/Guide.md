# Golang - Installation Guide


## Document Information

| Author          | Created On | Version | L0 Reviewer  | L1 Reviewer  | L2 Reviewer     |
| --------------- | ---------- | ------- | ------------ | ------------ | --------------- |
| Versha Tripathi | 13-04-2026 | v1.0    | Prince Batra | Nikita Joshi | Piyush Upadhyay |

---



## Table of Contents

* [Introduction](#introduction)
* [Prerequisites](#prerequisites)
* [Step 1 — Update System Packages](#step-1--update-system-packages)
* [Step 2 — Install Golang using APT](#step-2--install-golang-using-apt)
* [Step 3 — Verify the Installation](#step-3--verify-the-installation)
* [Step 4 — Configure Environment Variables](#step-4--configure-environment-variables)
* [Step 5 — Apply the Environment Changes](#step-5--apply-the-environment-changes)
* [Step 6 — Set Up Your Go Workspace](#step-6--set-up-your-go-workspace)
* [Conclusion](#conclusion)
* [Contact Information](#contact-information)
* [References](#references)

---
## Introduction

This guide provides a simple and structured approach to installing Golang on Ubuntu 24.04. It is designed for beginners and developers who want a clean and reliable setup using the system package manager. By following this guide, you will be able to install Go, configure the environment, and verify that everything is working correctly.

---
## Prerequisites

| Requirement | Detail                          |
| ----------- | ------------------------------- |
| Tools       | `curl` or `wget`                |

---

## Step 1 — Update System Packages

```bash
sudo apt update && sudo apt upgrade -y
```

---

## Step 2 — Install Golang using APT

```bash
sudo apt install -y golang-go
```
<img width="1176" height="988" alt="image" src="https://github.com/user-attachments/assets/2a45c81b-95b5-419e-89e5-bdc7d0392001" />

---

## Step 3 — Verify the Installation

```bash
go version
```
<img width="468" height="48" alt="image" src="https://github.com/user-attachments/assets/8327f7c8-aee1-4d49-8b9f-61b9729dfe3f" />

---

## Step 4 — Configure Environment Variables

```bash
nano ~/.bashrc
```

```bash
export GOPATH=$HOME/go
export PATH=$PATH:$GOPATH/bin
```
<img width="1210" height="832" alt="image-2" src="https://github.com/user-attachments/assets/993be0c4-92ca-409b-8ec0-7e690a9f0ac7" />

---

## Step 5 — Apply the Environment Changes

```bash
source ~/.bashrc
```

---

## Step 6 — Set Up Your Go Workspace

```bash
mkdir -p ~/go/{bin,src,pkg}
```

---



## Conclusion

Installing Golang using APT on Ubuntu 24.04 is the simplest and most reliable approach for most users. It ensures easy installation, automatic dependency handling, and smooth updates through the package manager. After setting up environment variables and verifying the installation, you are ready to start building Go applications.

---

## Contact Information

| Name            | Email                                                                                   |
| --------------- | --------------------------------------------------------------------------------------- |
| Versha Tripathi | [versha.tripathi.snaatak@mygurukulam.co](mailto:versha.tripathi.snaatak@mygurukulam.co) |

---

## References

| # | Resource                       | Link                                                                     |
| - | ------------------------------ | ------------------------------------------------------------------------ |
| 1 | Official Go Downloads          | [https://go.dev/dl](https://go.dev/dl)                                   |
| 2 | Go Installation Documentation  | [https://go.dev/doc/install](https://go.dev/doc/install)                 |
| 3 | Ubuntu 24.04 LTS Release Notes | [https://releases.ubuntu.com/24.04/](https://releases.ubuntu.com/24.04/) |

---
