---
layout: page
title: TryHackMe Applied Security Journal
---

# TryHackMe Applied Security Journal

Structured applied study of vulnerability mechanics through controlled lab environments.

---

## Current Focus: Web Application Security

I am intentionally working through web application security modules to deepen my understanding of how common vulnerability classes emerge within real systems. The objective is not exploit proficiency. The objective is architectural literacy, detection awareness, and stronger defensive judgment.

This path strengthens my ability to:

- interpret scan results in context
- identify trust boundary failures
- connect findings to observable telemetry
- design remediation-oriented analysis workflows
- improve automation guardrails within GLITCH

---

## Entry 1 — Linux Fundamentals 1

**Date Completed:** 05 April 2026

### Topics Covered

#### Navigation
```bash
pwd
ls
cd
whoami
```

#### System Structure
```bash
/
/home
/etc
/var
/tmp
```

#### Permissions
```bash
r = read
w = write
x = execute
-rwxr-xr--
```

#### Package Management
```bash
sudo apt update
sudo apt install nmap
```

#### Searching and Discovery
```bash
grep "password" file.txt
grep -i "error" logfile.txt
grep -r "api_key" /var/www/
grep -n "login" file.txt

find / -name "config.php"
find /home -name "*.txt"
find / -type f
find / -type d
find / -perm 777
find / -user root
```

#### Shell Operators and Redirection
```bash
command1 && command2
command1 || command2
command1 | command2
command > file.txt
command >> file.txt
command 2> error.log
command &
command > output.txt 2>&1
```

### Important Takeaways

**Why**
- Linux is a primary operating environment for cybersecurity work.
- File awareness matters because logs, configs, and attack paths all live in predictable locations.

**Watch**
- `find / -perm 777` can reveal world-writable files.
- `grep -r "password"` can expose credentials or secrets.
- `/var/log` is a key location for detection and forensics.
- Pipes and conditional operators are building blocks for automation.

**Mini Cheat Sheet**
```bash
find / -perm 777
find / -name "*.txt"
grep -r "password" /
find / -name "*.log" | grep "error"
grep -r "api_key" /var/www/ > results.txt
scan_target && report_results || echo "Scan failed"
```

---

## Entry 2 — Linux Fundamentals 2

**Date Completed:** 05 April 2026

### Topics Covered

#### User and Privilege Management
```bash
su
su root
sudo command
sudo -l
cat /etc/passwd
cat /etc/shadow
sudo adduser username
```

#### Process Management
```bash
ps
ps aux
top
kill <PID>
kill -9 <PID>
```

#### Common Directories
```bash
/           # root
/home       # user home folders
/etc        # configuration files
/var        # logs, cache, spool
/var/log    # system logs
/tmp        # temporary files
/bin        # essential commands
/usr/bin    # user-installed programs
/sbin       # system/admin commands
/opt        # third-party apps
/root       # root home
```

#### Users vs Groups
- Users = individual accounts
- Groups = permission collections
- One user can belong to multiple groups

#### File Permissions
```bash
chmod 755 file.txt
chmod 644 file.txt
chmod +x script.sh
```

```text
777 = rwx rwx rwx
755 = rwx r-x r-x
644 = rw- r-- r--
```

#### SSH
```bash
ssh user@ip
ssh -p 2222 user@ip
ssh -i id_rsa user@ip
exit
```

### Important Takeaways

**Why**
- Directories show where to look.
- Users and groups define who has access.
- Permissions define what they can do.
- Processes show what is happening now.
- SSH is a primary remote access method.

**Watch**
- `/etc/passwd` supports user enumeration.
- `/etc/shadow` contains password hashes.
- `/var/log` supports investigation.
- `/tmp` may be exploitable.
- `sudo -l` can reveal privilege escalation opportunities.
- Weak permissions and exposed SSH keys increase risk.

**Learned**
- Linux is structured and predictable.
- The file system acts as a map of the system.
- Permissions define security boundaries.
- Processes show live behavior.
- SSH extends system control across the network.

---

## Entry 3 — Linux Fundamentals 3

