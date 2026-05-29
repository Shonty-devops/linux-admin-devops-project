# Day 01 - Linux Reconnaissance & System Assessment

---

# Introduction

Congratulations! You've just joined LabEx Corporation as a Junior System Administrator.

Your first assignment involves supporting the company's most ambitious initiative yet — **Project Phoenix**, a next-generation platform designed to revolutionize digital workflow management for enterprise environments.

Before any infrastructure deployment or operational activity can begin, a system administrator must first understand the environment they are working with. This process is commonly referred to as **system reconnaissance**.

In this lab, the objective was to investigate and assess the Linux server environment by gathering critical operational details such as:

* current user identity
* operating system information
* kernel details
* server uptime
* system load
* user permissions
* group memberships
* real-time resource utilization

This foundational assessment establishes operational awareness and prepares administrators for future infrastructure management, troubleshooting, and DevOps workflows.

---

# Objective

The primary objectives of this lab were to:

* Understand the Linux operating environment
* Perform basic system reconnaissance
* Gather server operational details
* Analyze user and permission information
* Monitor real-time system activity
* Generate a system status report for documentation purposes

---

# Skills Covered

* Linux CLI navigation
* System reconnaissance
* User identification
* Kernel inspection
* Uptime analysis
* Permission awareness
* Resource monitoring
* Output redirection
* Report generation

---

# Linux Commands Used

```bash
whoami
uname
uname -a
uptime
id
top
touch
echo
cat
```

---

# Task 1 - First Login & Environment Verification

## Problem Statement

As a newly assigned administrator for Project Phoenix, the first step was to verify:

* the currently logged-in user
* the Linux operating system kernel

This helps ensure that administrative tasks are being performed on the correct system using the expected user account.

---

# Commands Used

```bash
whoami
uname
```

---

# Solution

```bash
labex:project/ $ whoami
labex

labex:project/ $ uname
Linux
```

---

# Output Explanation

| Command  | Purpose                                   |
| -------- | ----------------------------------------- |
| `whoami` | Displays the currently logged-in username |
| `uname`  | Displays the operating system kernel name |

The output confirmed:

* the active user account was `labex`
* the operating system kernel was Linux

---

# Why This Matters

User verification and OS identification are important during:

* server onboarding
* infrastructure validation
* SSH session verification
* cloud instance administration
* DevOps troubleshooting

These are standard reconnaissance steps performed before managing production infrastructure.

---

# Task 2 - Checking System Information & Uptime

## Problem Statement

After confirming user identity, the next step was to analyze:

* system architecture
* kernel version
* operating system details
* server uptime
* current system load

This information helps administrators understand the server environment and monitor operational stability.

---

# Commands Used

```bash
uname -a
uptime
```

---

# Solution

```bash
labex:project/ $ uname -a
Linux 6a127fc345bfee65e73322e5 6.8.0-111-generic #111-Ubuntu SMP PREEMPT_DYNAMIC Sat Apr 11 23:16:02 UTC 2026 x86_64 x86_64 x86_64 GNU/Linux

labex:project/ $ uptime
12:37:50 up 11 days, 1:27, 0 users, load average: 0.08, 0.33, 0.39
```

---

# Output Explanation

## `uname -a`

Displays:

* kernel version
* hostname
* architecture
* operating system details

Important information identified:

* Ubuntu Linux environment
* x86_64 architecture
* active Linux kernel version

---

## `uptime`

Displays:

* current server uptime
* active users
* system load averages

Load averages indicate CPU demand over:

* 1 minute
* 5 minutes
* 15 minutes

The server had:

* stable uptime
* low load averages
* healthy operational condition

---

# DevOps Relevance

Commands like `uname` and `uptime` are frequently used in:

* cloud server management
* Kubernetes node inspection
* Linux troubleshooting
* infrastructure monitoring
* CI/CD agent validation
* DevOps operational checks

---

# Task 3 - Gathering User & Group Information

## Problem Statement

Linux permissions are heavily based on:

* user identities
* group memberships
* access privileges

Understanding user and group assignments is essential for secure infrastructure management.

---

# Command Used

```bash
id
```

---

# Solution

