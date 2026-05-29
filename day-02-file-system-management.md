# Day 02 - Linux File System Management & Project Organization

---

# Introduction

Welcome to Day 02 at LabEx Corporation.

After successfully completing system reconnaissance and environmental assessment on Day 01, the development leadership team has assigned a new responsibility for **Project Phoenix**.

The previous administrator left the development environment in complete disorder:

* project files were scattered
* configuration files lacked backups
* documentation was unorganized
* outdated logs were consuming unnecessary storage
* directory structures were poorly designed

As the newly assigned **Digital Architect**, the mission was to transform this chaotic Linux workspace into a clean, organized, and production-ready project environment.

This lab focused on:

* directory management
* file organization
* backup creation
* archive management
* Linux file system operations
* workspace restructuring

These tasks closely simulate real-world Linux Administration and DevOps operational workflows.

---

# Objective

The primary objectives of this lab were to:

* Build a structured Linux project environment
* Organize application files logically
* Secure critical configuration backups
* Manage shared project resources
* Archive outdated log data
* Improve operational maintainability

---

# Skills Covered

* Linux directory management
* File organization
* File movement operations
* Backup creation
* Archive compression
* Linux cleanup workflows
* Storage optimization
* Output verification

---

# Linux Commands Used

```bash id="u3pj8r"
mkdir
mv
cp
ls
pwd
cd
tar
rm
```

---

# Task 1 - Setting Up the Project Directory Structure

## Problem Statement

The Project Phoenix workspace lacked a proper directory hierarchy.

To improve maintainability and operational efficiency, separate directories needed to be created for:

* source code
* configuration files
* documentation

A clean directory structure is essential for:

* DevOps workflows
* CI/CD pipelines
* collaborative development
* infrastructure organization

---

# Commands Used

```bash id="0zn2vm"
mkdir
pwd
ls -F
```

---

# Solution

```bash id="7v4htq"
labex:project/ $ cd ~/project/phoenix_project

labex:phoenix_project/ $ pwd
/home/labex/project/phoenix_project

labex:phoenix_project/ $ mkdir src config docs

labex:phoenix_project/ $ ls
README.md  config  config.json  docs  main_app.py  src

labex:phoenix_project/ $ ls -F ~/project/phoenix_project
README.md  config/  config.json  docs/  main_app.py  src/
```

---

# Output Explanation

| Directory | Purpose                        |
| --------- | ------------------------------ |
| `src/`    | Stores application source code |
| `config/` | Stores configuration files     |
| `docs/`   | Stores project documentation   |

The `/` symbol in `ls -F` output indicates directories.

---

# Why This Matters

Well-structured Linux project environments:

* improve navigation
* simplify troubleshooting
* enhance maintainability
* support automation workflows
* improve team collaboration

This structure closely resembles real-world DevOps and software engineering environments.

---

# Task 2 - Organizing Project Files

## Problem Statement

The root project directory contained scattered files:

* application code
* documentation
* configuration files

The objective was to relocate each file into its appropriate directory.

---

# Commands Used

```bash id="7mavxq"
mv
ls -F
```

---

# Solution

```bash id="3mjlwm"
labex:phoenix_project/ $ mv main_app.py src

labex:phoenix_project/ $ mv config.json config

labex:phoenix_project/ $ mv README.md docs

labex:phoenix_project/ $ ls -F ~/project/phoenix_project
config/  docs/  src/
```

---

# Final Project Structure

```bash id="h5xltv"
~/project/phoenix_project/

├── config/
│   └── config.json

├── docs/
│   └── README.md

└── src/
    └── main_app.py
```

---

# Output Explanation

| File          | Destination |
| ------------- | ----------- |
| `main_app.py` | `src/`      |
| `config.json` | `config/`   |
| `README.md`   | `docs/`     |

This created a cleaner and more maintainable project environment.

---

# DevOps Relevance

File organization is critical in:

* CI/CD pipelines
* containerized applications
* Kubernetes deployments
* infrastructure-as-code repositories
* configuration management systems

Organized directory structures improve:

* automation reliability
* deployment consistency
* operational efficiency

---

# Task 3 - Backing Up Critical Configuration Files

## Problem Statement

Configuration files are highly sensitive operational assets.

Before any modification or deployment activity, administrators should create backup copies to prevent:

* accidental loss
* corruption
* misconfiguration
* deployment failures

The goal was to create a secure backup of:

* `config.json`

---

# Commands Used

```bash id="l3n9to"
cp
ls
cat
```

---

# Solution

```bash id="k4s7wp"
labex:config/ $ cp config.json config.json.bak

labex:config/ $ ls
config.json  config.json.bak
```

