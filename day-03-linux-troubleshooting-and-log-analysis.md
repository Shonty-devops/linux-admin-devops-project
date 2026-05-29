# Day 03 - Linux Troubleshooting, Log Analysis & Configuration Investigation

---

# Introduction

Day 03 at LabEx Corporation introduced a critical production-style troubleshooting scenario for **Project Phoenix**.

The development team encountered:

* application failures
* deployment instability
* configuration inconsistencies
* production environment issues
* missing deployment assets

Emergency alerts flooded the monitoring systems, deployment pipelines stopped functioning, and users began reporting operational failures.

As the acting infrastructure investigator, the objective was to:

* analyze Linux log files
* inspect system boot messages
* investigate configuration discrepancies
* identify deployment inconsistencies
* uncover the root cause of production instability

This lab closely simulated real-world:

* Linux troubleshooting
* DevOps incident response
* log analysis workflows
* production diagnostics
* environment comparison tasks

---

# Objective

The primary objectives of this lab were to:

* Analyze application log files
* Filter critical error messages
* Investigate kernel-level boot issues
* Examine web server configurations
* Compare staging and production environments
* Identify missing deployment artifacts
* Generate operational troubleshooting reports

---

# Skills Covered

* Linux troubleshooting
* Log analysis
* Pattern matching
* Configuration validation
* Environment comparison
* Deployment verification
* Command pipelines
* Output redirection
* Infrastructure diagnostics

---

# Linux Commands Used

```bash id="3r2k0p"
grep
dmesg
diff
cat
ls
cd
sudo
>
>>
|
```

---

# Task 1 - Reviewing Application Log File Contents

## Problem Statement

The first step in troubleshooting Project Phoenix was investigating the application log file located at:

```bash id="p4r8q2"
~/project/logs/app.log
```

The objective was to:

* identify critical application failures
* isolate ERROR messages
* generate an error report for further investigation

---

# Commands Used

```bash id="s9n2yf"
grep
cat
>
```

---

# Initial Mistake During Investigation

```bash id="7x2rka"
grep "EROR" ~/project/logs/app.log > ~/project/error_report.txt
```

---

# Why the Command Failed

The keyword `EROR` was misspelled.

Linux text filtering is exact by default, so the incorrect pattern returned no results.

This troubleshooting step reinforced:

* attention to detail
* accurate pattern matching
* operational debugging discipline

---

# Final Working Solution

```bash id="5z8vnm"
grep "ERROR" ~/project/logs/app.log > ~/project/error_report.txt
```

---

# Generated Error Report

```bash id="w7o4lt"
[2023-10-26 10:00:03] ERROR: Failed to process payment transaction #12345.

[2023-10-26 10:00:05] ERROR: NullPointerException at com.innovatech.Billing.process(Billing.java:101).
```

---

# Output Explanation

The `grep` command filtered only lines containing:

* `ERROR`

The `>` operator redirected the output into:

* `error_report.txt`

---

# Why This Matters

Log filtering is a core Linux Administration and DevOps troubleshooting skill used for:

* incident investigation
* production debugging
* monitoring analysis
* application diagnostics
* SIEM investigations

---

# Task 2 - Investigating System Boot Messages

## Problem Statement

Application failures may sometimes originate from:

* hardware issues
* driver problems
* kernel failures
* system-level instability

The objective was to inspect Linux kernel boot messages for:

* failures
* errors

using the Linux kernel ring buffer.

---

# Commands Used

```bash id="4kpv5s"
dmesg
grep
sudo
|
```

---

# Initial Permission Issue

```bash id="q9n7lx"
dmesg
```

---

# Error Received

```bash id="l4z8cf"
dmesg: read kernel buffer failed: Operation not permitted
```

---

# Why the Error Happened

Accessing kernel logs requires elevated privileges.

This demonstrated the importance of:

* Linux permissions
* administrative access
* secure operational controls

---

# Final Working Solution

```bash id="b1v8do"
sudo dmesg | grep -iE 'fail|error' > ~/project/boot_issues.txt
```

---

# Kernel Investigation Output

```bash id="8cmv0w"
[    0.331538] acpi PNP0A03:00: fail to add MMCONFIG information

[    1.020305] RAS: Correctable Errors collector initialized.

[   22.813342] kernel: my-driver: probe failed with error -2
```

---

# Command Breakdown

| Command    | Purpose                                    |                               |
| ---------- | ------------------------------------------ | ----------------------------- |
| `dmesg`    | Displays kernel messages                   |                               |
| `sudo`     | Executes with elevated privileges          |                               |
| `grep -iE` | Case-insensitive extended pattern matching |                               |
| `          | `                                          | Pipes output between commands |

---

# Operational Importance

Kernel-level investigations are important for:

* infrastructure troubleshooting
* hardware diagnostics
* Linux server maintenance
* Kubernetes node debugging
* cloud instance analysis

---

# Task 3 - Examining Web Server Configuration

## Problem Statement

The next phase of investigation focused on:

* Nginx configuration analysis
* identifying performance bottlenecks
* validating worker process settings

The goal was to extract the:

