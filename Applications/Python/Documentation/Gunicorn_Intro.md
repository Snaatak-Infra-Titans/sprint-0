# Gunicorn — Introduction

## Document Details



| Author  | Created On     | Version | Last Updated By | Last Edited On | L0 Reviewer  | L1 Reviewer  | L2 Reviewer   |
|---------|----------------|---------|------------------|----------------|--------------|--------------|---------------|
| Deepak  | 14 April 2026  | v1.1    | Deepak           | 22 April 2026  | Mohit Kumar  | Faisal Khan  | Mahesh Kumar  |


## Table of Contents

1. [Introduction](#1-introduction)
2. [What is Gunicorn?](#2-what-is-gunicorn)
3. [Why Gunicorn?](#3-why-gunicorn)
4. [Key Features](#4-key-features)
5. [Conclusion](#5-conclusion)
6. [Contact Information](#6-contact-information)
7. [References](#7-references)


## 1. Introduction

Gunicorn is used to run Python web applications in production.

It helps handle multiple users and requests efficiently.



## 2. What is Gunicorn?

Gunicorn is a **WSGI HTTP server** for Python applications.

| Attribute | Meaning |
|-----------|--------|
| Type | WSGI Server |
| Language | Python |
| Use | Runs web applications |
| Compatibility | Flask, Django |



## 3. Why Gunicorn?

Flask/Django development servers are not suitable for production.

| Limitation (Dev Server) | Solution (Gunicorn) |
|------------------------|--------------------|
| Single request handling | Multiple workers |
| No reliability | Auto restart |
| Not production ready | Production grade |
| Poor performance | Efficient handling |



## 4. Key Features

| Feature | Description |
|---------|------------|
| Pre-fork Workers | Multiple processes handle requests |
| Concurrency | Handles many users at once |
| Auto Restart | Recovers from crashes |
| Easy Setup | Simple command-based usage |
| Scalable | Can increase workers |


## 5. Conclusion

Gunicorn makes Python applications production-ready by improving performance and reliability.





##  References

| Description | Link |
|-------------|------|
| Official Gunicorn documentation | [Gunicorn](https://gunicorn.org) |
| Gunicorn configuration guide | [Gunicorn Docs](https://docs.gunicorn.org/en/stable/settings.html) |


##  Contact Information

| Name |  | Contact |
|------|------|--------|
| Deepak |  | deepak.nagar.snaatak@mygurukulam.co |


