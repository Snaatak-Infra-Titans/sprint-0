# Common Stack | Applications | Golang | Installation Guide

## Document Information

| Author | Created On | Version | Last Updated By | Last Edited On | PRE Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|---|---|---|---|---|---|---|---|---|
| Versha Tripathi | 13-04-2026 | v1.0 | Versha Tripathi | 13-04-2026 | Team | - | - | - |

> **Platform:** Ubuntu 24.04 LTS (Noble Numbat)
> **Scope:** Step-by-step Go installation and environment setup

---

## Table of Contents

- [Prerequisites](#prerequisites)
- [Step 1 — Update System Packages](#step-1--update-system-packages)
- [Step 2 — Download the Go Tarball](#step-2--download-the-go-tarball)
- [Step 3 — Remove Any Previous Go Installation](#step-3--remove-any-previous-go-installation)
- [Step 4 — Extract the Tarball to /usr/local](#step-4--extract-the-tarball-to-usrlocal)
- [Step 5 — Configure Environment Variables](#step-5--configure-environment-variables)
- [Step 6 — Apply the Environment Changes](#step-6--apply-the-environment-changes)
- [Step 7 — Verify the Installation](#step-7--verify-the-installation)
- [Step 8 — Set Up Your Go Workspace](#step-8--set-up-your-go-workspace)
- [Step 9 — Write and Run a Test Program](#step-9--write-and-run-a-test-program)
- [Uninstallation](#uninstallation)
- [Troubleshooting](#troubleshooting)
- [Contact Information](#contact-information)
- [References](#references)

---

## Prerequisites

| Requirement | Detail |
|---|---|
| OS | Ubuntu 24.04 LTS (Noble Numbat) |
| User privileges | `sudo` access required |
| Network | Internet access to download Go binary |
| Tools | `curl` or `wget` (pre-installed on Ubuntu 24.04) |

---

## Step 1 — Update System Packages

Refresh the package index and upgrade existing packages to ensure your system is up to date.

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y curl wget
```

---

## Step 2 — Download the Go Tarball

Visit the [official Go downloads page](https://go.dev/dl/) for the latest stable release. Download the Linux AMD64 tarball:

```bash
wget https://go.dev/dl/go1.22.5.linux-amd64.tar.gz
```

> **Note:** Replace `go1.22.5` with the latest version from [https://go.dev/dl/](https://go.dev/dl/).

Optionally verify the checksum:

```bash
sha256sum go1.22.5.linux-amd64.tar.gz
```

Compare the output with the value listed on the official downloads page before proceeding.

---

## Step 3 — Remove Any Previous Go Installation

```bash
sudo rm -rf /usr/local/go
```

> **Note:** Skip this step if this is a fresh installation.

---

## Step 4 — Extract the Tarball to `/usr/local`

```bash
sudo tar -C /usr/local -xzf go1.22.5.linux-amd64.tar.gz
ls /usr/local/go
```

Expected directories: `bin`, `src`, `pkg`, `lib`, `doc`.

---

## Step 5 — Configure Environment Variables

Open your shell profile and append the following:

```bash
nano ~/.bashrc
```

```bash
# Go environment variables
export PATH=$PATH:/usr/local/go/bin
export GOPATH=$HOME/go
export PATH=$PATH:$GOPATH/bin
```

| Variable | Description |
|---|---|
| `PATH` | Adds Go compiler and tools to the executable path |
| `GOPATH` | Defines your Go workspace (modules and binaries) |

---

## Step 6 — Apply the Environment Changes

```bash
source ~/.bashrc
```

---

## Step 7 — Verify the Installation

```bash
go version
go env
```

Expected output: `go version go1.22.5 linux/amd64`

| Variable | Expected Value |
|---|---|
| `GOROOT` | `/usr/local/go` |
| `GOPATH` | `/home/<your-username>/go` |
| `GOARCH` | `amd64` |
| `GOOS` | `linux` |

---

## Step 8 — Set Up Your Go Workspace

```bash
mkdir -p ~/go/{bin,src,pkg}
```

| Directory | Purpose |
|---|---|
| `~/go/bin` | Compiled binary executables |
| `~/go/src` | Source code for your Go projects |
| `~/go/pkg` | Compiled package objects (cache) |

---

## Step 9 — Write and Run a Test Program

```bash
mkdir -p ~/go/src/hello && cd ~/go/src/hello
go mod init hello
nano main.go
```

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, Go on Ubuntu 24.04!")
}
```

```bash
go run main.go
```

Expected output: `Hello, Go on Ubuntu 24.04!`

Optionally build a standalone binary:

```bash
go build -o hello
./hello
```

---

## Uninstallation

```bash
# Remove Go installation
sudo rm -rf /usr/local/go

# Remove Go workspace (optional)
rm -rf ~/go
```

Remove the environment variables added in [Step 5](#step-5--configure-environment-variables) from `~/.bashrc`, then reload:

```bash
source ~/.bashrc
```

---

## Troubleshooting

| Issue | Cause | Fix |
|---|---|---|
| `go: command not found` | `PATH` not updated or reloaded | Run `source ~/.bashrc`; verify `echo $PATH` includes `/usr/local/go/bin` |
| Wrong version shown | Old Go installation still present | Re-run [Step 3](#step-3--remove-any-previous-go-installation) |
| Checksum mismatch | Corrupted or incomplete download | Re-download from [go.dev/dl](https://go.dev/dl/) |
| Permission denied on `/usr/local` | Missing sudo privileges | Prefix extraction command with `sudo` |
| `GOPATH` not set | Profile not reloaded | Run `source ~/.bashrc` or open a new terminal |

---

## Contact Information

| Name | Email |
|---|---|
| Versha Tripathi | [versha.tripathi.snaatak@mygurukulam.co](mailto:versha.tripathi.snaatak@mygurukulam.co) |

---

## References

| # | Resource | Link |
|---|---|---|
| 1 | Official Go Downloads | [go.dev/dl](https://go.dev/dl/) |
| 2 | Go Installation Documentation | [go.dev/doc/install](https://go.dev/doc/install) |
| 3 | Go Environment Variables | [pkg.go.dev/cmd/go](https://pkg.go.dev/cmd/go#hdr-Environment_variables) |
| 4 | Ubuntu 24.04 LTS Release Notes | [releases.ubuntu.com/24.04](https://releases.ubuntu.com/24.04/) |
