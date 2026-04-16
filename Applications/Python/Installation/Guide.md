#  Python 3.12 Installation Guide (Ubuntu 24.04)

Install Python 3.12 (Latest Stable) on Ubuntu 24.04 in a simple and beginner-friendly way

## 📄 Document Information

| Author | Created on | Version | Last updated by | Last edited on | PRE Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
| ------ | ---------- | ------- | --------------- | -------------- | ------------ | ----------- | ----------- | ----------- |
| Gourav | 15-04-2026 | v1.0    | Gourav          | 15-04-2026     | -            | -           | -           | -           |

---

##  Overview

This guide explains how to install Python using:

*  APT (Easy & Recommended)
*  Deadsnakes PPA (For latest versions)
*  pyenv (For multiple versions)

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

##  Python Basics

| Component | Purpose                      |
| --------- | ---------------------------- |
| CPython   | Main Python interpreter      |
| pip       | Install Python packages      |
| venv      | Create isolated environments |
| IDLE      | Basic Python editor          |

>  Always install **python3 + pip + venv**

---

##  Prerequisites

### Check Ubuntu Version

```bash
lsb_release -a
```
<img width="938" height="187" alt="image" src="https://github.com/user-attachments/assets/2711f55e-16f7-457a-b2d6-b1a71b1a19b8" />


---

### Check System Info

```bash
uname -m
df -h /
free -h
```
<img width="660" height="66" alt="image" src="https://github.com/user-attachments/assets/7e45a0b9-4727-4182-91de-e29a0a817fa6" />

<img width="1378" height="211" alt="image" src="https://github.com/user-attachments/assets/b2febf10-a615-448c-97d9-53c862160d16" />

---

### Update System

```bash
sudo apt update && sudo apt upgrade -y
```
<img width="929" height="881" alt="image" src="https://github.com/user-attachments/assets/0b53546c-7e94-45c2-9036-ef7fd5539e9a" />


---

##  Installation

###  Method A: APT (Recommended)

```bash
sudo apt install -y python3 python3-pip python3-venv
```
<img width="1045" height="175" alt="image" src="https://github.com/user-attachments/assets/2e44346b-199d-4e6c-bbfe-8b93b72eae38" />

---

### Verify Installation

```bash
python3 --version
pip3 --version
```
<img width="1171" height="202" alt="image" src="https://github.com/user-attachments/assets/ba435fd6-a8c0-429a-9a8f-2214b023b641" />


---

###  Method B: Deadsnakes PPA (Latest Python Versions)

```bash
sudo apt install -y software-properties-common
```

#### Add PPA Repository

```bash
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt update
```
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/d0c55936-f68e-43c1-9185-6c480d1465d1" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/0e8f0587-a3df-4ecb-9d90-1826c585da66" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/1dc10ac8-6059-4764-8e17-dc0c0e22c4bf" />


---

#### Install Python 3.12

```bash
sudo apt install -y python3.12 python3.12-venv python3.12-dev
```

---

###  Method C: pyenv (Multiple Versions)

```bash
sudo apt install -y make build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev curl libncursesw5-dev \
xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev
```

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/f8342d3b-2ca6-4cf1-9bda-51ce3fee73b7" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/73b40dc9-1aeb-4df8-bd44-d179daccd787" />


#### Install pyenv

```bash
curl https://pyenv.run | bash
```
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
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/c5a462ca-f74d-4337-a654-437dfe717b00" />


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
##  Multiple Python Versions

### List Available Python Versions

```bash
ls /usr/bin/python*
```

### Switch Default Version

```bash
sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.12 1
sudo update-alternatives --config python3
```

---

##  Verify Setup

```bash
python3 --version
pip3 --version
which python3
python3 -c "import sys; print(sys.executable)"
```

### Interactive Python Shell

```bash
python3
>>> print("Hello from Python!")
>>> exit()
```

### VS Code

```bash
sudo snap install code --classic
code --install-extension ms-python.python
```

---

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

##  Quick Commands

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

Author: Gourav Sharma | Sprint 0 | Infra Titans | 14 April 2026