**Date Completed:** April 2026

### Topics Covered

#### File Operations
```bash
cp file.txt backup.txt
mv file.txt newname.txt
rm file.txt
touch file.txt
```

#### File Viewing and Editing
```bash
cat file.txt
nano file.txt
vim file.txt
```

```text
Nano:
CTRL + O   save
CTRL + X   exit

Vim:
i
ESC
:wq
:q!
```

#### Downloading and Transfer
```bash
wget http://example.com/file.txt
wget -O newname.txt http://example.com/file.txt
scp file.txt user@ip:/path/
scp user@ip:/path/file.txt .
scp -r folder user@ip:/path/
```

#### Local Web Serving
```bash
python3 -m http.server
```

#### Process Monitoring and Job Control
```bash
ps
ps aux
jobs
fg
fg %1
```

#### Scheduling and Packages
```bash
crontab -e
crontab -l
* * * * * command

sudo apt update
sudo apt upgrade
sudo apt install nmap
sudo apt remove nmap
```

#### Logs
```bash
cd /var/log
ls
cat syslog
cat auth.log
less syslog
tail syslog
tail -f syslog
```

Important log files:
```bash
/var/log/syslog
/var/log/auth.log
```

### Important Takeaways

**Why**
- File operations control system state.
- Editors change system behavior.
- `wget` and `scp` move data.
- `http.server` quickly exposes files.
- `ps` reveals live activity.
- `cron` introduces persistence and automation.
- `apt` manages software lifecycle.
- logs provide visibility.

**Watch**
- `rm` is destructive.
- editing config files has system-wide impact.
- cron can be used for persistence.
- package management introduces trust and supply-chain considerations.
- `/var/log/auth.log` is valuable for authentication review.

---

## Entry 4 — Intro to Logs

**Date Completed:** 06 April 2026

### What Logs Do

Logs answer key investigative questions:
- what happened
- when it happened
- where it happened
- who did it
- whether it was successful

### Scenario

A web server is being scanned by an attacker. Logs are used to identify the attacker, understand their actions, and determine whether their activity was successful.

Relevant log file:
```bash
/var/log/gitlab/nginx/access.log
```

### Log Types
- system logs
- authentication logs
- application logs
- security logs
- network logs

### Log Formats
- plain text
- structured
- syslog
- combined

### Log Collection and Management
- logs come from systems, applications, and network devices
- management includes storage, rotation, and access control
- centralisation improves visibility and correlation
- `rsyslog` supports collection and forwarding
- manual collection can be done with `scp` or `rsync`

### Storage, Retention, and Deletion
- logs must be stored securely
- retained for a defined period
- deleted according to policy and legal requirements
- `logrotate` supports lifecycle management

### Log Analysis Process
- parsing
- normalisation
- sorting
- classification
- enrichment
- correlation
- visualisation
- reporting

### Log Analysis Tools

#### SIEM
- Splunk
- Elastic Stack

#### Linux Tools
```bash
cat
grep
sed
sort
uniq
awk
sha256sum
```

### Log Analysis Techniques
- pattern recognition
- anomaly detection
- correlation analysis
- timeline analysis

### Practical Log Analysis

**Raw logs** are viewed directly for rapid inspection and evidence preservation.

**Parsed logs** are filtered and standardized using:
```bash
cat
grep
sed
sort
uniq
awk
```

### Important Takeaways

**Why**
- logs help detect and investigate activity.

**Watch**
- repeated patterns can signal scanning or attack activity.
- missing or altered logs may indicate tampering.

**Learned**
- logs become more useful when combined, normalized, and interpreted together.

---

## Lab Entry Template

### Lab Name
### Completion Date
### Vulnerability Class

#### Root Cause Analysis
What design flaw or configuration weakness enabled this issue?

#### Trust Boundary Failure
Where did the system incorrectly assume safety or validation?

#### Detection Signals
What logs, telemetry, or monitoring data would expose this issue in production?

#### Preventative Controls
What configuration, validation, or architectural change would prevent this issue?

#### Governance Considerations
How could automation misclassify or mishandle this issue without human judgment?
