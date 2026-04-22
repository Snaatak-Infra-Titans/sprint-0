# SOP for Python Virtual Environment (venv)

| Author           | Created on | Version | Last updated by | Last edited on | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer      |
|------------------|------------|---------|-----------------|----------------|--------------|-------------|-------------|------------------|
| Shivam Uniyal    | 15-04-2026 | v1.0    | Shivam Uniyal   | 22-04-2026     | Team         | Anuj Jain   | Prashant    | Piyush Upadhyay  |

---

## Table of Contents

1. [Introduction](#1-introduction)  
2. [Purpose](#2-purpose)  
3. [System Requirements](#3-system-requirements)  
4. [Step-by-Step Procedure](#4-step-by-step-procedure)  
5. [Troubleshooting](#5-troubleshooting)  
6. [FAQs](#6-faqs)  
7. [Contact Information](#7-contact-information)  
8. [References](#8-references)  
9. [Conclusion](#9-conclusion)

---

## 1. Introduction

A Python Virtual Environment (venv) is an isolated workspace that allows separate environments for different projects. Each environment has its own Python interpreter and packages, preventing dependency conflicts. It helps manage different library versions, improves reproducibility, and keeps the system environment clean.

---

## 2. Purpose

The purpose of this SOP is to provide a structured and easy-to-follow guide for managing Python virtual environments in Ubuntu.

This document helps users to:

- Create and configure a virtual environment  
- Activate and work inside the environment  
- Install and manage Python packages  
- Export dependencies for reuse  
- Deactivate and delete environments  
- Troubleshoot common issues  

---

## 3. System Requirements

| Component | Minimum Requirement |
|----------|-------------------|
| CPU      | Dual Core          |
| RAM      | 4 GB               |
| Disk     | 10 GB free space   |
| OS       | Ubuntu 24.04       |

---

## 4. Step-by-Step Procedure

### Step 1: Install venv package
```bash
sudo apt update
sudo apt install python3-venv -y
```
<img width="1240" height="470" alt="Screenshot 2026-04-22 at 5 41 19 PM" src="https://github.com/user-attachments/assets/8c34422e-3671-433c-a5e6-9c718682afee" />
--
<img width="693" height="129" alt="Screenshot 2026-04-22 at 5 42 28 PM" src="https://github.com/user-attachments/assets/baa332d8-db91-465b-8b6a-aa75ac81dd53" />

---

### Step 2: Create Virtual Environment
```bash
python3 -m venv myenv
```

Verify:
```bash
ls -d myenv
```
<img width="693" height="95" alt="Screenshot 2026-04-22 at 5 47 50 PM" src="https://github.com/user-attachments/assets/da3176d0-945a-47d4-9659-765ae096e4f9" />

---

### Step 3: Activate Virtual Environment
```bash
source myenv/bin/activate
```
<img width="693" height="76" alt="Screenshot 2026-04-22 at 5 49 09 PM" src="https://github.com/user-attachments/assets/fcc054d7-9964-4581-955c-e1f1b7c28c79" />

---

### Step 4: Install Python Packages
```bash
pip install requests
```
<img width="1403" height="465" alt="Screenshot 2026-04-22 at 5 53 16 PM" src="https://github.com/user-attachments/assets/b6817c11-53a2-459f-82be-bf9e099e964d" />

Verify:
```bash
pip list
```
<img width="1335" height="241" alt="Screenshot 2026-04-22 at 5 54 08 PM" src="https://github.com/user-attachments/assets/d2a5bc31-7470-4efb-9d91-8b21cd1becdb" />

---

### Step 5: Freeze Dependencies
```bash
pip freeze > requirements.txt
```
<img width="1335" height="210" alt="Screenshot 2026-04-22 at 5 55 14 PM" src="https://github.com/user-attachments/assets/92b6f104-6648-41ef-9ea0-e5735d0a4658" />

---

### Step 6: Deactivate Virtual Environment
```bash
deactivate
```
<img width="831" height="75" alt="Screenshot 2026-04-22 at 5 56 11 PM" src="https://github.com/user-attachments/assets/c340e57d-2166-4ccb-842a-1598436a43d3" />

---

### Step 7: Delete Virtual Environment
```bash
rm -rf myenv
```
<img width="901" height="143" alt="Screenshot 2026-04-22 at 5 57 33 PM" src="https://github.com/user-attachments/assets/20862ff7-b19c-4deb-a2c8-7ac1017fd077" />

---

## 5. Troubleshooting

| Issue | Possible Cause | Solution |
|------|---------------|----------|
| Activation not working | Incorrect command | Use `source myenv/bin/activate` |
| Permission denied | Missing execution rights | Run `chmod +x myenv/bin/activate` |
| pip not found | pip not installed | Run `python3 -m ensurepip --upgrade` |
| Wrong Python version | Multiple Python versions installed | Verify using `python3 --version` |
| Environment not activating | Wrong directory | Navigate to correct folder before activating |
| Packages not installing | Network issue or pip outdated | Run `pip install --upgrade pip` |

---

## 6. FAQs

**Q1. What is a virtual environment?**  
It is an isolated Python environment used to manage dependencies separately.

**Q2. Why use virtual environments?**  
To avoid conflicts between different projects.

**Q3. How do I activate the environment?**  
```
source myenv/bin/activate
```

**Q4. How do I install dependencies from a file?**  
```
pip install -r requirements.txt
```

---

## 7. Contact Information

| Name           | Email ID |
|----------------|----------|
| Shivam Uniyal  | shivam.uniyal.snaatak@mygurukulam.co |

---

## 8. References

| Link | Description |
|------|------------|
| https://docs.python.org/3/library/venv.html | Official Python venv documentation |
| https://ubuntu.com | Ubuntu documentation |

---

## 9. Conclusion

This SOP provides a simple and structured approach to managing Python virtual environments. It helps avoid dependency conflicts and ensures a clean and efficient development setup. Following these steps improves consistency and reliability in DevOps workflows.
