---
layout: page
title: Vulnerable System Analysis
---

# Vulnerable System Analysis Reports

Technical assessments of authorized lab targets conducted in isolated environments.

---

## Assessment Report

**Target System:** Metasploitable 2 (Linux)  
**Date:** February 2026  
**Scope:** Internal Lab Network – 192.168.56.0/24  

---

### Executive Summary

The assessed system intentionally contains multiple high-risk vulnerabilities designed for security training. The overall security posture is critically weak due to exposed services, outdated software versions, and weak authentication controls. Several services allow unauthorized access or facilitate privilege escalation if left unpatched in a production environment.

Immediate remediation would require service hardening, credential management, and elimination of legacy software.

---

## Findings

---

### 1. Exposed FTP Service with Anonymous Access

**Severity:** High  
**CVSS Context:** High (Confidentiality & Integrity Impact)

**Description:**  
The FTP service is configured to allow anonymous authentication. This permits unauthenticated users to list directory contents and potentially access sensitive files.

**Business Impact:**  
In a production environment, anonymous file access could lead to:
- Data leakage
- Credential exposure
- Reconnaissance for further exploitation

Publicly accessible file shares significantly increase attack surface.

**Remediation Recommendation:**  
- Disable anonymous authentication.
- Restrict FTP access via firewall rules.
- Replace legacy FTP with secure alternatives (e.g., SFTP).
- Implement authentication logging and monitoring.

---

### 2. Outdated Web Application Components

**Severity:** Medium–High  

**Description:**  
The web application stack contains outdated software versions with known vulnerabilities. Version enumeration indicates exposure to publicly documented exploits.

**Business Impact:**  
Unpatched web services increase the likelihood of:
- Remote code execution
- Data exfiltration
- Website defacement
- Lateral movement within the network

**Remediation Recommendation:**  
- Apply current vendor patches.
- Remove deprecated components.
- Implement routine vulnerability scanning and patch cadence.
- Deploy web application firewall (WAF) protections.

---

### 3. Weak Credential Practices

**Severity:** High  

**Description:**  
Several services use default or weak credentials that are easily guessable.

**Business Impact:**  
Weak authentication controls significantly reduce the effort required for unauthorized access. In production, this could enable privilege escalation and full system compromise.

**Remediation Recommendation:**  
- Enforce strong password policies.
- Eliminate default credentials.
- Implement multi-factor authentication where applicable.
- Conduct periodic credential audits.

---

## Overall Risk Assessment

The system demonstrates systemic security weaknesses typical of unmaintained legacy environments. Risk concentration is high due to overlapping vulnerabilities and poor segmentation controls.

This assessment reinforces the importance of:
- Service minimization
- Patch management
- Credential governance
- Network segmentation

---

*All testing was conducted within an isolated, authorized lab environment.*
