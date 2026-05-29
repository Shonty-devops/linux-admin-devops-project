# Day 06 - Linux Process Management, Monitoring & Background Job Control

---

# Introduction

A critical performance incident occurred on the main application server at LabEx Corporation. Users experienced severe slowdowns, application response times increased dramatically, and system resources were being exhausted unexpectedly.

As the acting Linux Administrator, the objective was to:

* investigate active system processes
* monitor real-time CPU usage
* identify resource-intensive workloads
* terminate misbehaving processes
* validate critical services
* manage long-running background jobs

This lab simulated real-world Linux process management scenarios commonly encountered in:

* production Linux servers
* DevOps environments
* cloud infrastructure
* CI/CD systems
* application monitoring operations

---

# Objective

The primary goals of this lab were to:

* Inspect running Linux processes
* Monitor system performance in real time
* Identify high CPU-consuming workloads
* Verify critical services
* Terminate problematic processes safely
* Execute persistent background jobs
* Redirect logs and outputs properly

---

# Skills Covered

* Linux process management
* System monitoring
* Resource troubleshooting
* Process termination
* Background job execution
* Output redirection
* Linux administration
* DevOps operational troubleshooting

---

# Linux Commands Used

```bash id="m1q8vs"
ps
top
pgrep
pkill
nohup
grep
kill
&
2>&1
```

---

# Task 1 - Listing Active System Processes

## Problem Statement

The first step in troubleshooting a Linux server slowdown is understanding:

* what processes are running
* who owns them
* how much CPU and memory they consume

The objective was to generate a detailed snapshot of all active system processes.

---

# Command Used

```bash id="v9k2xp"
ps -aux
```

---

# Solution

```bash id="r4t7zn"
labex:project/ $ ps -aux
```

---

# Command Explanation

| Option | Purpose                                     |
| ------ | ------------------------------------------- |
| `a`    | Show processes for all users                |
| `u`    | Display user-oriented output                |
| `x`    | Include processes without terminal sessions |

---

# Example Output

```bash id="p6f1yb"
USER       PID %CPU %MEM COMMAND
root         1  0.0  0.1 /sbin/init
labex     1234 95.0  0.0 resource_hog.sh
labex     1235  0.0  0.0 critical_service.sh
```

---

# Why This Matters

The `ps` command is one of the most essential Linux Administration tools for:

* process auditing
* production troubleshooting
* performance analysis
* infrastructure monitoring

It is heavily used in:

* DevOps operations
* cloud servers
* containerized environments
* Kubernetes worker nodes

---

# Task 2 - Monitoring Real-Time System Performance

## Problem Statement

Static process snapshots were insufficient because system load continuously changed.

The objective was to:

* monitor real-time CPU and memory usage
* identify the top resource-consuming process

---

# Command Used

```bash id="h3w8cn"
top
```

---

# Solution

```bash id="d7x0qa"
labex:project/ $ top
```

---

# Real-Time Monitoring Output

```bash id="n5z2lr"
PID USER      %CPU COMMAND
217 labex    100.0 resource_hog.sh
```

---

# Resource Hog Identified

The process consuming the highest CPU was:

* `resource_hog.sh`

CPU utilization reached:

* `100%`

This explained the production slowdown affecting the server.

---

# Why `top` is Important

The `top` utility provides:

* real-time process monitoring
* CPU usage analysis
* memory consumption tracking
* system load visibility

This tool is widely used in:

* Linux production servers
* DevOps monitoring
* SRE operations
* incident response workflows

---

# Task 3 - Identifying Critical Processes

## Problem Statement

Before terminating any process, it was necessary to:

* verify critical application services
* identify the PID of important workloads

The objective was to locate:

* `critical_service.sh`

---

# Commands Used

```bash id="f4y9mp"
pgrep
ps
```

---

# Finding the PID

```bash id="x8r2kv"
pgrep -f critical_service.sh
```

---

# Example Output

```bash id="q1m7wd"
1235
```

---

# Process Verification

```bash id="j6n0zs"
ps -p 1235 -o pid,ppid,cmd
```

---

# Example Verification Output

```bash id="t2c8eu"
PID PPID CMD
1235 1 /bin/bash /home/labex/project/critical_service.sh
```

