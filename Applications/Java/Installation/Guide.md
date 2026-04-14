# ☕ Java — Complete Installation Guide

> **"Write Once, Run Anywhere."** — Java's core philosophy since 1995.

---

## 📖 Table of Contents

- [What is Java?](#what-is-java)
- [JDK vs JRE vs JVM — Know Before You Install](#jdk-vs-jre-vs-jvm--know-before-you-install)
- [Which Java Version Should You Install?](#which-java-version-should-you-install)
- [Which Distribution Should You Choose?](#which-distribution-should-you-choose)
- [Installation — Windows](#installation--windows)
- [Installation — macOS](#installation--macos)
- [Installation — Linux (Ubuntu/Debian)](#installation--linux-ubuntudebian)
- [Installation — Linux (RHEL/Fedora/CentOS)](#installation--linux-rhelfedoracentos)
- [Installing Multiple Java Versions](#installing-multiple-java-versions)
- [Setting JAVA_HOME](#setting-java_home)
- [Verifying Your Installation](#verifying-your-installation)
- [Your First Java Program](#your-first-java-program)
- [IDE Setup Recommendations](#ide-setup-recommendations)
- [Common Issues & Fixes](#common-issues--fixes)
- [Uninstalling Java](#uninstalling-java)
- [Quick Reference](#quick-reference)

---

## What is Java?

**Java** is a high-level, object-oriented, platform-independent programming language and runtime environment developed by Sun Microsystems (now owned by Oracle) in 1995.

Java programs are compiled into **bytecode** that runs on the **Java Virtual Machine (JVM)**, making them portable across any operating system — Windows, macOS, Linux — without recompilation.

It is widely used for:
- Enterprise backend applications (Spring Boot, Jakarta EE)
- Android mobile development
- Big Data tools (Hadoop, Kafka, Spark)
- Web servers and microservices
- Desktop applications (JavaFX)

---

## JDK vs JRE vs JVM — Know Before You Install

Understanding these three terms will save you confusion:

```
┌─────────────────────────────────────────┐
│                   JDK                   │  ← Install this for development
│  ┌───────────────────────────────────┐  │
│  │               JRE                 │  │  ← Needed to RUN Java programs
│  │  ┌─────────────────────────────┐  │  │
│  │  │            JVM              │  │  │  ← Executes bytecode
│  │  │  (Java Virtual Machine)     │  │  │
│  │  └─────────────────────────────┘  │  │
│  │  + Java Standard Libraries        │  │
│  └───────────────────────────────────┘  │
│  + Compiler (javac)                     │
│  + Debugger, profiler, other dev tools  │
└─────────────────────────────────────────┘
```

| Component | Full Name | Purpose | Who Needs It |
|---|---|---|---|
| **JVM** | Java Virtual Machine | Executes compiled bytecode | Everyone (embedded in JRE/JDK) |
| **JRE** | Java Runtime Environment | Runs Java applications | End users running Java apps |
| **JDK** | Java Development Kit | Compiles + runs Java code | **Developers** ← install this |

> ✅ **Rule:** Always install the **JDK**. It includes everything in the JRE and JVM, plus the tools you need to write, compile, and debug Java programs.

---

## Which Java Version Should You Install?

Java releases a new version every 6 months, but only certain versions are **Long-Term Support (LTS)** — these receive security updates for years.

| Version | Type | Status | Recommendation |
|---|---|---|---|
| Java 8 | LTS | End of free support (Oracle) | ⚠️ Legacy only |
| Java 11 | LTS | Active support | ✅ Good for enterprise |
| Java 17 | LTS | Active support | ✅ Stable, widely used |
| **Java 21** | **LTS** | **Active support** | ✅✅ **Recommended (latest LTS)** |
| Java 22/23 | Non-LTS | Short-term support | ⚠️ Cutting edge, not for production |

> 🎯 **Recommendation for most users:** Install **Java 21 (LTS)**. It's the latest long-term support version with modern features like virtual threads, pattern matching, and record types.

---

## Which Distribution Should You Choose?

Since Java 17, Oracle's JDK requires a commercial license for production use. Several **free, open-source distributions** are available — all based on **OpenJDK** (the open-source reference implementation):

| Distribution | Provider | License | Best For |
|---|---|---|---|
| **[Eclipse Temurin](https://adoptium.net)** | Eclipse Foundation | Free / Open Source | ✅ **Recommended default** |
| **[Oracle JDK](https://www.oracle.com/java/)** | Oracle | Free for dev, paid for prod | Oracle-certified environments |
| **[Amazon Corretto](https://aws.amazon.com/corretto/)** | Amazon | Free / Open Source | AWS deployments |
| **[Azul Zulu](https://www.azul.com/downloads/)** | Azul Systems | Free / Open Source | Enterprise needs |
| **[GraalVM](https://www.graalvm.org/)** | Oracle | Free / Open Source | Native image compilation |
| **[Microsoft OpenJDK](https://www.microsoft.com/openjdk)** | Microsoft | Free / Open Source | Azure deployments |

> ✅ **Recommended:** **Eclipse Temurin (Adoptium)** — free, well-maintained, community-backed, and the most common choice for open-source projects.

---

## Installation — Windows

### Method 1: Using the Installer (Recommended for Beginners)

**Step 1 — Download the installer**

1. Go to **https://adoptium.net**
2. Select:
   - Version: **Java 21 (LTS)**
   - OS: **Windows**
   - Architecture: **x64** (for most modern PCs)
3. Download the `.msi` installer

**Step 2 — Run the installer**

1. Double-click the downloaded `.msi` file
2. Click **Next** on the welcome screen
3. Accept the license agreement
4. On the **Custom Setup** screen, enable:
   - ✅ **Add to PATH** (critical!)
   - ✅ **Set JAVA_HOME variable**
   - ✅ **JavaSoft registry keys**
5. Choose install location (default: `C:\Program Files\Eclipse Adoptium\jdk-21\`)
6. Click **Install** → **Finish**

**Step 3 — Verify installation**

Open **Command Prompt** (`Win + R` → type `cmd` → Enter):

```cmd
java -version
javac -version
```

Expected output:
```
openjdk version "21.0.3" 2024-04-16
OpenJDK Runtime Environment Temurin-21.0.3+9 (build 21.0.3+9)
OpenJDK 64-Bit Server VM Temurin-21.0.3+9 (build 21.0.3+9, mixed mode, sharing)

javac 21.0.3
```

---

### Method 2: Using winget (Windows Package Manager)

Open **PowerShell** or **Command Prompt** as Administrator:

```powershell
# Install Eclipse Temurin JDK 21
winget install EclipseAdoptium.Temurin.21.JDK

# Or install Oracle JDK 21
winget install Oracle.JDK.21
```

---

### Method 3: Using Chocolatey

```powershell
# Install Chocolatey first if needed: https://chocolatey.org/install
choco install temurin21          # Eclipse Temurin JDK 21
```

---

### Setting PATH Manually on Windows (if not done by installer)

1. Open **Start Menu** → search `Environment Variables`
2. Click **"Edit the system environment variables"**
3. Click **"Environment Variables..."** button
4. Under **System variables**, click **New**:
   - Variable name: `JAVA_HOME`
   - Variable value: `C:\Program Files\Eclipse Adoptium\jdk-21.0.3.9-hotspot`
5. Find the **Path** variable → click **Edit** → **New** → add:
   ```
   %JAVA_HOME%\bin
   ```
6. Click **OK** on all dialogs
7. **Restart** Command Prompt and verify with `java -version`

---

## Installation — macOS

### Method 1: Using Homebrew (Recommended)

**Step 1 — Install Homebrew** (if not already installed):

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

**Step 2 — Install Eclipse Temurin JDK 21:**

```bash
# Add the Adoptium tap
brew tap homebrew/cask-versions

# Install JDK 21 (LTS)
brew install --cask temurin@21
```

**Step 3 — Verify:**

```bash
java -version
javac -version
```

---

### Method 2: Using the macOS Installer Package

1. Go to **https://adoptium.net**
2. Select: Java 21 → macOS → your architecture:
   - **x64** — Intel Macs
   - **AArch64** — Apple Silicon (M1/M2/M3/M4)
3. Download the `.pkg` file
4. Double-click to run the installer → follow the prompts
5. The JDK installs to `/Library/Java/JavaVirtualMachines/`

**Step 4 — Set JAVA_HOME** (add to `~/.zshrc` or `~/.bash_profile`):

```bash
# For Apple Silicon (M1/M2/M3)
echo 'export JAVA_HOME=$(/usr/libexec/java_home -v 21)' >> ~/.zshrc

# Apply immediately
source ~/.zshrc
```

**Verify:**

```bash
echo $JAVA_HOME
# /Library/Java/JavaVirtualMachines/temurin-21.jdk/Contents/Home

java -version
```

---

### Method 3: Using SDKMAN (Best for Multiple Versions)

```bash
# Install SDKMAN
curl -s "https://get.sdkman.io" | bash
source "$HOME/.sdkman/bin/sdkman-init.sh"

# List available Java versions
sdk list java

# Install Temurin 21
sdk install java 21.0.3-tem

# Set as default
sdk default java 21.0.3-tem
```

> SDKMAN is the macOS/Linux equivalent of a version manager (like nvm for Node.js). Highly recommended if you'll work with multiple Java versions.

---

## Installation — Linux (Ubuntu/Debian)

### Method 1: APT Package Manager (Quickest)

```bash
# Update package index
sudo apt update

# Install OpenJDK 21 (Ubuntu 23.04+)
sudo apt install -y openjdk-21-jdk

# For older Ubuntu versions, add the Adoptium repository:
sudo apt install -y wget apt-transport-https gpg

wget -qO - https://packages.adoptium.net/artifactory/api/gpg/key/public | \
  gpg --dearmor | \
  sudo tee /etc/apt/trusted.gpg.d/adoptium.gpg > /dev/null

echo "deb https://packages.adoptium.net/artifactory/deb $(. /etc/os-release && echo $VERSION_CODENAME) main" | \
  sudo tee /etc/apt/sources.list.d/adoptium.list

sudo apt update
sudo apt install -y temurin-21-jdk
```

**Verify:**

```bash
java -version
javac -version
which java          # /usr/bin/java
```

---

### Method 2: Using SDKMAN (Recommended for Developers)

```bash
# Install SDKMAN
curl -s "https://get.sdkman.io" | bash
source "$HOME/.sdkman/bin/sdkman-init.sh"

# Install Temurin JDK 21
sdk install java 21.0.3-tem

# Verify
java -version
```

---

### Set JAVA_HOME on Ubuntu/Debian

```bash
# Find the JDK path
sudo update-alternatives --config java
# Note the path shown, e.g.: /usr/lib/jvm/temurin-21-amd64

# Add to ~/.bashrc (or ~/.zshrc)
echo 'export JAVA_HOME=/usr/lib/jvm/temurin-21-amd64' >> ~/.bashrc
echo 'export PATH=$JAVA_HOME/bin:$PATH' >> ~/.bashrc

source ~/.bashrc

# Verify
echo $JAVA_HOME
```

---

## Installation — Linux (RHEL/Fedora/CentOS)

### Method 1: DNF / YUM

```bash
# Fedora / RHEL 8+
sudo dnf install -y java-21-openjdk-devel

# CentOS 7 (using yum)
sudo yum install -y java-11-openjdk-devel

# Verify
java -version
```

### Method 2: Adoptium Repository (RHEL/CentOS)

```bash
# Add Adoptium repo
cat <<EOF | sudo tee /etc/yum.repos.d/adoptium.repo
[Adoptium]
name=Adoptium
baseurl=https://packages.adoptium.net/artifactory/rpm/rhel/\$releasever/\$basearch
enabled=1
gpgcheck=1
gpgkey=https://packages.adoptium.net/artifactory/api/gpg/key/public
EOF

sudo dnf install -y temurin-21-jdk

# Verify
java -version
```

---

## Installing Multiple Java Versions

It's common to need multiple Java versions for different projects. Here's how to manage them:

### On Windows — Using `JAVA_HOME` Switching

Create a batch script `setjava.bat`:

```cmd
@echo off
if "%1"=="11" set JAVA_HOME=C:\Program Files\Eclipse Adoptium\jdk-11.0.23.9-hotspot
if "%1"=="17" set JAVA_HOME=C:\Program Files\Eclipse Adoptium\jdk-17.0.11.9-hotspot
if "%1"=="21" set JAVA_HOME=C:\Program Files\Eclipse Adoptium\jdk-21.0.3.9-hotspot
set PATH=%JAVA_HOME%\bin;%PATH%
echo Switched to Java %1
java -version
```

---

### On macOS / Linux — Using SDKMAN (Recommended)

```bash
# Install multiple versions
sdk install java 11.0.23-tem
sdk install java 17.0.11-tem
sdk install java 21.0.3-tem

# Switch globally
sdk use java 17.0.11-tem

# Switch for current project only (creates .sdkmanrc)
sdk env init           # Creates .sdkmanrc with current version
sdk env                # Applies .sdkmanrc in current directory
```

---

### On Linux — Using `update-alternatives`

```bash
# List all installed Java versions
sudo update-alternatives --config java

# Output:
# There are 3 choices for the alternative java:
#   Selection  Path                                         Priority
# * 0          /usr/lib/jvm/java-21-openjdk-amd64/bin/java  1111
#   1          /usr/lib/jvm/java-11-openjdk-amd64/bin/java  1111
#   2          /usr/lib/jvm/java-17-openjdk-amd64/bin/java  1111

# Type the selection number and press Enter to switch
```

---

## Setting JAVA_HOME

`JAVA_HOME` is an environment variable many tools (Maven, Gradle, IDEs, application servers) rely on to locate your JDK.

### Windows

```cmd
setx JAVA_HOME "C:\Program Files\Eclipse Adoptium\jdk-21.0.3.9-hotspot" /M
setx PATH "%JAVA_HOME%\bin;%PATH%" /M
```

Or set via System Properties → Environment Variables (see Windows section above).

---

### macOS

```bash
# Add to ~/.zshrc (Zsh — default on macOS Catalina+)
echo 'export JAVA_HOME=$(/usr/libexec/java_home -v 21)' >> ~/.zshrc
source ~/.zshrc

# For Bash (older macOS)
echo 'export JAVA_HOME=$(/usr/libexec/java_home -v 21)' >> ~/.bash_profile
source ~/.bash_profile
```

The `java_home` utility automatically finds the correct path for the specified version.

---

### Linux

```bash
# Add to ~/.bashrc or /etc/environment for system-wide setting
echo 'export JAVA_HOME=/usr/lib/jvm/temurin-21-amd64' >> ~/.bashrc
echo 'export PATH=$JAVA_HOME/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
```

---

## Verifying Your Installation

Run these checks after installation on any OS:

```bash
# Check Java runtime version
java -version

# Check Java compiler version
javac -version

# Check JAVA_HOME is set
echo $JAVA_HOME          # macOS/Linux
echo %JAVA_HOME%         # Windows CMD

# Find where java binary is located
which java               # macOS/Linux
where java               # Windows

# Show all JVM flags and properties
java -XshowSettings:all -version

# List all available JVMs (macOS only)
/usr/libexec/java_home -V
```

Expected healthy output:

```
openjdk version "21.0.3" 2024-04-16
OpenJDK Runtime Environment Temurin-21.0.3+9 (build 21.0.3+9)
OpenJDK 64-Bit Server VM Temurin-21.0.3+9 (build 21.0.3+9, mixed mode, sharing)

javac 21.0.3
```

---

## Your First Java Program

Let's confirm the full toolchain works end-to-end:

**Step 1 — Create the file**

Create a file named `HelloWorld.java`:

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
        System.out.println("Java version: " + System.getProperty("java.version"));
        System.out.println("Running on: " + System.getProperty("os.name"));
    }
}
```

> ⚠️ The filename **must exactly match** the class name: `HelloWorld.java`

**Step 2 — Compile**

```bash
javac HelloWorld.java
```

This creates `HelloWorld.class` (the bytecode file).

**Step 3 — Run**

```bash
java HelloWorld
```

Expected output:

```
Hello, World!
Java version: 21.0.3
Running on: Mac OS X          # (or Windows 11, Linux, etc.)
```

**Step 4 (Java 11+) — Single-file shortcut**

For single-file programs, you can skip compilation:

```bash
java HelloWorld.java          # Compiles and runs in one step
```

---

## IDE Setup Recommendations

A good IDE dramatically improves Java development. Here are the top choices:

### IntelliJ IDEA (Recommended)
- **Download:** https://www.jetbrains.com/idea/
- **Community Edition** is free and sufficient for most Java development
- Best-in-class refactoring, code completion, and debugging
- Auto-detects installed JDKs

```
File → Project Structure → SDKs → + → JDK
Point to your JAVA_HOME directory
```

---

### Visual Studio Code
- **Download:** https://code.visualstudio.com/
- Install the **Extension Pack for Java** (Microsoft)

```bash
# Install extensions via CLI
code --install-extension vscjava.vscode-java-pack
```

Configure JDK in `settings.json`:

```json
{
  "java.jdt.ls.java.home": "/Library/Java/JavaVirtualMachines/temurin-21.jdk/Contents/Home"
}
```

---

### Eclipse IDE
- **Download:** https://www.eclipse.org/downloads/
- Free and open-source
- Good for enterprise/Jakarta EE development

---

### NetBeans
- **Download:** https://netbeans.apache.org/
- Free, Apache-maintained
- Good for beginners

---

## Common Issues & Fixes

### ❌ `java: command not found` / `'java' is not recognized`

**Cause:** Java is not in your PATH.

**Fix:**
```bash
# Check if Java is installed but not in PATH
ls /usr/lib/jvm/                          # Linux
ls /Library/Java/JavaVirtualMachines/     # macOS
dir "C:\Program Files\Eclipse Adoptium\"  # Windows

# Then set JAVA_HOME and PATH as described above
```

---

### ❌ `javac: command not found`

**Cause:** Only the JRE is installed, not the JDK.

**Fix:** Install the **JDK** (not JRE):
```bash
sudo apt install -y openjdk-21-jdk        # Ubuntu — note: -jdk not -jre
```

---

### ❌ Wrong Java version showing after install

**Cause:** Old Java is still first in PATH, or JAVA_HOME points to an old version.

**Fix:**
```bash
# Check which java is being used
which java
java -version

# On Linux, reconfigure alternatives
sudo update-alternatives --config java

# On macOS
export JAVA_HOME=$(/usr/libexec/java_home -v 21)
```

---

### ❌ `Error: A JNI error has occurred` / `UnsupportedClassVersionError`

**Cause:** Code was compiled with a newer Java version than the one running it.

**Fix:** Ensure your compile-time and runtime JDK versions match:
```bash
java -version     # Runtime
javac -version    # Compiler
# Both should show the same major version
```

---

### ❌ `JAVA_HOME` is set but Maven/Gradle still fails

**Cause:** Tool is picking up system Java, not JAVA_HOME.

**Fix:**
```bash
# Check what Maven sees
mvn --version

# Force Maven to use JAVA_HOME
export JAVA_HOME=/path/to/jdk
mvn --version     # Should now reflect the correct version
```

---

### ❌ macOS — `xcrun: error` when installing Homebrew

**Cause:** Xcode Command Line Tools not installed.

**Fix:**
```bash
xcode-select --install
```

---

## Uninstalling Java

### Windows

1. **Control Panel** → **Programs** → **Uninstall a program**
2. Find **Eclipse Temurin JDK** (or Oracle JDK)
3. Click **Uninstall**
4. Remove `JAVA_HOME` from Environment Variables
5. Remove `%JAVA_HOME%\bin` from PATH

---

### macOS

```bash
# Remove Temurin JDK installed via .pkg
sudo rm -rf /Library/Java/JavaVirtualMachines/temurin-21.jdk

# Remove via Homebrew
brew uninstall --cask temurin@21

# Via SDKMAN
sdk uninstall java 21.0.3-tem
```

---

### Linux (Ubuntu/Debian)

```bash
# Remove OpenJDK
sudo apt remove --purge openjdk-21-jdk
sudo apt autoremove

# Remove Temurin
sudo apt remove --purge temurin-21-jdk
sudo apt autoremove

# Via SDKMAN
sdk uninstall java 21.0.3-tem
```

---

### Linux (RHEL/Fedora)

```bash
sudo dnf remove java-21-openjdk-devel
```

---

## Quick Reference

### Installation Commands by Platform

```bash
# ─── Windows ───────────────────────────────────────────────
winget install EclipseAdoptium.Temurin.21.JDK

# ─── macOS (Homebrew) ───────────────────────────────────────
brew install --cask temurin@21

# ─── Ubuntu/Debian ──────────────────────────────────────────
sudo apt update && sudo apt install -y openjdk-21-jdk

# ─── Fedora/RHEL ────────────────────────────────────────────
sudo dnf install -y java-21-openjdk-devel

# ─── Any OS (SDKMAN) ────────────────────────────────────────
curl -s "https://get.sdkman.io" | bash
sdk install java 21.0.3-tem
```

### Verification Commands

```bash
java -version          # Runtime version
javac -version         # Compiler version
echo $JAVA_HOME        # JDK home (macOS/Linux)
echo %JAVA_HOME%       # JDK home (Windows)
which java             # Java binary location (macOS/Linux)
where java             # Java binary location (Windows)
```

### Compile & Run

```bash
javac MyProgram.java   # Compile → produces MyProgram.class
java MyProgram         # Run (no .class extension)
java MyProgram.java    # Compile + run in one step (Java 11+)
```

---

## Further Reading

- 📘 [Eclipse Adoptium (Temurin) — Official Site](https://adoptium.net)
- 📘 [OpenJDK — Reference Implementation](https://openjdk.org)
- 📘 [Oracle Java Downloads](https://www.oracle.com/java/technologies/downloads/)
- 📘 [SDKMAN — Multi-version Manager](https://sdkman.io)
- 📄 [Java Version History](https://en.wikipedia.org/wiki/Java_version_history)
- 🛠 [IntelliJ IDEA Community Edition](https://www.jetbrains.com/idea/download/)
- 🛠 [VS Code Extension Pack for Java](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack)

---

*Documentation covers Java 21 LTS | Updated for Eclipse Temurin, Oracle JDK, SDKMAN*
