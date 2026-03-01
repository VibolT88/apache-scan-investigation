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
```
---
### Step 2 — IP Identification

I want to preview what source IP address is presented. Count and sort from greatest to smallest how much they appear in the log.

```bash
awk '{print $1}' acunetix.txt | sort | uniq -c | sort -nr | head
```

---
### Step 3 — HTTP Method Distribution

Demonstrates behavioral pattern analysis

```bash
awk '{ print $6}' acunetix.txt | sort | uniq -c | sort -nr
```
---
### Step 4 — Endpoint Targeting

Show the attack surface what the adversaries are trying to target.

```bash
awk '{ print $7}' acunetix.txt | sort | uniq -c | sort -nr
```
---
### Step 5 — Investigating Status Codes
investigating status code to track adversarie movement.

```bash
awk '{print $9}' acunetix.txt | sort | uniq -c | sort -nr
```
---
### Step 6 — Targeting 500 error breakdown
viewing 500 error codes to if I can find any payloads

```bash
awk '$9 == 500 {print $7}' acunetix.txt | sort | uniq -c | sort -nr | head
```
Payloads found:

---
### Step 7 — Timeline Analysis
Viewing the log for start to finish (how long did it take).

```bash
sort -k4 acunetix.txt | head -1
sort -k4 acunetox.txt | tail -1
```
