# Ansible Inventory — Dynamic Inventory Documentation

**OT-Microservices | DevOps Engineering — Sprint 0**

> Author: Deepak |  April 2026

---

| Author | Created On | Version | Last Updated By | Last Edited On | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|--------|------------|---------|-----------------|----------------|--------------|-------------|-------------|-------------|
| Deepak | April 2026 | v1.0 | Deepak | April 2026 | | | | |

---

## Table of Contents

1. [What Is Ansible Inventory?](#1-what-is-ansible-inventory)
2. [Static vs Dynamic Inventory](#2-static-vs-dynamic-inventory)
3. [How Dynamic Inventory Works](#3-how-dynamic-inventory-works)
4. [Cloud Source: AWS EC2](#4-cloud-source-aws-ec2)
5. [Database Source: PostgreSQL (CMDB)](#5-database-source-postgresql-cmdb)
6. [Testing Your Inventory](#6-testing-your-inventory)
7. [Best Practices](#7-best-practices)
8. [Common Errors and Fixes](#8-common-errors-and-fixes)
9. [Conclusion](#9-conclusion)
10. [References](#10-references)

---

## 1. What Is Ansible Inventory?

An Ansible inventory is simply a **list of target machines** that Ansible will connect to and manage. Before Ansible can run a playbook on any server, it needs to know:

- The server's IP address or hostname
- Which group it belongs to (e.g., `employee_api`, `databases`)
- How to connect to it (SSH user, key, port)

Inventories come in two forms — **static** and **dynamic**.

---

## 2. Static vs Dynamic Inventory

| Feature | Static Inventory | Dynamic Inventory |
|---|---|---|
| Definition | A manually written file with IPs/hostnames | A script or plugin that queries a live source |
| Update frequency | Manual — someone must edit the file | Automatic — refreshed every time Ansible runs |
| Cloud environments | Breaks when IPs change | Always current — reflects live state |
| Grouping | Manual | Automatic (by cloud tags, DB fields, etc.) |
| Best for | Small, fixed server lists | Cloud or frequently changing infrastructure |

> **In short:** If servers are created and destroyed regularly (like EC2 instances), static inventory is impractical. Dynamic inventory solves this by fetching the live server list at runtime.

---

## 3. How Dynamic Inventory Works

When you use a dynamic inventory source, this is what happens each time you run a playbook:

1. Ansible calls the inventory **plugin or script** before the playbook starts
2. The plugin queries an **external source** (AWS API, PostgreSQL table, etc.)
3. The source returns a **JSON list** of current hosts and their groups
4. Ansible uses this as if you had written a static file — but it's always up to date

```
Developer runs: ansible-playbook -i inventories/ site.yml
                        │
                        ▼
            Inventory plugin/script runs
                        │
                        ▼
         Queries AWS / Database for live hosts
                        │
                        ▼
        Returns JSON: { "employee_api": ["10.0.1.10"], ... }
                        │
                        ▼
         Ansible runs the playbook against live hosts
```

---

## 4. Cloud Source: AWS EC2

The `amazon.aws.aws_ec2` plugin queries the AWS EC2 API and automatically groups instances based on their **tags**.

### 4.1 Prerequisites

```bash
# Install required Python library
pip install boto3 botocore

# Install the AWS Ansible collection
ansible-galaxy collection install amazon.aws

# Configure AWS credentials
aws configure
```

### 4.2 Plugin Configuration File

Create `inventories/aws_ec2.yml` — the filename **must** end in `aws_ec2.yml`:

```yaml
plugin: amazon.aws.aws_ec2

# AWS region to query
regions:
  - ap-south-1

# Only return running instances
filters:
  instance-state-name: running

# Group hosts by their EC2 tags
keyed_groups:
  - key: tags.Service
    prefix: service
  - key: tags.Environment
    prefix: env

# Use private IP to connect (within VPC)
compose:
  ansible_host: private_ip_address
  ansible_user: ubuntu
```

### 4.3 EC2 Tagging Strategy for OT-Microservices

Tag your EC2 instances like this when launching them:

| EC2 Instance | Tag: Service | Tag: Environment | Ansible Group |
|---|---|---|---|
| Employee API server | `employee-api` | `production` | `service_employee_api` |
| Salary API server | `salary-api` | `production` | `service_salary_api` |
| Attendance API server | `attendance-api` | `production` | `service_attendance_api` |
| Frontend server | `frontend` | `production` | `service_frontend` |
| ScyllaDB server | `scylladb` | `production` | `service_scylladb` |
| PostgreSQL server | `postgresql` | `production` | `service_postgresql` |

---

## 5. Database Source: PostgreSQL (CMDB)

If your team maintains a server registry in a PostgreSQL database (a CMDB), Ansible can query it directly using a Python script. This is useful for on-premises servers or any host not managed by a cloud provider.

Since OT-Microservices already uses PostgreSQL (for the Attendance API), a CMDB table can live in the same database.

### 5.1 Create the CMDB Table

```sql
-- Run inside psql connected to attendance_db
CREATE TABLE ansible_hosts (
    id            SERIAL PRIMARY KEY,
    hostname      TEXT NOT NULL,
    ip_address    TEXT NOT NULL,
    ansible_group TEXT NOT NULL,
    ssh_user      TEXT DEFAULT 'ubuntu',
    service       TEXT,
    active        BOOLEAN DEFAULT true
);

-- Insert OT-Microservices servers
INSERT INTO ansible_hosts (hostname, ip_address, ansible_group, service) VALUES
  ('employee-api-01',  '10.0.1.10', 'employee_api',  'employee-api'),
  ('salary-api-01',    '10.0.1.11', 'salary_api',    'salary-api'),
  ('attendance-api-01','10.0.1.12', 'attendance_api','attendance-api'),
  ('frontend-01',      '10.0.1.13', 'frontend',      'frontend'),
  ('scylladb-01',      '10.0.1.20', 'databases',     'scylladb'),
  ('postgres-01',      '10.0.1.21', 'databases',     'postgresql');
```

### 5.2 Dynamic Inventory Script

Create `inventories/db_inventory.py`:

```python
#!/usr/bin/env python3
# Usage: ansible-playbook -i inventories/db_inventory.py site.yml

import json, sys, os
import psycopg2

DB_CONFIG = {
    'host':     os.getenv('CMDB_HOST',     '127.0.0.1'),
    'port':     os.getenv('CMDB_PORT',     '5432'),
    'dbname':   os.getenv('CMDB_DBNAME',   'attendance_db'),
    'user':     os.getenv('CMDB_USER',     'postgres'),
    'password': os.getenv('CMDB_PASSWORD', 'password'),
}

def get_inventory():
    conn = psycopg2.connect(**DB_CONFIG)
    cur  = conn.cursor()
    cur.execute('SELECT hostname, ip_address, ansible_group, ssh_user FROM ansible_hosts WHERE active = true')
    rows = cur.fetchall()
    cur.close(); conn.close()

    inventory = { '_meta': { 'hostvars': {} }, 'all': { 'children': [] } }

    for hostname, ip, group, user in rows:
        if group not in inventory:
            inventory[group] = { 'hosts': [] }
            inventory['all']['children'].append(group)
        inventory[group]['hosts'].append(hostname)
        inventory['_meta']['hostvars'][hostname] = {
            'ansible_host': ip,
            'ansible_user': user,
        }

    return inventory

if __name__ == '__main__':
    if '--list' in sys.argv:
        print(json.dumps(get_inventory(), indent=2))
    elif '--host' in sys.argv:
        print(json.dumps({}))
```

```bash
# Make it executable
chmod +x inventories/db_inventory.py
```

> **Note:** Use environment variables for DB credentials. Never hardcode passwords in the script.

---

## 6. Testing Your Inventory

### List all hosts and groups

```bash
# AWS EC2
ansible-inventory -i inventories/aws_ec2.yml --list

# Database source
ansible-inventory -i inventories/db_inventory.py --list
```

### View the group tree

```bash
ansible-inventory -i inventories/aws_ec2.yml --graph
```

**Example output:**
```
@all:
  |--@service_employee_api:
  |  |--10.0.1.10
  |--@service_salary_api:
  |  |--10.0.1.11
  |--@service_attendance_api:
  |  |--10.0.1.12
  |--@service_frontend:
  |  |--10.0.1.13
```

### Ping a specific group

```bash
ansible -i inventories/aws_ec2.yml service_employee_api -m ping
```

### Combine multiple sources (directory inventory)

```
inventories/
├── aws_ec2.yml          # Cloud hosts from AWS
├── db_inventory.py      # On-premises hosts from database
└── group_vars/
    └── all.yml          # Variables applied to all hosts
```

```bash
# Ansible merges all sources automatically
ansible-playbook -i inventories/ site.yml
```

---

## 7. Best Practices

| Practice | Why It Matters |
|---|---|
| Tag all cloud resources consistently | Tags drive dynamic grouping — without them, all hosts land in one group |
| Use environment variables for credentials | Never hardcode AWS keys or DB passwords in config files |
| Always run `--list` before a playbook | Verify the host list looks correct before deploying |
| Use `ansible_host` to set the connection IP | Relying on DNS resolution is fragile in cloud environments |
| Document your tagging strategy in a README | New team members need to know which tags map to which groups |
| Pin collection versions in `requirements.yml` | Prevents breaking changes when upstream collections update |

---

## 8. Common Errors and Fixes

| Error | Cause | Fix |
|---|---|---|
| `No hosts matched` | Filters too strict or EC2 tags missing | Remove filters temporarily and run `--list` to see what the plugin returns |
| `botocore.exceptions.NoCredentialsError` | AWS credentials not configured | Run `aws configure` or export `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` |
| `Plugin not found: amazon.aws.aws_ec2` | Collection not installed | Run `ansible-galaxy collection install amazon.aws` |
| `psycopg2.OperationalError: could not connect` | Wrong DB host/port or firewall blocking port 5432 | Check DB connection details and firewall rules |
| `Permission denied (publickey)` | SSH key not set for the inventory hosts | Add `ansible_ssh_private_key_file` in `group_vars/all.yml` |
| `Script is not executable` | `chmod` not set on inventory script | Run `chmod +x inventories/db_inventory.py` |

---

## 9. Conclusion

Dynamic inventory removes the biggest operational headache of Ansible at scale: keeping a list of servers up to date. Instead of manually editing a file every time an EC2 instance is launched or terminated, the inventory plugin does it for you — automatically, every time you run a playbook.

For OT-Microservices, the recommended setup is:

- Use `aws_ec2` plugin for all cloud-hosted services
- Apply consistent `Service` and `Environment` tags to all EC2 instances
- Optionally use the PostgreSQL CMDB script for any on-premises or non-cloud hosts
- Point Ansible at the `inventories/` directory to merge both sources

With this in place, adding a new server to your fleet requires zero changes to any Ansible configuration file — just tag it correctly and it appears automatically.

---

## 10. References

- [Ansible Inventory Guide](https://docs.ansible.com/ansible/latest/inventory_guide/)
- [amazon.aws.aws_ec2 Plugin](https://docs.ansible.com/ansible/latest/collections/amazon/aws/aws_ec2_inventory.html)
- [GCP Compute Inventory Plugin](https://docs.ansible.com/ansible/latest/collections/google/cloud/gcp_compute_inventory.html)
- [Writing a Custom Inventory Script](https://docs.ansible.com/ansible/latest/dev_guide/developing_inventory.html)
- [OT-Microservices Repository](https://github.com/OT-MICROSERVICES)

---

> **Document Owner:** Deepak ||                     **Last Updated:** April 2026
