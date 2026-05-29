# Day 05 - Linux User Management, Access Control & System Security

---

# Introduction

On the final day at LabEx Corporation, the responsibility shifted from infrastructure troubleshooting to one of the most security-critical areas of Linux Administration:

* user management
* account provisioning
* access control
* authentication management
* system security

Project Phoenix had entered its final development phase, and strict control over system access became essential.

The CTO assigned two critical operational tasks:

* onboard a new senior developer responsible for leading the final deployment phase
* immediately revoke access for a former contractor identified during previous security investigations

This lab simulated real-world Linux Administration workflows involving:

* user onboarding
* account security
* group management
* password administration
* account locking
* access governance

---

# Objective

The primary objectives of this lab were to:

* Create Linux user accounts
* Configure secure home directories
* Assign passwords securely
* Manage Linux group memberships
* Implement role-based access control
* Lock unauthorized user accounts
* Strengthen Linux system security

---

# Skills Covered

* Linux user administration
* User provisioning
* Group management
* Access control
* Password configuration
* Account locking
* Security operations
* Linux authentication management

---

# Linux Commands Used

```bash id="q4p9tw"
useradd
userdel
usermod
passwd
groups
id
grep
ls
sudo
```

---

# Task 1 - Onboarding a New Developer

## Problem Statement

A new senior developer named:

* Brenda Smith

needed access to Project Phoenix infrastructure.

According to organizational policy, usernames followed the format:

* `first_initial.last_name`

The objective was to create a Linux user account:

* `b.smith`

---

# Commands Used

```bash id="o5x2zc"
useradd
grep
id
```

---

# Solution

```bash id="g1q7rf"
labex:project/ $ sudo useradd b.smith

labex:project/ $ grep "b.smith" /etc/passwd

b.smith:x:5002:5004::/home/b.smith:/bin/sh

labex:project/ $ id b.smith

uid=5002(b.smith) gid=5004(b.smith) groups=5004(b.smith)
```

---

# Output Explanation

| Field           | Meaning                |
| --------------- | ---------------------- |
| `uid`           | User ID                |
| `gid`           | Primary Group ID       |
| `/home/b.smith` | Default home directory |
| `/bin/sh`       | Default login shell    |

The account was successfully added to the Linux system.

---

# Why This Matters

User provisioning is one of the most important Linux Administration responsibilities.

This process is critical in:

* DevOps teams
* cloud environments
* enterprise infrastructure
* CI/CD systems
* production operations

---

# Task 2 - Creating a Secure Home Directory

## Problem Statement

The user account existed, but no home directory had been created.

A Linux home directory provides:

* personal workspace
* configuration storage
* user-specific environment settings
* operational isolation

The objective was to recreate the user properly with:

* automatic home directory creation

---

# Commands Used

```bash id="l8y0wd"
userdel
useradd -m
ls -la
```

---

# Solution

```bash id="u6m3xv"
labex:project/ $ sudo userdel b.smith

labex:project/ $ sudo useradd -m b.smith
```

---

# Home Directory Verification

```bash id="k2r9cp"
labex:project/ $ ls -la /home/

drwxr-x--- 2 b.smith b.smith 57 May 25 13:11 b.smith
```

---

# Detailed Home Directory Inspection

```bash id="w4z8fs"
labex:project/ $ sudo ls -la /home/b.smith
```

---

# Generated Default Files

| File           | Purpose                |
| -------------- | ---------------------- |
| `.bashrc`      | Shell configuration    |
| `.profile`     | User environment setup |
| `.bash_logout` | Logout session script  |

---

# Why This Matters

Proper home directory configuration is essential for:

* Linux user isolation
* secure environments
* developer workspaces
* automation tools
* cloud systems

This is standard operational practice in Linux Administration.

---

# Task 3 - Assigning an Initial Password

## Problem Statement

The account was created but remained inaccessible because no password had been configured.

The objective was to:

* assign a secure password
* activate the user account

---

# Commands Used

```bash id="v1x4oa"
passwd
grep
sudo
```

---

# Initial Password Error

```bash id="f3n9zy"
sudo passwd b.smith
```

---

# Error Received

```bash id="x8m1ke"
Sorry, passwords do not match.

passwd: Authentication token manipulation error

passwd: password unchanged
```

---

# Why the Error Happened

The password confirmation did not match the original password.

This reinforced:

* authentication handling
* secure credential validation
* Linux password management workflows

