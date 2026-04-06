---
layout: page
title: TryHackMe Applied Security Journal
---

# TryHackMe Applied Security Journal

Structured applied study of vulnerability mechanics through controlled lab environments.

---
Entry 1
Room Name: Linux Fundamentals 1
Date Completed: 05 April 2026
Notes During the Room:
# Navigation
pwd       # Where am I?
ls        # What’s here?
cd        # Move around
whoami    # Who am I?
# System Structure
/         # Root
/home     # Users
/etc      # Configs
/var      # Logs
/tmp      # Temp
# Permissions
r = read
w = write
x = execute
# Example
-rwxr-xr--
# Package Management (Debian-based)
sudo apt update
sudo apt install nmap
# grep = search inside files
grep "password" file.txt
grep -i "error" logfile.txt
grep -r "api_key" /var/www/
grep -n "login" file.txt
# find = search for files in system
find / -name "config.php"
find /home -name "*.txt"
find / -type f
find / -type d
find / -perm 777
find / -user root
# AND operator (run next if success)
command1 && command2
# OR operator (run next if fail)
command1 || command2
# Pipe (send output to another command)
command1 | command2

# Redirect output to file (overwrite)
command > file.txt
# Append output to file
command >> file.txt
# Redirect errors
command 2> error.log
# Run in background
command &
# Combine stdout + stderr
command > output.txt 2>&1

Important Takeaways:
WHY (Operational Relevance)
Linux is the native battlefield for cybersecurity
File awareness = locating logs, configs, attack paths
WATCH (Things That Matter Later)
find / -perm 777 → world-writable = 🚨 vuln potential
grep -r "password" → credential discovery
/var/log → detection + forensics goldmine
| (pipe) → core of automation chains
&& / || → decision logic in scripts
Mini cheat Sheet:
# Find writable files (potential vuln)
find / -perm 777
# Find files by name
find / -name "*.txt"
# Search for sensitive data
grep -r "password" /
# Combine tools (🔥 real power)
find / -name "*.log" | grep "error"
# Save output
grep -r "api_key" /var/www/ > results.txt
# Conditional execution
scan_target && report_results || echo "Scan failed"


Entry 2
Room Name: Linux Fundamentals 2
Date Completed: 5, April 2026
Notes During the Room:
# Switching users
su
su root
# Run as root
sudo command

# Check sudo permissions
sudo -l
# View users
cat /etc/passwd
# View password hashes (privileged)
cat /etc/shadow
# Add user
sudo adduser username
# Process management
ps
ps aux
top
# Kill process
kill <PID>
kill -9 <PID>

COMMON DIRECTORIES (System Awareness)
# Root
/           # top of the filesystem
# User directories
/home       # user home folders
# System configs
/etc        # configuration files
# Logs & variable data
/var        # logs, cache, spool
/var/log    # logs (very important)
/tmp        # temporary files
# Binaries (programs)
/bin        # essential commands
/usr/bin    # user-installed programs
# Admin binaries
/sbin       # system/admin commands
# Optional software
/opt        # third-party apps
# Root user home
/root       # root's personal directory

/etc = how system is configured
/var/log = what has happened
/home = user activity
/tmp = temporary / sometimes exploitable

USERS vs GROUPS
Users = individual accounts (identity)
Groups = collections of users (permissions)
One user → multiple groups
user: glenn
groups: sudo, developers

FILE PERMISSIONS (Symbolic + Numeric)
Symbolic
r = read
w = write
x = execute

-rwxr-xr--

Numeric Format
r = 4
w = 2
x = 1
Permission
Value
rwx
7
rw-
6
r-x
5
r--
4


Usage
chmod 755 file.txt
chmod 644 file.txt
chmod +x script.sh

Common Configs
777 = rwx rwx rwx   # dangerous
755 = rwx r-x r-x   # scripts
644 = rw- r-- r--   # files

🔍 SSH (Secure Shell)
ssh user@ip
ssh -p 2222 user@ip
ssh -i id_rsa user@ip
exit
Protocol: TCP
Port: 22
Purpose: Secure remote access

🧠 PROCESS & SYSTEM AWARENESS
ps aux
top
kill -9 <PID>
Process = running program
PID = identifier
Used for monitoring + control 




Important Takeaways:
WHY (Operational Relevance)
Directories = where to look
Users + groups = who has access
Permissions = what they can do
Processes = what is happening
SSH = how you access systems
 WATCH (Things That Matter Later)
/etc/passwd → user enumeration
/etc/shadow → password hashes
/var/log → logs + forensic goldmine
/tmp → potential exploit location
sudo -l → privilege escalation
777 permissions → misconfig risk
SSH keys → HIGH VALUE
LEARNED (Skill Acquisition)
Linux is structured and predictable
File system = map of the system
Permissions = security boundaries
Processes = live behavior
SSH = remote control layer