---

# Backup Verification

```bash id="z0odsv"
labex:config/ $ cat config.json

labex:config/ $ cat config.json.bak
```

---

# Output Explanation

| File              | Purpose                |
| ----------------- | ---------------------- |
| `config.json`     | Original configuration |
| `config.json.bak` | Backup copy            |

The `.bak` extension is commonly used in Linux environments to indicate backup files.

---

# Why Backups Matter

Configuration backups are critical for:

* rollback operations
* disaster recovery
* deployment validation
* infrastructure troubleshooting
* operational reliability

This is a standard Linux Administration best practice.

---

# Task 4 - Reorganizing Shared Team Resources

## Problem Statement

The development team maintained a separate shared documentation directory outside the main project structure.

The objective was to integrate:

* team guidelines
* API specifications
* shared documentation

into the primary project documentation directory.

---

# Commands Used

```bash id="1gaxoq"
mv
ls
```

---

# Solution

```bash id="0xyh9u"
labex:project/ $ mv ~/project/shared_docs ~/project/phoenix_project/docs/

labex:docs/ $ ls
README.md  shared_docs

labex:docs/ $ ls ~/project/phoenix_project/docs/shared_docs/

api_spec.doc  team_guidelines.txt
```

---

# Final Documentation Structure

```bash id="s0oz5d"
~/project/phoenix_project/docs/

├── README.md

└── shared_docs/
    ├── api_spec.doc
    └── team_guidelines.txt
```

---

# Operational Benefits

Centralized documentation:

* improves collaboration
* simplifies onboarding
* supports DevOps workflows
* reduces operational confusion
* enhances project maintainability

---

# Task 5 - Archiving & Cleaning Old Log Files

## Problem Statement

The server contained outdated 2023 log files consuming storage space.

The objective was to:

* archive old logs
* compress them
* remove obsolete files
* preserve recent operational logs

This simulates real-world Linux maintenance and storage optimization workflows.

---

# Understanding the tar Command

The `tar` utility is widely used in Linux systems for:

* file archiving
* backup management
* log compression
* deployment packaging

---

# Important tar Options

| Option | Purpose             |
| ------ | ------------------- |
| `c`    | Create archive      |
| `z`    | Compress using gzip |
| `f`    | Specify filename    |

---

# Commands Used

```bash id="s0dq3k"
tar
rm
ls
```

---

# Initial Failed Attempt

```bash id="k11jpx"
tar -czf old_logs.tar.gz
```

### Error

```bash id="w29yyv"
tar: Cowardly refusing to create an empty archive
```

---

# Why the Error Happened

The `tar` command requires:

* archive name
* files to archive

No files were provided initially.

This troubleshooting step helped reinforce proper Linux command syntax understanding.

---

# Final Working Solution

```bash id="nwv5sl"
labex:logs/ $ tar -czf old_logs.tar.gz app_2023-01-15.log db_2023-02-20.log

labex:logs/ $ rm app_2023-01-15.log db_2023-02-20.log

labex:logs/ $ ls

app_2024-05-01.log  old_logs.tar.gz
```

---

# Final Logs Directory Structure

```bash id="7p56he"
~/project/logs/

├── app_2024-05-01.log
└── old_logs.tar.gz
```

---

# Output Explanation

| File                 | Purpose                         |
| -------------------- | ------------------------------- |
| `old_logs.tar.gz`    | Compressed archive of old logs  |
| `app_2024-05-01.log` | Active operational log retained |

---

# Operational Importance

Log archival is essential for:

* storage management
* operational cleanup
* compliance retention
* troubleshooting history
* production server maintenance

These practices are widely used in:

* Linux servers
* cloud environments
* Kubernetes nodes
* DevOps infrastructure

---

# Key Learnings

Through this lab, I learned:

* Linux directory structuring
* File movement operations
* Backup creation strategies
* Archive compression workflows
* Storage cleanup procedures
* Linux project organization
* Real-world operational maintenance
* Troubleshooting Linux command errors

---

# DevOps & Infrastructure Relevance

The skills practiced in this lab are highly relevant to:

* DevOps Engineering
* Infrastructure Management
* Cloud Operations
* CI/CD Pipelines
* Configuration Management
* Kubernetes environments
* Linux server administration

File system organization and backup management are foundational operational skills required in production environments.

---

# Summary

In this lab, I successfully:

* created a structured Linux project hierarchy
* organized scattered application resources
* secured configuration backups
* centralized shared documentation
* archived outdated logs
* optimized storage usage
* improved operational maintainability

This exercise strengthened my Linux file system management skills while reinforcing operational best practices commonly used in DevOps and Infrastructure Engineering environments.