```bash
labex:project/ $ id

uid=5000(labex) gid=5000(labex) groups=5000(labex),27(sudo),121(ssl-cert),5002(public)
```

---

# Output Explanation

| Field    | Meaning                      |
| -------- | ---------------------------- |
| `uid`    | User ID                      |
| `gid`    | Primary Group ID             |
| `groups` | Additional group memberships |

The output showed:

* the user belongs to the `sudo` group
* the user has elevated administrative permissions
* additional group memberships provide access to shared resources

---

# Why This Matters

Understanding Linux permissions is critical for:

* access control
* infrastructure security
* CI/CD environments
* shared development servers
* Kubernetes node management
* production administration

---

# Task 4 - Real-Time System Monitoring

## Problem Statement

A Linux administrator must constantly monitor system health and resource utilization.

The goal of this task was to observe:

* CPU usage
* memory consumption
* active processes
* system performance

using Linux's real-time monitoring tools.

---

# Command Used

```bash
top
```

---

# Solution

```bash
labex:project/ $ top
```

---

# Monitoring Overview

The `top` utility provides:

* real-time process monitoring
* CPU utilization
* memory analysis
* process prioritization
* load statistics
* running task information

---

# Key Metrics Observed

| Metric       | Description                    |
| ------------ | ------------------------------ |
| CPU Usage    | Active processor utilization   |
| Memory Usage | RAM consumption                |
| Load Average | System workload                |
| Tasks        | Running and sleeping processes |
| PID          | Process identifiers            |

---

# Operational Importance

The `top` command is widely used for:

* production troubleshooting
* identifying resource-heavy applications
* server monitoring
* infrastructure diagnostics
* performance analysis

This is one of the most important Linux administration tools.

---

# Task 5 - Generating a System Status Report

## Problem Statement

Documentation and reporting are essential operational responsibilities for Linux Administrators.

The goal of this task was to:

* capture important system details
* save command outputs
* create a reusable system report

using Linux output redirection.

---

# Commands Used

```bash
touch system_report.txt
echo
cat
>
>>
```

---

# Solution

```bash
labex:project/ $ cd ~/project

labex:project/ $ touch system_report.txt

labex:project/ $ echo -e "$(whoami)" > system_report.txt

labex:project/ $ echo -e "$(uname -a)" >> system_report.txt

labex:project/ $ echo -e "$(uptime)" >> system_report.txt

labex:project/ $ cat system_report.txt
```

---

# Generated Report Output

```bash
labex

Linux 6a127fc345bfee65e73322e5 6.8.0-111-generic #111-Ubuntu SMP PREEMPT_DYNAMIC Sat Apr 11 23:16:02 UTC 2026 x86_64 x86_64 x86_64 GNU/Linux

12:55:08 up 11 days, 1:44, 0 users, load average: 0.00, 0.08, 0.25
```

---

# Output Redirection Explanation

| Operator | Function                |
| -------- | ----------------------- |
| `>`      | Creates/overwrites file |
| `>>`     | Appends data to file    |

This approach allows administrators to:

* generate reports
* store logs
* capture troubleshooting information
* automate documentation

---

# Key Learnings

Through this lab, I learned:

* Linux system reconnaissance
* User identity verification
* Kernel and OS inspection
* Server uptime analysis
* Group and permission awareness
* Real-time monitoring techniques
* Output redirection and reporting
* Foundational Linux operational workflows

---

# DevOps & Infrastructure Relevance

This lab established foundational skills required for:

* Linux Administration
* DevOps Engineering
* Cloud Infrastructure
* Kubernetes Operations
* CI/CD environments
* Production troubleshooting
* Infrastructure monitoring

Understanding system reconnaissance is essential before managing:

* containers
* cloud instances
* deployment servers
* Kubernetes nodes
* automation pipelines

---

# Summary

In this lab, I successfully:

* verified Linux user identity
* analyzed system information
* inspected server uptime and load
* reviewed user and group permissions
* monitored real-time system performance
* generated a Linux system assessment report

This exercise strengthened my understanding of Linux system reconnaissance and operational monitoring, which are foundational skills for Linux Administration and DevOps Engineering.
