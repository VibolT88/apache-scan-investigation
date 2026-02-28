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

Check total number of lines in the log:

```bash
wc -l acunetix.txt



---

### 🔹 Step 2 — Log Format

```markdown
### Step 2 — Inspect Log Format

Check the first few lines to understand log structure:

```bash
head -n 5 acunetix.txt
