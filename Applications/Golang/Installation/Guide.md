# Common Stack | Applications | Golang | Installation Guide

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

---

## Prerequisites

Before you begin, ensure the following:

- A machine running **Ubuntu 24.04 LTS**
- A user account with **sudo** privileges
- Internet access to download the Go binary
- `curl` or `wget` installed (both are available by default on Ubuntu 24.04)

---

## Step 1 — Update System Packages

Refresh the package index and upgrade existing packages to ensure your system is up to date.

```bash
sudo apt update && sudo apt upgrade -y
```

Also install `curl` and `wget` if they are not already present:

```bash
sudo apt install -y curl wget
```

---

## Step 2 — Download the Go Tarball

Visit the [official Go downloads page](https://go.dev/dl/) to find the latest stable release. At the time of writing, the latest version is **Go 1.22.x**.

Download the Linux AMD64 tarball using `wget`:

```bash
wget https://go.dev/dl/go1.22.5.linux-amd64.tar.gz
```

> **Note:** Replace `go1.22.5` with the latest version number from [https://go.dev/dl/](https://go.dev/dl/).

Optionally, verify the SHA256 checksum against the value listed on the downloads page:

```bash
sha256sum go1.22.5.linux-amd64.tar.gz
```

Compare the output with the checksum provided on the official site before proceeding.

---

## Step 3 — Remove Any Previous Go Installation

If Go was previously installed under `/usr/local/go`, remove it to avoid conflicts:

```bash
sudo rm -rf /usr/local/go
```

> **Note:** Skip this step if this is a fresh installation.

---

## Step 4 — Extract the Tarball to `/usr/local`

Extract the downloaded tarball into `/usr/local`. This creates a `go` directory at `/usr/local/go`:

```bash
sudo tar -C /usr/local -xzf go1.22.5.linux-amd64.tar.gz
```

Confirm the extraction was successful:

```bash
ls /usr/local/go
```

Expected output includes directories such as `bin`, `src`, `pkg`, `lib`, and `doc`.

---

## Step 5 — Configure Environment Variables

Add the Go binary path to your system's `PATH` and define the `GOPATH` workspace directory.

Open your shell profile file:

```bash
# For bash (default shell on Ubuntu)
nano ~/.bashrc

# For zsh (if you use zsh)
nano ~/.zshrc

# For a system-wide installation (all users)
sudo nano /etc/profile.d/go.sh
```

Append the following lines at the end of the file:

```bash
# Go environment variables
export PATH=$PATH:/usr/local/go/bin
export GOPATH=$HOME/go
export PATH=$PATH:$GOPATH/bin
```

| Variable   | Description                                                    |
|------------|----------------------------------------------------------------|
| `PATH`     | Adds the Go compiler and tools to the executable path         |
| `GOPATH`   | Defines your Go workspace (where modules and binaries are stored) |

---

## Step 6 — Apply the Environment Changes

Reload your shell profile to apply the changes in the current session:

```bash
source ~/.bashrc
```

Or, for a system-wide profile:

```bash
source /etc/profile.d/go.sh
```

---

## Step 7 — Verify the Installation

Confirm that Go is correctly installed and the version is as expected:

```bash
go version
```

**Expected output:**

```
go version go1.22.5 linux/amd64
```

Also confirm the environment configuration:

```bash
go env
```

Key variables to check:

| Variable   | Expected Value                        |
|------------|---------------------------------------|
| `GOROOT`   | `/usr/local/go`                       |
| `GOPATH`   | `/home/<your-username>/go`            |
| `GOARCH`   | `amd64`                               |
| `GOOS`     | `linux`                               |

---

## Step 8 — Set Up Your Go Workspace

Create the standard Go workspace directory structure:

```bash
mkdir -p ~/go/{bin,src,pkg}
```

| Directory       | Purpose                                              |
|-----------------|------------------------------------------------------|
| `~/go/bin`      | Compiled binary executables                         |
| `~/go/src`      | Source code for your Go projects                    |
| `~/go/pkg`      | Compiled package objects (cache)                    |

---

## Step 9 — Write and Run a Test Program

Validate the full installation by creating and running a simple Go program.

**1. Create a project directory:**

```bash
mkdir -p ~/go/src/hello && cd ~/go/src/hello
```

**2. Initialise a Go module:**

```bash
go mod init hello
```

**3. Create the source file:**

```bash
nano main.go
```

**4. Paste the following content:**

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, Go on Ubuntu 24.04!")
}
```

**5. Run the program:**

```bash
go run main.go
```

**Expected output:**

```
Hello, Go on Ubuntu 24.04!
```

**6. (Optional) Build a standalone binary:**

```bash
go build -o hello
./hello
```

---

## Uninstallation

To completely remove Go from your system:

**1. Remove the Go installation directory:**

```bash
sudo rm -rf /usr/local/go
```

**2. Remove the Go workspace (optional):**

```bash
rm -rf ~/go
```

**3. Remove the environment variables** by deleting or commenting out the lines added in [Step 5](#step-5--configure-environment-variables) from `~/.bashrc` (or the relevant profile file), then reload:

```bash
source ~/.bashrc
```

---

## Troubleshooting

| Issue                              | Cause                                      | Fix                                                                 |
|------------------------------------|--------------------------------------------|---------------------------------------------------------------------|
| `go: command not found`            | `PATH` not updated or not reloaded         | Run `source ~/.bashrc` and verify `echo $PATH` includes `/usr/local/go/bin` |
| Wrong version shown                | Old Go installation still present          | Re-run Step 3 to remove the old installation                        |
| Checksum mismatch                  | Corrupted or incomplete download           | Re-download the tarball from [go.dev/dl](https://go.dev/dl/)        |
| Permission denied on `/usr/local`  | Missing sudo privileges                    | Prefix extraction command with `sudo`                               |
| `GOPATH` not set                   | Profile not reloaded                       | Run `source ~/.bashrc` or open a new terminal session               |

---

## References

- [Official Go Downloads](https://go.dev/dl/)
- [Go Installation Documentation](https://go.dev/doc/install)
- [Go Environment Variables](https://pkg.go.dev/cmd/go#hdr-Environment_variables)
- [Ubuntu 24.04 LTS Release Notes](https://releases.ubuntu.com/24.04/)

---

*Last updated: April 2026 | Tested on Ubuntu 24.04 LTS (Noble Numbat)*
