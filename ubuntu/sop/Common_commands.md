# SOP: Common Linux Commands

| Author | Created On | Version | Last Updated By | Last Edited On | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|--------|------------|---------|-----------------|----------------|--------------|-------------|-------------|-------------|
| Deepak | April 2026 | v1.0 | Deepak | April 2026 | | | | |

**Project:** OT-Microservices | Sprint 0  


---

## Table of Contents

1. [Purpose](#1-purpose)
2. [What is a Terminal?](#2-what-is-a-terminal)
3. [Navigation & Filesystem](#3-navigation--filesystem)
4. [File & Directory Operations](#4-file--directory-operations)
5. [Viewing File Contents](#5-viewing-file-contents)
6. [System Information & Monitoring](#6-system-information--monitoring)
7. [Searching & Filtering](#7-searching--filtering)
8. [Networking & Connectivity](#8-networking--connectivity)
9. [Process Management](#9-process-management)
10. [Pipes & Redirection](#10-pipes--redirection)
11. [sudo — Running as Root](#11-sudo--running-as-root)
12. [Shell Shortcuts & History](#12-shell-shortcuts--history)
13. [Commands Used in OT-Microservices Deployment](#13-commands-used-in-ot-microservices-deployment)
14. [Conclusion](#14-conclusion)
15. [References](#15-references)

---

## 1. Purpose

This SOP documents the most frequently used Linux commands for working on Ubuntu 22.04 LTS servers. It is written for team members at all levels — whether you are opening a terminal for the first time or just need a quick reference during deployment.

By the end of this document, you will be able to:

- Move around the filesystem and manage files
- Read and monitor log files
- Check if services and ports are running
- Search through files and command output
- Run background processes safely

> **Note:** All commands in this document are tested on **Ubuntu 22.04 LTS**.

---

## 2. What is a Terminal?

The terminal (also called the shell or command line) is a text-based way to interact with your server. Instead of clicking buttons, you type commands.

When you open a terminal, you will see something like this:

```
ubuntu@ip-10-0-1-5:~$
```

This is called the **prompt**. It tells you:

| Part | Meaning |
|------|---------|
| `ubuntu` | Your username |
| `ip-10-0-1-5` | The server hostname |
| `~` | Your current location (`~` means home directory) |
| `$` | You are a regular user (not root) |

> **Tip:** If you see `#` instead of `$`, you are logged in as root (the superuser).

---

## 3. Navigation & Filesystem

These commands help you move around and understand where you are.

---

### 3.1 `pwd` — Where Am I?

`pwd` stands for **Print Working Directory**. It shows you your exact location.

```bash
pwd
```

**Example output:**
```
/home/ubuntu
```

> **When to use:** Run `pwd` whenever you are unsure where you are before doing anything important.

---

### 3.2 `ls` — What's in This Folder?

`ls` lists files and folders in your current location.

```bash
# Basic list
ls

# Detailed list (shows permissions, size, date)
ls -l

# Show hidden files too (files starting with a dot)
ls -a

# Detailed + hidden + human-readable sizes (most useful combination)
ls -lah

# List a specific folder without going into it
ls -l /var/log
```

**Example output of `ls -lah`:**
```
drwxr-xr-x  5 ubuntu ubuntu 4.0K Apr 10 10:23 employee-api
drwxr-xr-x  8 ubuntu ubuntu 4.0K Apr 10 11:01 frontend
-rw-r--r--  1 ubuntu ubuntu  512 Apr 10 09:45 start-all.sh
```

The columns mean: `permissions | owner | group | size | date | name`

---

### 3.3 `cd` — Move to a Different Folder

`cd` stands for **Change Directory**.

```bash
# Go to a specific folder
cd /home/ubuntu/employee-api

# Go into a subfolder from where you are
cd frontend

# Go up one level (back to parent folder)
cd ..

# Go up two levels
cd ../..

# Go back to your home folder (shortcut)
cd ~

# Go back to the folder you were just in (toggle)
cd -
```

> **Tip:** After `cd`, always run `pwd` to confirm you are in the right place.

---

## 4. File & Directory Operations

---

### 4.1 `mkdir` — Create a Folder

```bash
# Create a single folder
mkdir logs

# Create nested folders in one shot (no error if they already exist)
mkdir -p app/config/env
```

---

### 4.2 `touch` — Create an Empty File

```bash
# Create a new empty file
touch notes.txt

# Create multiple files at once
touch a.log b.log c.log
```

> **Also used to:** Update the last-modified timestamp of an existing file without changing its contents.

---

### 4.3 `cp` — Copy a File or Folder

```bash
# Copy a file
cp config.yaml config.yaml.backup

# Copy a folder and everything inside it (-r = recursive)
cp -r frontend/ frontend_backup/

# Copy and preserve original timestamps and permissions
cp -p app.py app_v2.py
```

---

### 4.4 `mv` — Move or Rename

```bash
# Rename a file
mv old_name.txt new_name.txt

# Move a file into a folder
mv app.log /var/log/archive/

# Move all .log files to a folder
mv *.log /var/log/archive/
```

---

### 4.5 `rm` — Delete Files or Folders

```bash
# Delete a single file
rm old_notes.txt

# Delete a folder and everything inside it
rm -r build/

# Force delete without asking for confirmation
rm -f temp.lock

# Force delete a folder recursively — USE WITH EXTREME CAUTION
rm -rf node_modules/
```

> ⚠️ **WARNING:** `rm` is permanent. There is no Recycle Bin in the terminal. Always double-check the path before running `rm -rf`. Never run `rm -rf /` or `rm -rf ~`.

---

### 4.6 `chmod` — Change File Permissions

Permissions control who can read, write, or run a file.

```bash
# Make a script executable (so you can run it)
chmod +x start-all.sh

# Give full access to owner, read+execute to everyone else
chmod 755 /home/ubuntu

# Give read+write to owner, read-only to everyone else
chmod 644 config.yaml

# Apply permissions recursively to all files inside a folder
chmod -R 755 frontend/build
```

**Understanding permission numbers:**

| Number | Meaning |
|--------|---------|
| `7` | Read + Write + Execute (rwx) |
| `6` | Read + Write (rw-) |
| `5` | Read + Execute (r-x) |
| `4` | Read only (r--) |

The three digits represent: **owner**, **group**, **everyone else** — in that order.

---

### 4.7 `chown` — Change Who Owns a File

```bash
# Change the owner of a file
chown ubuntu app.log

# Change owner and group
chown www-data:www-data /var/www/html

# Change ownership recursively for a whole folder
chown -R ubuntu /home/ubuntu/frontend
```

---

## 5. Viewing File Contents

---

### 5.1 `cat` — Print a File to the Terminal

```bash
# Print the whole file
cat config.yaml

# Print with line numbers
cat -n app.py
```

> **Best for:** Short files. For large files, use `less` instead.

---

### 5.2 `less` — Read Large Files Page by Page

```bash
less application.log
```

**Controls inside `less`:**

| Key | Action |
|-----|--------|
| Arrow keys / PgUp / PgDn | Scroll up and down |
| `/searchword` | Search forward |
| `n` | Jump to next search result |
| `q` | Quit |

---

### 5.3 `head` and `tail` — See the Start or End of a File

```bash
# See the first 20 lines of a file
head -n 20 employee.log

# See the last 50 lines of a file
tail -n 50 salary.log

# Watch a log file in real-time as new lines are added
tail -f attendance.log
```

> **`tail -f` is extremely useful** when a service is running and you want to watch its output live. Press `Ctrl + C` to stop.

---

### 5.4 `nano` — Simple Text Editor

```bash
# Open a file to edit
nano config.yaml
```

**Controls inside `nano`:**

| Shortcut | Action |
|----------|--------|
| `Ctrl + O` then `Enter` | Save the file |
| `Ctrl + X` | Exit nano |
| `Ctrl + W` | Search inside the file |
| `Ctrl + K` | Cut the current line |
| `Ctrl + U` | Paste the cut line |

---

## 6. System Information & Monitoring

---

### 6.1 `df` — How Much Disk Space is Left?

```bash
# Show disk space for all drives in human-readable sizes
df -h
```

**Example output:**
```
Filesystem      Size  Used Avail Use% Mounted on
/dev/root        20G  8.1G   11G  43% /
```

> **Check this before** running `npm install` or `mvn build` — both can use several GB.

---

### 6.2 `du` — How Big is This Folder?

```bash
# Total size of a folder
du -sh node_modules/

# Size of each item in current directory
du -sh *
```

---

### 6.3 `top` — Live CPU and Memory Usage

```bash
top
```

Shows a live updating list of all running processes. Press `q` to quit.

```bash
# Better version with colors (install first)
sudo apt install htop -y
htop
```

---

### 6.4 `free` — How Much RAM is Being Used?

```bash
free -h
```

**Example output:**
```
              total   used   free
Mem:           3.8G   2.1G   1.7G
Swap:          1.0G   0.0G   1.0G
```

---

### 6.5 `uname` — What OS and Kernel is This?

```bash
# Kernel version
uname -r

# Full system info
uname -a

# OS name and version
cat /etc/os-release
```

---

## 7. Searching & Filtering

---

### 7.1 `grep` — Search for Text Inside Files or Output

`grep` is one of the most useful commands you will use every day.

```bash
# Search for a word in a file
grep "ERROR" app.log

# Case-insensitive search (finds error, ERROR, Error)
grep -i "error" app.log

# Show line numbers alongside matches
grep -n "ERROR" app.log

# Search inside all files in a folder (recursively)
grep -r "employee_salary" ~/salary-api/src/

# Show lines that do NOT contain a word
grep -v "DEBUG" app.log

# Count how many lines match
grep -c "ERROR" app.log

# Show 3 lines after each match (for context)
grep -A 3 "Exception" salary.log

# Show 3 lines before each match
grep -B 3 "FATAL" salary.log
```

---

### 7.2 `find` — Search for Files by Name

```bash
# Find a file by exact name
find ~ -name "config.yaml"

# Find all .log files
find /var/log -name "*.log"

# Find only folders (not files)
find ~/salary-api -type d

# Find files modified in the last 1 day
find /tmp -mtime -1

# Find files larger than 100 MB
find / -size +100M
```

---

### 7.3 `wc` — Count Lines, Words, or Characters

```bash
# Count lines in a file
wc -l employee.log

# Count lines in filtered output
cat app.log | grep ERROR | wc -l
```

---

## 8. Networking & Connectivity

---

### 8.1 `curl` — Make HTTP Requests from the Terminal

`curl` lets you call URLs directly from the terminal. You will use this constantly to test whether APIs are running.

```bash
# Basic GET request
curl http://localhost:8080/api/v1/employee/health

# Silent mode (hides progress stats)
curl -s http://localhost/employee/health

# Check only the HTTP status code and headers
curl -I http://localhost

# POST request with JSON data
curl -X POST http://localhost/employee/create \
  -H 'Content-Type: application/json' \
  -d '{"id": "E001", "name": "John"}'

# Pretty-print the JSON response
curl -s http://localhost/employee/search/all | python3 -m json.tool
```

---

### 8.2 `ping` — Test if a Host is Reachable

```bash
# Send 4 packets and stop
ping -c 4 google.com

# Test your own machine (loopback — always works if networking is fine)
ping -c 4 127.0.0.1
```

---

### 8.3 `ss` — Check Which Ports are Open

```bash
# Show all TCP ports currently listening
ss -tlnp

# Check if a specific port is in use
ss -tlnp | grep :8080
```

> **In OT-Microservices**, you expect these ports to be listening when everything is running:
> `80` (Nginx), `8080` (Go), `8081` (Python), `8082` (Java), `9042` (ScyllaDB), `5432` (PostgreSQL), `6379` (Redis)

---

### 8.4 `wget` — Download a File

```bash
# Download to current folder
wget https://example.com/file.tar.gz

# Download to a specific folder
wget -P lib/ https://jdbc.postgresql.org/download/postgresql-42.7.2.jar
```

---

## 9. Process Management

---

### 9.1 `ps` — See What's Running

```bash
# Full list of all running processes
ps aux

# Filter for a specific process
ps aux | grep java
ps aux | grep gunicorn
```

---

### 9.2 `kill` — Stop a Process

```bash
# Graceful stop (give the process a chance to clean up)
kill 12345

# Force kill (immediate — use only if regular kill doesn't work)
kill -9 12345

# Kill all processes with a given name
pkill gunicorn
```

> **Note:** Always try `kill PID` first. Use `kill -9` only as a last resort since it doesn't allow the process to clean up.

---

### 9.3 `nohup` — Keep a Process Running After You Log Out

When you run a command normally and close your terminal, the process stops. `nohup` prevents this.

```bash
# Run a command in the background, keep it running after logout
nohup ./employee-api > employee.log 2>&1 &

# The & at the end puts it in the background
# > employee.log sends output to a log file
# 2>&1 also captures errors into the same log file
```

After running this, you will see something like:
```
[1] 18432
```
That number (`18432`) is the **Process ID (PID)**. Keep it — you need it to stop the process later with `kill 18432`.

---

## 10. Pipes & Redirection

The real power of Linux comes from combining commands. The `|` symbol (pipe) sends the output of one command into another.

---

### 10.1 The Pipe `|`

```bash
# Show only java processes (filter ps output with grep)
ps aux | grep java

# Count how many ERROR lines are in a log
cat app.log | grep ERROR | wc -l

# Watch logs in real-time but only show errors
tail -f app.log | grep ERROR
```

---

### 10.2 Redirection Operators

| Operator | Meaning | Example |
|----------|---------|---------|
| `>` | Write output to a file (overwrites) | `echo "hello" > file.txt` |
| `>>` | Append output to a file | `echo "hello" >> file.txt` |
| `2>&1` | Merge error output into standard output | `command > out.log 2>&1` |

---

## 11. `sudo` — Running as Root

Some commands need administrator (root) privileges. `sudo` lets you run a single command as root without switching users.

```bash
# Run one command as root
sudo systemctl restart nginx

# Edit a system file
sudo nano /etc/nginx/sites-available/ot-microservices

# Run a command as a different user
sudo -u postgres psql

# Re-run your last command with sudo (useful when you forget)
sudo !!
```

> ⚠️ **Be careful with sudo.** Mistakes made as root can break the entire system. Only use it when necessary.

---

## 12. Shell Shortcuts & History

These will save you a lot of time.

| Shortcut | What it Does |
|----------|-------------|
| `Tab` | Autocomplete a command or filename |
| `Tab Tab` | Show all possible completions |
| `Ctrl + C` | Cancel the currently running command |
| `Ctrl + L` | Clear the screen |
| `Ctrl + R` | Search through your command history |
| `↑ / ↓` arrows | Scroll through previous commands |
| `!!` | Repeat the last command |
| `!42` | Repeat command number 42 from history |
| `Ctrl + A` | Jump to beginning of the line |
| `Ctrl + E` | Jump to end of the line |
| `Alt + Backspace` | Delete one word at a time |

```bash
# See your recent command history
history

# Search history for a specific command
history | grep curl
```

> **`Ctrl + R` tip:** Press it and start typing any part of a previous command. It will find the most recent match. Press `Enter` to run it.

---

## 13. Commands Used in OT-Microservices Deployment

This section lists the exact commands from the deployment guide and explains **what each one actually does** in plain language.

---

### 13.1 System Setup

```bash
# Update the list of available packages from the internet
sudo apt update

# Install all pending upgrades
sudo apt upgrade -y

# Install multiple tools at once
# curl=download tool, wget=download tool, git=version control,
# nano=text editor, net-tools=network utils, build-essential=compilers
sudo apt install -y curl wget git nano net-tools build-essential
```

---

### 13.2 Cloning the Repository

```bash
# Download the source code from GitHub to your current folder
git clone https://github.com/OT-MICROSERVICES/employee-api.git

# Check that the folder was created
ls
```

---

### 13.3 Checking If a Service Started Successfully

After starting any service, always verify it is actually running:

```bash
# Check if the Go Employee API responded correctly
curl http://localhost:8080/api/v1/employee/health

# Check the Attendance API (Python)
curl http://localhost:8081/api/v1/attendance/health

# Check the Salary API (Java)
curl http://localhost:8082/actuator/health

# Check all ports at once — you should see 8080, 8081, 8082, 80
ss -tlnp
```

---

### 13.4 Reading Logs When Something Goes Wrong

```bash
# Watch the Go Employee API log live
tail -f ~/employee.log

# Watch the Python Attendance API log live
tail -f ~/attendance.log

# Watch the Java Salary API log live
tail -f ~/salary.log

# Search for errors in a specific log file
grep -i "error" ~/salary.log

# Check Nginx errors
sudo tail -f /var/log/nginx/error.log
```

---

### 13.5 Starting and Stopping Services

```bash
# Start a service
sudo systemctl start nginx
sudo systemctl start postgresql
sudo systemctl start redis-server
sudo systemctl start scylla-server

# Stop a service
sudo systemctl stop nginx

# Restart a service (stop + start)
sudo systemctl restart nginx

# Reload config without fully restarting (Nginx supports this)
sudo systemctl reload nginx

# Check if a service is running
sudo systemctl status nginx

# Enable a service to start automatically on server reboot
sudo systemctl enable nginx
```

---

### 13.6 Working with the Go Employee API

```bash
# Go into the project folder
cd ~/employee-api

# Download all code dependencies
go mod tidy

# Build the application (creates a binary file called employee-api)
go build -o employee-api

# Run the migrations (creates the database tables)
make run-migrations

# Start the API in the background and log output to employee.log
export GIN_MODE=release
nohup ./employee-api > ~/employee.log 2>&1 &

# Confirm it started
curl http://localhost:8080/api/v1/employee/health
```

---

### 13.7 Working with the Python Attendance API

```bash
cd ~/attendance-api

# Tell Poetry to use Python 3.11
poetry env use /usr/bin/python3.11

# Install all Python dependencies
poetry install

# Run migrations to create the attendance database tables
make run-migrations

# Start the API using Gunicorn on port 8081
nohup poetry run gunicorn --bind 0.0.0.0:8081 app:app > ~/attendance.log 2>&1 &

# Confirm it started
curl http://localhost:8081/api/v1/attendance/health
```

---

### 13.8 Working with the Java Salary API

```bash
cd ~/salary-api

# Build the project (skipping tests since they need a running database)
mvn clean install -DskipTests

# Start the API (the JAR file is the compiled application)
nohup java -jar target/salary-0.1.0-RELEASE.jar > ~/salary.log 2>&1 &

# Java takes 30-60 seconds to start. Wait, then check:
curl http://localhost:8082/actuator/health
```

---

### 13.9 Building and Deploying the React Frontend

```bash
cd ~/frontend

# Fix the homepage path (makes assets work on any server)
sed -i 's|"homepage": "https://opstree.github.io"|"homepage": "."|' package.json

# Install all JavaScript dependencies
npm install

# This flag fixes a compatibility issue between the old build tool (Webpack 4)
# and newer versions of Node.js
export NODE_OPTIONS=--openssl-legacy-provider

# Build the production version of the React app
npm run build

# Give Nginx permission to read the build output
sudo chmod 755 /home/ubuntu
sudo chmod -R 755 /home/ubuntu/frontend/build

# Reload Nginx so it picks up the new build
sudo systemctl reload nginx

# Test that the frontend is being served
curl -I http://localhost
```

---

### 13.10 Testing the Database Connections

```bash
# Connect to ScyllaDB (the NoSQL database)
cqlsh localhost 9042 -u scylladb -p password

# Inside cqlsh — check the tables exist
DESCRIBE KEYSPACE employee_db;

# Connect to PostgreSQL (the relational database)
psql -h 127.0.0.1 -U postgres -d attendance_db

# Inside psql — list tables
\dt

# Test Redis (the cache)
redis-cli ping
# Expected response: PONG
```

---

### 13.11 Stopping the Background Services

When you need to stop the APIs (e.g., to restart after a code change):

```bash
# Find the process ID of a running service
ps aux | grep employee-api
ps aux | grep gunicorn
ps aux | grep salary

# Stop it using the PID you found above
kill <PID>

# Or stop all processes matching a name at once
pkill -f employee-api
pkill -f gunicorn
pkill -f salary
```

---

## 14. Conclusion

This SOP covers the Linux commands you need to work on the OT-Microservices project from day one. 

**A simple learning path if you are new:**

1. Start with **Section 3 and 4** — navigation and file operations. Practice moving around and creating files.
2. Move to **Section 5** — `cat`, `tail -f`, and `nano` will be your most used commands for reading logs and editing configs.
3. Then **Section 7** — `grep` is something you will use every single day.
4. Finally **Section 13** — read through the deployment commands and run them alongside the Deployment Guide.

> **Remember:** You can always look up any command using `man <command>`. For example, `man ls` shows the full manual for the `ls` command.

---

## 15. References

| Resource | Link |
|----------|------|
| OT-Microservices Repository | https://github.com/OT-MICROSERVICES | |
| Ubuntu Man Pages | https://manpages.ubuntu.com |
| Linux Command Library | https://linuxcommandlibrary.com |
| Explain Shell (breaks down any command) | https://explainshell.com |

---

*Author: Deepak | Sprint 0 | Infra-Titans | April 2026*