Entry 3
Room Name: Linux Fundamentals 3
Date Completed: 
Notes During the Room:
File Operations
cp file.txt backup.txt
mv file.txt newname.txt
rm file.txt
touch file.txt
Note: rm is permanent (no recycle bin)

File Viewing & Editing
cat file.txt
nano file.txt
vim file.txt
Nano
CTRL + O   # save
CTRL + X   # exit
Vim
i
ESC
:wq
:q!

Downloading Files — wget
wget http://example.com/file.txt
wget -O newname.txt http://example.com/file.txt

Secure Transfer — scp
scp file.txt user@ip:/path/
scp user@ip:/path/file.txt .
scp -r folder user@ip:/path/

Python HTTP Server
python3 -m http.server

Process Monitoring — ps
ps
ps aux

Job Control
jobs
fg
fg %1

Task Scheduling — cron
crontab -e
crontab -l
* * * * * command

Package Management — apt
sudo apt update
sudo apt upgrade
sudo apt install nmap
sudo apt remove nmap

Logs (System Monitoring & Forensics)
cd /var/log        # navigate to logs
ls                 # list log files

cat syslog         # view system logs
cat auth.log       # authentication logs

less syslog        # scroll through logs
tail syslog        # last lines
tail -f syslog     # live log monitoring
Important Log Files
/var/log/syslog      # general system activity
/var/log/auth.log    # login/authentication attempts
Logs show:
logins
errors
system events
suspicious activity 





Important Takeaways:





Entry 4
Room Name: Intro to Logs
Date Completed: 6, April 2026
Notes During the Room:
What Are Logs?
Logs are records of events that occur on a system. They help answer:
what happened
when it happened
where it happened
who did it
whether it was successful

Scenario
A web server is being scanned by an attacker. Logs are used to:
identify the attacker
determine what they are doing
check if they were successful
Log file used:
/var/log/gitlab/nginx/access.log

Log Types
System logs → system activity
Authentication logs → logins and sudo
Application logs → web/app activity
Security logs → security events
Network logs → connections and traffic

Log Formats
Plain text → human readable
Structured → machine readable
Syslog → standard Linux format
Combined → used in web server logs

Log Collection
Logs come from:
systems
applications
network devices

Log Management
Includes:
storage
rotation
access control
logrotate

Log Centralisation
Logs from multiple systems are stored in one place for easier analysis.

Log Forwarding
rsyslog is used to collect and forward logs.
Manual collection:
scp /var/log/syslog user@server:/logs/

Storage, Retention, Deletion
logs must be stored securely
kept for a set time
deleted when no longer needed

Log Analysis Process
Parsing → break logs apart
Normalisation → standardize logs
Sorting → organize logs
Classification → group logs
Enrichment → add context
Correlation → link events
Visualisation → display data
Reporting → summarize results

Log Analysis Tools
SIEM tools (Splunk, ELK)
Linux tools:
cat grep sed sort uniq awk sha256sum

Log Analysis Techniques
pattern recognition
anomaly detection
correlation
timeline analysis

Practical Log Analysis
Raw Logs
View logs directly without changes.
Parsed Logs
Use tools to filter and organize logs:
cat grep sed sort uniq awk

Important Takeaways:
WHY
Logs help detect and investigate activity.
WATCH
repeated activity = possible attack
missing logs = possible tampering
LEARNED
Logs are useful when combined and analyzed together.

Key Takeaway
Logs are used to monitor systems and investigate security events.









## Current Focus: Web Application Security & Pentesting Path

I am intentionally working through Web Application Security modules to deepen my understanding of how common vulnerability classes emerge within real systems.

The purpose is not exploitation proficiency, but architectural literacy.

Web application vulnerabilities often stem from:

- Broken trust boundaries
- Insufficient input validation
- Improper authentication or session controls
- Business logic design flaws
- Logging and monitoring gaps

Studying these mechanisms strengthens my ability to:

- Interpret scan results within context
- Design detection logic around observable telemetry
- Understand how vulnerabilities propagate operational risk
- Improve automation guardrails within structured analysis frameworks (e.g., GLITCH)

Each lab is documented through a defensive lens — focusing on root cause, detection signals, remediation strategy, and governance implications rather than exploit mechanics.

---

## Lab Entry Template

### Lab Name:
### Completion Date:
### Vulnerability Class:

---

### Root Cause Analysis
What design flaw or configuration weakness enabled this vulnerability?

---

### Trust Boundary Failure
Where did the system incorrectly assume safety or validation?

---

### Detection Signals
What logs, telemetry, or monitoring data would expose this issue in production?

---

### Preventative Controls
What configuration, validation, or architectural change would prevent this vulnerability?

---

### Governance Considerations
How could automation misclassify or mishandle this issue without human judgment?
