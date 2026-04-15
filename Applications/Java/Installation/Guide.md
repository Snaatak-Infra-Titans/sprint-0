#  Java JDK 21 Installation Guide (Ubuntu 24.04)

Install Java JDK 21 (LTS) on Ubuntu 24.04 in a simple and beginner-friendly way 

##  Document Information

| Author           | Created on  | Version | Last updated by | Last edited on | PRE Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|------------------|------------|---------|-----------------|----------------|-------------|------------|------------|------------|
| Versha Tripathi  | 13-04-2026 | v1.0    | Versha Tripathi | 13-04-2026     | -           | -          | -          | -          |
---

##  Overview

This guide covers installing Java using:

*  APT (Recommended)
*  Eclipse Temurin (Official Build)
*  SDKMAN (Multiple Versions)

---

##  Why Java 21?

* Long-Term Support (LTS)
* Security updates till **2031**
* Features:

  * Virtual Threads
  * Pattern Matching
  * Records

---

##  Java Basics

| Component | Purpose                |
| --------- | ---------------------- |
| JVM       | Runs Java programs     |
| JRE       | JVM + libraries        |
| JDK       | JRE + compiler + tools |

 Always install **JDK**

---

##  Prerequisites

### Check Ubuntu Version

```bash
lsb_release -a
```


 <img width="459" height="133" alt="image" src="https://github.com/user-attachments/assets/d76366d6-8193-45b8-b2aa-1e82c048c8e5" />


---

### Check System Info

```bash
uname -m
df -h /
free -h
```

 <img width="819" height="278" alt="image" src="https://github.com/user-attachments/assets/2efe7b3c-fa8c-4dd0-a5f6-0e1ca1997b67" />


---

### Update System

```bash
sudo apt update && sudo apt upgrade -y
```

 <img width="1064" height="703" alt="image" src="https://github.com/user-attachments/assets/aad5ca98-e87e-46e7-b23d-8c19d9de2ad4" />


---

##  Installation

###  Method A: APT (Recommended)

```bash
sudo apt install -y openjdk-21-jdk
```

 <img width="1322" height="698" alt="image" src="https://github.com/user-attachments/assets/cf41b783-4498-48df-a97f-36d1bd7a1db7" />


---

### Verify Installation

```bash
java -version
javac -version
```

 <img width="806" height="146" alt="image" src="https://github.com/user-attachments/assets/ebdf5ad9-9400-4072-b823-4d1e969c2b20" />


---

###  Method B: Eclipse Temurin

```bash
sudo apt install -y wget apt-transport-https gpg
```

#### Add GPG Key

```bash
wget -qO - https://packages.adoptium.net/artifactory/api/gpg/key/public \
| gpg --dearmor \
| sudo tee /etc/apt/trusted.gpg.d/adoptium.gpg > /dev/null
```

 <img width="1089" height="473" alt="image" src="https://github.com/user-attachments/assets/99c803eb-d0e9-4878-a66c-e898488d76c5" />


---

#### Add Repository

```bash
echo "deb https://packages.adoptium.net/artifactory/deb noble main" \
| sudo tee /etc/apt/sources.list.d/adoptium.list
```

---

#### Install

```bash
sudo apt update
sudo apt install -y temurin-21-jdk
```

 <img width="1849" height="887" alt="image" src="https://github.com/user-attachments/assets/368d5308-bd04-4264-a16e-e090b1992161" />


---

###  Method C: SDKMAN

```bash
curl -s "https://get.sdkman.io" | bash
source "$HOME/.sdkman/bin/sdkman-init.sh"
```

 <img width="1071" height="887" alt="image" src="https://github.com/user-attachments/assets/330bd90e-5b0e-469e-b1c4-9863a8e9fcff" />


---

#### Install Java

```bash
sdk list java
sdk install java 21.0.3-tem
sdk default java 21.0.3-tem
```

 <img width="1845" height="435" alt="image" src="https://github.com/user-attachments/assets/9d3eee21-7706-4bf8-a57d-67d5dbbdab54" />


---

##  Set JAVA_HOME

### Find Path

```bash
readlink -f $(which java)
```

---

### Set Variable

```bash
nano ~/.bashrc
```

Add:

```bash
export JAVA_HOME=/usr/lib/jvm/java-21-openjdk-amd64
export PATH=$JAVA_HOME/bin:$PATH
```

Apply:

```bash
source ~/.bashrc
echo $JAVA_HOME
```

 *Add screenshot here*

---

##  Multiple Java Versions

### Install Java 17

```bash
sudo apt install -y openjdk-17-jdk
```

---

### Switch Version

```bash
sudo update-alternatives --config java
sudo update-alternatives --config javac
```

 *Add screenshot here*

---

##  Verify Setup

```bash
java -version
javac -version
which java
echo $JAVA_HOME
```

 *Add screenshot here*

---

##  First Java Program

### Create File

```bash
nano HelloWorld.java
```

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

 *Add screenshot here*

---

### Compile

```bash
javac HelloWorld.java
ls
```

 *Add screenshot here*

---

### Run

```bash
java HelloWorld
```

 *Add screenshot here*

---

##  Shortcut (Java 11+)

```bash
java HelloWorld.java
```

---

##  IDE Setup

### IntelliJ IDEA

```bash
sudo snap install intellij-idea-community --classic
```

 *Add screenshot here*

---

### VS Code

```bash
sudo snap install code --classic
code --install-extension vscjava.vscode-java-pack
```

 *Add screenshot here*

---

##  Common Issues

### java: command not found

```bash
export PATH=/usr/lib/jvm/java-21-openjdk-amd64/bin:$PATH
```

---

### javac not found

```bash
sudo apt install -y openjdk-21-jdk
```

---

### Wrong Java Version

```bash
sudo update-alternatives --config java
```

---

### UnsupportedClassVersionError

```bash
javac --release 17 HelloWorld.java
```

---

##  Quick Commands

| Task          | Command                           |
| ------------- | --------------------------------- |
| Install Java  | `sudo apt install openjdk-21-jdk` |
| Check version | `java -version`                   |
| Compile       | `javac file.java`                 |
| Run           | `java file`                       |
| Set JAVA_HOME | `export JAVA_HOME=...`            |

---

##  Done!

You have successfully:

* Installed Java 21
* Configured environment
* Run your first program

---

