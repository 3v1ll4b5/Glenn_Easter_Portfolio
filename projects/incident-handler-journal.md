---
layout: page
title: Incident Handling Methodologies
---

# Incident Handling Methodologies

Structured simulation of incident response workflows based on NIST SP 800-61 and SANS PICERL frameworks.

---

## Simulation: Phishing-Based Credential Harvesting Attempt

**Framework Applied:** NIST SP 800-61

---

### 1. Preparation

Baseline controls assumed in place:

- Email filtering and spam detection
- Endpoint antivirus / EDR
- Centralized log collection
- User security awareness training
- Incident escalation playbook

Response tools available:

- SIEM platform for log analysis
- Endpoint investigation utilities
- Account management tools for credential resets
- Internal communication escalation process

---

### 2. Detection & Analysis

**Trigger Event:**
Multiple users reported suspicious email messages requesting password verification via external link.

**Initial Indicators:**
- Email sender domain visually similar to internal domain
- Embedded hyperlink redirecting to non-corporate domain
- High urgency language within message

**Log Review Findings:**
- Several successful link clicks recorded in proxy logs
- No immediate malicious payload execution detected
- Two affected accounts attempted authentication from unusual IP addresses within 15 minutes of link interaction

**Scope Determination:**
- Identified impacted user accounts
- Queried authentication logs for anomalous login attempts
- Verified whether lateral movement occurred

Scope confirmed limited to credential exposure risk, no confirmed system compromise.

---

### 3. Containment, Eradication & Recovery

**Containment Actions:**
- Forced password reset for affected accounts
- Invalidated active authentication sessions
- Blocked malicious domain at firewall and email gateway

**Eradication:**
- Removed phishing emails from inboxes via centralized admin tools
- Conducted endpoint scans for persistence mechanisms (none detected)

**Recovery:**
- Confirmed normal login behavior restored
- Monitored accounts for 48 hours for abnormal access patterns
- Communicated outcome to affected users

---

### 4. Post-Incident Activity

**Lessons Learned:**
- Email filter tuning required for domain impersonation patterns
- MFA enforcement reduces impact of credential harvesting
- Faster user reporting significantly reduces exposure window

**Recommended Improvements:**
- Implement stricter domain similarity detection rules
- Enforce mandatory MFA across all accounts
- Conduct quarterly phishing simulation exercises
- Update incident playbook with refined credential exposure workflow

---

## Operational Reflection

This exercise reinforces the importance of structured scope assessment before escalation. Not all phishing events result in compromise, but disciplined log correlation and rapid containment are critical in preventing credential misuse.

The goal of incident response is not speed alone, but controlled decision-making under uncertainty.
