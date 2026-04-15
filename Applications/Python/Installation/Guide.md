# 🐍 Python 3.12 Installation Guide (Ubuntu 24.04)

Install Python 3.12 (Latest Stable) on Ubuntu 24.04 in a simple and beginner-friendly way

## 📄 Document Information

| Author | Created on | Version | Last updated by | Last edited on | PRE Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
| ------ | ---------- | ------- | --------------- | -------------- | ------------ | ----------- | ----------- | ----------- |
| Gourav | 15-04-2026 | v1.0    | Gourav          | 15-04-2026     | -            | -           | -           | -           |

---

## 📌 Overview

This guide explains how to install Python using:

* ✅ APT (Easy & Recommended)
* ✅ Deadsnakes PPA (For latest versions)
* ✅ pyenv (For multiple versions)

---

## 🌟 Why Python 3.12?

* Latest stable version
* Security support till **2028**
* Key improvements:

  * Better error messages (easy to debug)
  * Faster performance
  * New syntax improvements
  * Better `f-string` support

---

## 🧱 Python Basics

| Component | Purpose                      |
| --------- | ---------------------------- |
| CPython   | Main Python interpreter      |
| pip       | Install Python packages      |
| venv      | Create isolated environments |
| IDLE      | Basic Python editor          |

> ✅ Always install **python3 + pip + venv**

---

## ✅ Prerequisites

### Check Ubuntu Version

```bash
lsb_release -a
```

> 📸 *Add screenshot here*

---

### Check System Info

```bash
uname -m
df -h /
free -h
```

> 📸 *Add screenshot here*

---

### Update System

```bash
sudo apt update && sudo apt upgrade -y
```

> 📸 *Add screenshot here*

---

## 🚀 Installation

### 🅰️ Method A: APT (Recommended)

```bash
sudo apt install -y python3 python3-pip python3-venv
```

> 📸 *Add screenshot here*

---

### Verify Installation

```bash
python3 --version
pip3 --version
```

> 📸 *Add screenshot here*

---

### 🅱️ Method B: Deadsnakes PPA (Latest Python Versions)

```bash
sudo apt install -y software-properties-common
```

#### Add PPA Repository

```bash
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt update
```

> 📸 *Add screenshot here*

---

#### Install Python 3.12

```bash
sudo apt install -y python3.12 python3.12-venv python3.12-dev
```

> 📸 *Add screenshot here*

---

### 🅲️ Method C: pyenv (Multiple Versions)

```bash
sudo apt install -y make build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev curl libncursesw5-dev \
xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev
```

#### Install pyenv

```bash
curl https://pyenv.run | bash
```

> 📸 *Add screenshot here*

---

#### Configure Shell

```bash
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(pyenv init -)"' >> ~/.bashrc
source ~/.bashrc
```

---

#### Install Python via pyenv

```bash
pyenv install --list | grep 3.12
pyenv install 3.12.3
pyenv global 3.12.3
```

> 📸 *Add screenshot here*

---

## 🔧 Set Up pip & Virtual Environment

### Upgrade pip

```bash
python3 -m pip install --upgrade pip
```

---

### Create a Virtual Environment

```bash
python3 -m venv myenv
source myenv/bin/activate
```

> 📸 *Add screenshot here*

---

### Deactivate Virtual Environment

```bash
deactivate
```

---

## 🔄 Multiple Python Versions

### List Available Python Versions

```bash
ls /usr/bin/python*
```

---

### Switch Default Version

```bash
sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.12 1
sudo update-alternatives --config python3
```

> 📸 *Add screenshot here*

---

## ✅ Verify Setup

```bash
python3 --version
pip3 --version
which python3
python3 -c "import sys; print(sys.executable)"
```

> 📸 *Add screenshot here*

---

## 🖥️ First Python Program

### Create File

```bash
nano hello_world.py
```

```python
print("Hello, World!")
```

> 📸 *Add screenshot here*

---

### Run the Program

```bash
python3 hello_world.py
```

> 📸 *Add screenshot here*

---

### Interactive Python Shell

```bash
python3
>>> print("Hello from Python!")
>>> exit()
```

---

## 🛠️ IDE Setup

### PyCharm Community

```bash
sudo snap install pycharm-community --classic
```

> 📸 *Add screenshot here*

---

### VS Code

```bash
sudo snap install code --classic
code --install-extension ms-python.python
```

> 📸 *Add screenshot here*

---

## ❗ Common Issues

### python3: command not found

```bash
sudo apt install -y python3
```

---

### pip3 not found

```bash
sudo apt install -y python3-pip
```

---

### Wrong Python Version

```bash
sudo update-alternatives --config python3
```

---

### ModuleNotFoundError

```bash
pip3 install <module-name>
# OR inside virtual environment:
source myenv/bin/activate
pip install <module-name>
```

---

### Permission Denied on pip install

```bash
pip3 install <package> --user
# OR use virtual environment (recommended)
```

---

## ⚡ Quick Commands

| Task                    | Command                     |
| ----------------------- | --------------------------- |
| Install Python          | `sudo apt install python3`  |
| Check version           | `python3 --version`         |
| Run a script            | `python3 script.py`         |
| Install a package       | `pip3 install <package>`    |
| Create virtual env      | `python3 -m venv myenv`     |
| Activate virtual env    | `source myenv/bin/activate` |
| Deactivate virtual env  | `deactivate`                |
| List installed packages | `pip3 list`                 |

---

## 🎉 Done!

You have successfully:

* Installed Python 3.12
* Set up pip and virtual environment
* Run your first Python program

---

Author: Gourav Sharma | Sprint 0 | Opstree Solutions | 14 April 2026