* `worker_processes`

directive from the Nginx configuration file.

---

# Commands Used

```bash id="0m2xrs"
cat
grep
>>
```

---

# Initial Mistakes During Investigation

```bash id="q3s6pt"
cd ~/project/config/nginx.conf
```

---

# Why the Error Happened

`nginx.conf` is a file, not a directory.

This reinforced:

* Linux path understanding
* file vs directory distinction
* command accuracy

---

# Additional Typographical Error

```bash id="g7p2vl"
cat nginx.xonf
```

---

# Error Cause

The filename was misspelled:

* `nginx.xonf`
  instead of:
* `nginx.conf`

---

# Final Working Solution

```bash id="m4o8tw"
cat nginx.conf | grep "worker_process" >> ~/project/error_report.txt
```

---

# Updated Error Report

```bash id="x8v4zn"
[2023-10-26 10:00:03] ERROR: Failed to process payment transaction #12345.

[2023-10-26 10:00:05] ERROR: NullPointerException at com.innovatech.Billing.process(Billing.java:101).

worker_processes 4;
```

---

# Why This Matters

Nginx worker process configuration directly affects:

* application scalability
* request handling
* concurrency performance
* infrastructure optimization

This is highly relevant in:

* DevOps Engineering
* load balancing
* production web servers
* cloud infrastructure

---

# Task 4 - Comparing Staging & Production Configurations

## Problem Statement

One of the most common causes of production failures is:

* staging vs production drift

The objective was to compare:

* staging configuration
* production configuration

to identify operational inconsistencies.

---

# Commands Used

```bash id="9f3cly"
diff
cat
>
```

---

# Final Working Solution

```bash id="d2w5or"
diff ~/project/config/staging/app.conf ~/project/config/production/app.conf > ~/project/config_diff.txt
```

---

# Configuration Difference Output

```bash id="f1q7xa"
1,5c1,5

< # Staging Configuration
< database.url=jdbc:mysql://staging-db:3306/nexus
< api.key=staging_key_abc123
< feature.flag.new_dashboard=true
< timeout.ms=3000

---

> # Production Configuration
> database.url=jdbc:mysql://prod-db:3306/nexus
> api.key=prod_key_xyz789
> feature.flag.new_dashboard=false
> timeout.ms=5000
```

---

# Key Differences Identified

| Setting      | Staging     | Production     |
| ------------ | ----------- | -------------- |
| Database     | staging-db  | prod-db        |
| API Key      | staging key | production key |
| Feature Flag | enabled     | disabled       |
| Timeout      | 3000ms      | 5000ms         |

---

# Operational Importance

Configuration drift is a major issue in:

* CI/CD pipelines
* Kubernetes clusters
* Infrastructure-as-Code
* cloud deployments
* DevOps workflows

The `diff` command is essential for:

* configuration audits
* deployment verification
* troubleshooting inconsistencies

---

# Task 5 - Verifying Directory Consistency Between Servers

## Problem Statement

Production instability may also occur due to:

* missing deployment files
* incomplete synchronization
* failed releases

The objective was to compare:

* staging server files
* production server files

to identify missing assets.

---

# Commands Used

```bash id="h8o1wp"
diff -r
cat
>
```

---

# Initial Mistake During Comparison

```bash id="1r0sxe"
diff ~/home/labex/project/server1_files ~/home/labex/project/server2_files
```

---

# Why the Error Happened

The path was incorrect:

* `/home/labex/home/labex/...`

This highlighted the importance of:

* Linux path accuracy
* directory validation
* troubleshooting operational errors

---

# Final Working Solution

```bash id="u2k7ac"
diff -r ~/project/server1_files ~/project/server2_files > ~/project/missing_files.txt
```

---

# Missing File Report

```bash id="y5q9zn"
Only in /home/labex/project/server1_files: asset2.js
```

---

# Investigation Findings

The report confirmed:

* `asset2.js` existed in staging
* the file was missing from production

This likely contributed to:

* deployment instability
* application failures
* inconsistent behavior

---

# Why This Matters

Deployment consistency is critical for:

* Kubernetes deployments
* CI/CD automation
* infrastructure reliability
* production stability
* cloud-native applications

---

# Key Learnings

Through this lab, I learned:

* Linux troubleshooting workflows
* Application log analysis
* Kernel diagnostics
* Configuration validation
* Environment comparison
* File synchronization auditing
* Infrastructure investigation techniques
* Real-world incident response practices

---

# DevOps & Infrastructure Relevance

The operational skills practiced in this lab are directly relevant to:

* DevOps Engineering
* Site Reliability Engineering (SRE)
* Linux Administration
* Production Support
* Infrastructure Monitoring
* Kubernetes Operations
* CI/CD troubleshooting
* Cloud Infrastructure

---

# Summary

In this lab, I successfully:

* investigated application errors
* analyzed Linux kernel messages
* examined Nginx configuration settings
* compared staging and production environments
* identified missing deployment assets
* generated operational troubleshooting reports

This exercise strengthened my Linux troubleshooting and infrastructure investigation skills while simulating real-world DevOps incident response workflows.
