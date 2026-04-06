---
layout: page
title: Vulnerable System Analysis
---

# 🧪 Vulnerable System Analysis

Technical assessments of authorized lab targets conducted in isolated environments. :contentReference[oaicite:0]{index=0}  

---

## 📊 Assessment Report — Metasploitable 2

**Target System:** Metasploitable 2 (Linux)  
**Date:** February 2026  
**Scope:** Internal Lab Network – 192.168.56.0/24  

---

### 🧠 Executive Summary

The assessed system intentionally contains multiple high-risk vulnerabilities designed for security training. The overall security posture is critically weak due to exposed services, outdated software versions, and weak authentication controls.

Several services allow unauthorized access or facilitate privilege escalation if left unpatched in a production environment.

**Immediate remediation priorities:**
- Service hardening  
- Credential governance  
- Removal of legacy software  

---

## 🔍 Findings

---

### 1. Exposed FTP Service with Anonymous Access  
**Severity:** High  

**Description**  
The FTP service permits anonymous authentication, allowing unauthenticated users to list directories and access files.

**Business Impact**
- Data leakage  
- Credential exposure  
- Reconnaissance vector expansion  

**Remediation**
- Disable anonymous FTP access  
- Restrict via firewall rules  
- Replace with SFTP  
- Enable authentication logging  

---

### 2. Outdated Web Application Components  
**Severity:** Medium–High  

**Description**  
Outdated software exposes the system to known vulnerabilities.

**Business Impact**
- Remote code execution  
- Data exfiltration  
- Lateral movement  

**Remediation**
- Apply vendor patches  
- Remove deprecated components  
- Implement patch management  
- Deploy WAF protections  

---

### 3. Weak Credential Practices  
**Severity:** High  

**Description**  
Default or weak credentials are in use.

**Business Impact**
- Unauthorized access  
- Privilege escalation  
- Full system compromise  

**Remediation**
- Enforce strong password policies  
- Remove default credentials  
- Implement MFA  
- Conduct audits  

---

## ⚠️ Overall Risk Assessment

The system demonstrates systemic security weaknesses typical of unmaintained environments. Risk is elevated due to overlapping vulnerabilities and lack of segmentation.

**Critical controls required:**
- Service minimization  
- Patch management  
- Credential governance  
- Network segmentation  

---

# 🧪 Assessment Report — OWASP Juice Shop

---

## 🧠 Overview

This report documents the analysis of a deliberately vulnerable web application, OWASP Juice Shop, conducted in a controlled lab environment.

The focus is on identifying vulnerability patterns, understanding root causes, and mapping them to detection and mitigation strategies.

---

## 🎯 Objective

- Identify vulnerability classes  
- Analyze insecure design decisions  
- Map vulnerabilities to log signals  
- Develop defensive understanding  

---

## 🛠️ Environment

- Local deployment via Docker  
- Target: Juice Shop  
- Tools:
  - Browser DevTools  
  - Burp Suite  
  - Linux CLI  
  - Log inspection  

---

## 🔍 Vulnerability Analysis

---

### 1. Broken Authentication  
**Root Cause:**  
Improper server-side validation  

**Trust Boundary Failure:**  
Client input trusted without verification  

**Detection Signals**
- Repeated failed logins  
- Abnormal login success patterns  

**Controls**
- Server-side validation  
- Rate limiting  
- Account lockout  

---

### 2. SQL Injection  
**Root Cause:**  
Unsanitized input  

**Trust Boundary Failure:**  
Assumed safe input  

**Detection Signals**
- Query anomalies  
- Error messages  
- Injection patterns (`' OR 1=1`)  

**Controls**
- Parameterized queries  
- Input validation  
- ORM usage  

---

### 3. Sensitive Data Exposure  
**Root Cause:**  
Improper data handling  

**Trust Boundary Failure:**  
Excessive data exposure  

**Detection Signals**
- Sensitive data in logs/responses  
- Unencrypted traffic  

**Controls**
- Encryption  
- Access controls  
- Data minimization  

---

### 4. IDOR  
**Root Cause:**  
Missing authorization checks  

**Trust Boundary Failure:**  
User-controlled identifiers trusted  

**Detection Signals**
- Sequential ID access  
- Unauthorized resource access  

**Controls**
- Authorization enforcement  
- Indirect references  
- Permission validation  

---

## 📡 Log-Based Detection Strategy

### Key Log Sources
/var/log/nginx/access.log
/var/log/nginx/error.log
application logs

### Indicators
High request frequency
Repeated 4xx/5xx responses
Suspicious query strings
Unusual User-Agents
Authentication anomalies

### 🧠 Analysis Approach
Observe system behavior
Identify deviations
Map activity to logs
Correlate events

### 🔑 Key Findings
Vulnerabilities stem from broken trust boundaries
Input validation failures are a primary cause
Logs provide strong detection signals
Effective detection requires correlation

### 🛡️ Defensive Insight
Understanding exploitation improves:
detection capability
logging strategy design
preventative controls
architectural security

### 🏛️ Governance Considerations
Automation requires human validation
Logs must be:
complete
accurate
tamper-resistant

### 📌 Conclusion
The Juice Shop lab demonstrates how design and validation failures lead to exploitable conditions. By linking vulnerabilities to observable signals, this analysis strengthens defensive capabilities and detection strategy development.

All testing conducted in an isolated, authorized lab environment.
