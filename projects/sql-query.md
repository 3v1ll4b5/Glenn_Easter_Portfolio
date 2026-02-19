# SQL for Security Analysis

Applying structured query language (SQL) to security detection, log investigation, and anomaly analysis.

---

## Overview

In security operations environments, SQL is not just a database skill — it is a detection and investigation tool.

This section demonstrates how I translate security hypotheses into structured queries against authentication logs and event telemetry. The focus is not simply data retrieval, but:

- Converting threat scenarios into measurable patterns
- Aggregating events into meaningful investigative views
- Distinguishing noise from signal through structured filtering
- Producing outputs that support triage and escalation decisions

---

## Scenario: Detecting Failed Login Spikes

**Objective:**  
Identify high-frequency failed authentication attempts that may indicate brute-force or automated attack behavior.

**Detection Hypothesis:**  
A source IP generating repeated failed logins within a short time window may represent malicious activity rather than normal user error.

**Query Strategy:**
- Filter for failed authentication events
- Group by source and time bucket
- Count attempts within defined intervals
- Surface only activity exceeding a defined threshold

**Example Query:**

```sql
/* SAMPLE QUERY — VALIDATE SCHEMA AND ENVIRONMENT BEFORE USE */
SELECT
    source_ip,
    DATE_TRUNC('minute', timestamp) AS time_window,
    COUNT(*) AS failed_attempts,
    MIN(timestamp) AS first_attempt,
    MAX(timestamp) AS last_attempt
FROM auth_logs
WHERE status = 'FAILED'
GROUP BY source_ip, DATE_TRUNC('minute', timestamp)
HAVING COUNT(*) > 5
ORDER BY failed_attempts DESC;
```
