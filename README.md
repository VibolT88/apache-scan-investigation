# Apache Web Log Investigattion
This project demonstrates a security-focused investigation of Apache access logs to identify suspicious scanning activity and potential exploit attempts.
---

## Objective
Simulate a SOC Level 1 analyst’s workflow analyzing Apache access logs to:
- Identify anomalous request patterns
- Quantify HTTP methods and status codes
- Detect potential exploit behavior
- Assess whether any successful compromise occurred

## Background

Web servers produce access logs that record incoming HTTP requests. These logs can reveal normal user behavior as well as malicious activity (scanning, exploitation attempts, enumeration phases). This lab uses a real Apache access log sample to simulate a threat investigation.


## Environment

- Analysis Platform: Ubuntu
- Log Type: Apache access logs
- Tools Used: grep, awk, sort, uniq, wc
___
### Step 1 — Determine Scope of Log

Here’s a command to count lines:

```bash
wc -l acunetix.txt
