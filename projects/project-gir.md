---
layout: page
title: Project G.I.R.
---

# Project G.I.R. (Glitch, Intrude, Repeat)

**Status:** *Active Development / Independent Research*

## Overview
Project G.I.R. is my personal modular learning framework designed to structure my hands-on cybersecurity training. It serves as a practical laboratory to apply concepts learned in the Merit America curriculum, specifically focusing on vulnerability assessment, automation discipline, and defensive context.

## Why This Exists
In cybersecurity, "tool fatigue" can set in quickly. I created Project G.I.R. to:
1.  **Move beyond "point-and-click":** Understand how security tools work under the hood.
2.  **Contextualize findings:** Instead of just finding a vulnerability, I want to understand its business impact and remediation.
3.  **Practice safe automation:** Learn how to script security tasks without causing system instability or scope creep.

## Architecture & Philosophy
Project G.I.R. is built on the philosophy of **3v1l T3chnol0gies** (my personal learning ecosystem namespace), which centers on "Responsible Automation."

### Core Principles
-   **Human-in-the-Loop:** No action is taken by the system without an authorized user reviewing the proposed step. This enforces judgment and prevents accidental actions.
-   **Defensive Focus:** The goal is not to exploit, but to identify, document, and remediate.
-   **Safety Scopes:** All activities are strictly bound to recognized, authorized IP ranges (my local lab).

### High-Level Components
1.  **Scanner Integration:** (e.g., Nmap, Nikto) Wrapper scripts that run scans with non-destructive flags.
2.  **Risk Scoring Engine:** A logic layer that interprets raw scan output and assigns a "Risk Context" score based on potential impact (Low, Medium, High).
3.  **Reporting Module:** a simple output formatter that translates technical logs into human-readable summaries.

## Alignment with Classroom Learning
This project directly reinforces my studies in:
-   **Python/Scripting:** Writing the glue code to connect modules.
-   **Networking:** Understanding ports, protocols, and services during the scanning phase.
-   **Risk Management:** Deciding which findings matter and why.

## Ethical Boundaries
*Project G.I.R. is strictly for educational use on systems I own.*
-   It includes hard-coded "guardrails" to prevent execution against public IP addresses.
-   It does not contain exploitation payloads.
-   It is a tool for learning *defense* by understanding *offense*.

---
[Return to Home](../index.md)