---

# Final Working Solution

```bash id="p5r2mn"
sudo passwd b.smith
```

---

# Password Successfully Updated

```bash id="c7v0qs"
passwd: password updated successfully
```

---

# Password Hash Verification

```bash id="a2z8uw"
sudo grep "^b.smith:" /etc/shadow
```

---

# Output Example

```bash id="t4l7xy"
b.smith:$y$j9T$hZzdz1qF0VqDOBCD13Rbe/$80zeTR.GaFMvujNWMz5FTHa2uGJm/3Ga/0vHSmKUad7:20598:0:99999:7:::
```

---

# Security Importance

The `/etc/shadow` file securely stores:

* encrypted password hashes
* password aging policies
* authentication settings

This is a critical Linux security component.

---

# Task 4 - Adding the User to the Developers Group

## Problem Statement

To allow Brenda access to Project Phoenix resources, the user needed membership in the:

* `developers`

group.

The objective was to:

* append the user to the developers group
* preserve existing memberships

---

# Commands Used

```bash id="h7w3np"
usermod
groups
id
grep
```

---

# Initial Syntax Errors

```bash id="y9r4mv"
usermod -a -G=developers b.smith
```

---

# Error

```bash id="n5c1kt"
group '=developers' does not exist
```

---

# Additional Syntax Error

```bash id="j8u6pl"
usermod -a -G:developers b.smith
```

---

# Why the Errors Happened

The `-G` option syntax was incorrect.

Correct syntax:

```bash id="q1v5ez"
usermod -a -G developers username
```

---

# Permission Error Encountered

```bash id="r3k8fs"
usermod: Permission denied
```

---

# Why the Error Happened

Administrative privileges were required.

This reinforced:

* Linux privilege management
* secure administrative controls

---

# Final Working Solution

```bash id="b6m0xr"
sudo usermod -a -G developers b.smith
```

---

# Group Membership Verification

```bash id="w9q2cu"
groups b.smith

b.smith : b.smith developers
```

---

# Detailed User Information

```bash id="e2x7op"
id b.smith

uid=5002(b.smith) gid=5004(b.smith) groups=5004(b.smith),5003(developers)
```

---

# Group Database Verification

```bash id="s1l8zt"
grep "^developers:" /etc/group

developers:x:5003:b.smith
```

---

# Why This Matters

Linux groups enable:

* role-based access control
* collaborative permissions
* secure resource sharing
* operational segmentation

This is heavily used in:

* DevOps environments
* Kubernetes clusters
* CI/CD infrastructure
* cloud-native systems

---

# Task 5 - Locking a Departing Employee Account

## Problem Statement

A former contractor:

* `j.doe`

had been identified during earlier security investigations as having unauthorized access.

The objective was to:

* immediately disable login access
* preserve audit data
* retain user files for compliance purposes

---

# Commands Used

```bash id="m8y4qv"
usermod -L
grep
sudo
```

---

# Final Working Solution

```bash id="k5n1ws"
sudo usermod -L j.doe
```

---

# Account Lock Verification

```bash id="f7x2ap"
sudo grep "^j.doe:" /etc/shadow
```

---

# Verification Output

```bash id="r0z6yc"
j.doe:!:20598:0:99999:7:::
```

---

# Output Explanation

The `!` symbol indicates:

* the account is locked
* login authentication is disabled
* password access is blocked

The account still exists for:

* compliance auditing
* forensic investigations
* file retention
* legal requirements

---

# Security Importance

Account locking is commonly used for:

* employee offboarding
* incident response
* access revocation
* compliance operations
* security investigations

---

# Key Learnings

Through this lab, I learned:

* Linux user provisioning
* Home directory management
* Password administration
* Role-based access control
* Linux group management
* Account security operations
* Authentication workflows
* Secure user lifecycle management

---

# DevOps & Infrastructure Relevance

The skills practiced in this lab are highly relevant to:

* DevOps Engineering
* Linux Administration
* Cloud Infrastructure
* Kubernetes RBAC
* IAM operations
* CI/CD security
* Infrastructure governance
* Production security management

---

# Summary

In this lab, I successfully:

* created Linux user accounts
* configured secure home directories
* assigned user passwords
* managed Linux group memberships
* implemented access control
* locked unauthorized accounts
* strengthened Linux system security

This exercise reinforced critical Linux Administration and DevOps security concepts related to authentication, authorization, and secure infrastructure management.
