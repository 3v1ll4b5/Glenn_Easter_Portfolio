---
layout: page
title: Vulnerable System Analysis
---

# Vulnerable System Analysis

Technical assessments of authorized lab targets conducted in isolated environments.

---

## Assessment Report — Metasploitable 2

**Target System:** Metasploitable 2 (Linux)  
**Date:** February 2026  
**Scope:** Internal Lab Network – 192.168.56.0/24  

### Executive Summary

The assessed system intentionally contains multiple high-risk vulnerabilities designed for security training. The overall security posture is critically weak due to exposed services, outdated software versions, and weak authentication controls.

Several services allow unauthorized access or facilitate privilege escalation if left unpatched in a production environment.

**Immediate remediation priorities:**
- service hardening
- credential governance
- removal of legacy software

---

## Findings

### 1. Exposed FTP Service with Anonymous Access
**Severity:** High

**Description**  
The FTP service permits anonymous authentication, allowing unauthenticated users to list directories and access files.

**Business Impact**
- data leakage
- credential exposure
- reconnaissance vector expansion

**Remediation**
- disable anonymous FTP access
- restrict via firewall rules
- replace with SFTP
- enable authentication logging

### 2. Outdated Web Application Components
**Severity:** Medium–High

**Description**  
Outdated software exposes the system to known vulnerabilities.

**Business Impact**
- remote code execution
- data exfiltration
- lateral movement

**Remediation**
- apply vendor patches
- remove deprecated components
- implement patch management
- deploy WAF protections

### 3. Weak Credential Practices
**Severity:** High

**Description**  
Default or weak credentials are in use.

**Business Impact**
- unauthorized access
- privilege escalation
- full system compromise

**Remediation**
- enforce strong password policies
- remove default credentials
- implement MFA
- conduct audits

### Overall Risk Assessment

The system demonstrates systemic security weaknesses typical of unmaintained environments. Risk is elevated due to overlapping vulnerabilities and lack of segmentation.

**Critical controls required:**
- service minimization
- patch management
- credential governance
- network segmentation

---

## Assessment Report — OWASP Juice Shop

### Overview

This report documents the analysis of a deliberately vulnerable web application, OWASP Juice Shop, conducted in a controlled lab environment.

The focus is on identifying vulnerability patterns, understanding root causes, and mapping them to detection and mitigation strategies.

### Objective
- identify vulnerability classes
- analyze insecure design decisions
- map vulnerabilities to log signals
- develop defensive understanding

### Environment
- local deployment via Docker
- target: Juice Shop
- tools:
  - browser developer tools
  - Burp Suite
  - Linux CLI
  - log inspection

### Vulnerability Analysis

#### 1. Broken Authentication
**Root Cause:** Improper server-side validation  
**Trust Boundary Failure:** Client input trusted without verification

**Detection Signals**
- repeated failed login attempts
- abnormal login success patterns

**Controls**
- server-side validation
- rate limiting
- account lockout

#### 2. SQL Injection
**Root Cause:** Unsanitized input  
**Trust Boundary Failure:** Assumed safe input

**Detection Signals**
- query anomalies
- error messages
- injection patterns (`' OR 1=1`)

**Controls**
- parameterized queries
- input validation
- ORM usage

#### 3. Sensitive Data Exposure
**Root Cause:** Improper data handling  
**Trust Boundary Failure:** Excessive data exposure

**Detection Signals**
- sensitive data in logs or responses
- unencrypted traffic

**Controls**
- encryption
- access controls
- data minimization

#### 4. Insecure Direct Object Reference (IDOR)
**Root Cause:** Missing authorization checks  
**Trust Boundary Failure:** User-controlled identifiers trusted

**Detection Signals**
- sequential ID access
- unauthorized resource access

**Controls**
- authorization enforcement
- indirect references
- permission validation

### Log-Based Detection Strategy

**Key Log Sources**
```bash
/var/log/nginx/access.log
/var/log/nginx/error.log
application logs
```

**Indicators**
- high request frequency
- repeated 4xx/5xx responses
- suspicious query strings
- unusual User-Agent values
- authentication anomalies

### Analysis Approach
- observe system behavior
- identify deviations
- map activity to logs
- correlate events

### Key Findings
- vulnerabilities stem from broken trust boundaries
- input validation failures are a primary cause
- logs provide strong detection signals
- effective detection requires correlation

### Defensive Insight

Understanding exploitation improves:
- detection capability
- logging strategy design
- preventative controls
- architectural security

### Governance Considerations
- automation requires human validation
- logs must be complete, accurate, and tamper-resistant

### Conclusion

The Juice Shop lab demonstrates how design and validation failures lead to exploitable conditions. By linking vulnerabilities to observable signals, this analysis strengthens defensive capabilities and detection strategy development.

---

*All testing conducted in an isolated, authorized lab environment.*
