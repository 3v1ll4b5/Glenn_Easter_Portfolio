# SQL for Security Analysis

*Applying database skills to security log analysis.*

---

## **Coming Soon**

As part of my training, I am learning how structured query language (SQL) is used not just for database management, but for querying large datasets typical of SIEM (Security Information and Event Management) logs. This section will demonstrate my ability to construct queries to find anomalies or specific patterns.

---

### Template for Future Entries

#### Scenario: [e.g., Detecting Failed Login Spikes]
**Objective:** Identify potential brute-force attempts from authentication logs.

**Query Logic:**
*Searching for > 5 failed login attempts from a single IP within 1 minute.*

**Example Query:**
```sql
/* SAMPLE CODE - DO NOT RUN ON PROD WITHOUT REVIEW */
SELECT 
    source_ip, 
    COUNT(*) as failed_attempts,
    MIN(timestamp) as start_time,
    MAX(timestamp) as end_time
FROM 
    auth_logs
WHERE 
    status = 'FAILED'
GROUP BY 
    source_ip
HAVING 
    COUNT(*) > 5;
```

**Interpretation:**
*Explanation of what the results would tell an analyst.*

---
[Return to Home](../README.md)