---

# Command Explanation

| Command    | Purpose                                  |
| ---------- | ---------------------------------------- |
| `pgrep -f` | Search processes using full command line |
| `ps -p`    | Display details for a specific PID       |

---

# Why This Matters

Process identification is critical before:

* restarting services
* killing workloads
* debugging applications
* performing maintenance

This is standard practice in:

* Linux Administration
* DevOps Engineering
* Kubernetes troubleshooting
* CI/CD pipeline monitoring

---

# Task 4 - Terminating a Misbehaving Process

## Problem Statement

The process:

* `resource_hog.sh`

was consuming excessive CPU resources and impacting overall server performance.

The objective was to terminate the process safely.

---

# Command Used

```bash id="z3q7hf"
pkill resource_hog.sh
```

---

# Solution

```bash id="k9t5ru"
labex:project/ $ pkill resource_hog.sh
```

---

# Verification Command

```bash id="c6v1xn"
ps aux | grep "resource_hog.sh"
```

---

# Why `pkill` Was Used

Unlike `kill`, which requires a PID, `pkill` allows administrators to:

* terminate processes by name
* simplify operational workflows
* quickly stop problematic workloads

---

# Why This Matters

Process termination is frequently required during:

* production incidents
* runaway scripts
* memory leaks
* infrastructure failures
* high CPU events

This is a core Linux operational skill.

---

# Task 5 - Running Background Processes with `nohup`

## Problem Statement

A developer requested execution of:

* `data_processor.sh`

The script needed to:

* continue running after logout
* execute in the background
* store logs persistently

---

# Commands Used

```bash id="m7x4pl"
nohup
&
2>&1
```

---

# Initial Execution Attempt

```bash id="v0q9ke"
nohup data_processor.sh > processor.log &
```

---

# Error Encountered

```bash id="p2r6dy"
nohup: failed to run command 'data_processor.sh': No such file or directory
```

---

# Why the Error Happened

The script was not executed using:

* relative path notation (`./`)

Linux could not locate the executable file.

---

# Correct Working Solution

```bash id="w5f8oc"
nohup ./data_processor.sh > processor.log 2>&1 &
```

---

# Command Breakdown

| Component     | Purpose                     |
| ------------- | --------------------------- |
| `nohup`       | Prevent hangup after logout |
| `./script.sh` | Execute local script        |
| `>`           | Redirect standard output    |
| `2>&1`        | Redirect standard error     |
| `&`           | Run in background           |

---

# Successful Execution Output

```bash id="b8y3sm"
[1] 1103
```

---

# Log File Verification

```bash id="g4x1vr"
cat processor.log
```

---

# Output Example

```bash id="l6p9tk"
Starting data processing at Tue May 26 13:34:49 CST 2026

Data processing complete at Tue May 26 13:34:54 CST 2026
```

---

# Process Verification

```bash id="d1n5uw"
ps aux | grep data_processor.sh
```

---

# Why This Matters

Background process management is essential in:

* DevOps pipelines
* automation systems
* CI/CD jobs
* batch processing
* infrastructure operations

The `nohup` utility is commonly used for:

* long-running deployments
* migration jobs
* backup scripts
* automation tasks

---

# Key Learnings

Through this lab, I learned how to:

* inspect Linux processes
* monitor live resource utilization
* identify high CPU workloads
* verify critical services
* terminate problematic processes
* execute resilient background jobs
* redirect logs effectively
* troubleshoot process execution issues

---

# DevOps & Infrastructure Relevance

The concepts practiced in this lab are highly relevant to:

* Linux System Administration
* DevOps Engineering
* Site Reliability Engineering (SRE)
* Cloud Infrastructure
* Kubernetes Operations
* CI/CD systems
* Production Monitoring
* Incident Response

---

# Summary

In this lab, I successfully:

* listed active Linux processes
* monitored CPU and memory usage
* identified performance bottlenecks
* verified critical application services
* terminated a resource-intensive process
* executed persistent background jobs
* redirected logs and process outputs correctly

This exercise strengthened my understanding of Linux process lifecycle management and operational troubleshooting used in real-world DevOps and production infrastructure environments.
