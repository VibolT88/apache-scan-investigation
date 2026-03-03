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
- DVWA lab enviorment
- Tools Used: grep, awk, sort, uniq, wc
___
### Step 1 — Determine Scope of Log

I wanted to determine how large the file and it is structured.
Here’s a command to count lines:

```bash
wc -l acunetix.txt
head -n 3 acunetix.txt
```
---
### Step 2 — IP Identification

I want to preview what source IP address is presented. Count and sort from greatest to smallest how much they appear in the log.

```bash
awk '{print $1}' acunetix.txt | sort | uniq -c | sort -nr | head
```

---
### Step 3 — HTTP Method Distribution

After viewing the I.P address, I've looked up the HTTP Methods with in the logs to see if there are any irregular patterns.


```bash
awk '{ print $6}' acunetix.txt | sort | uniq -c | sort -nr
```
---
### Step 4 — Endpoint Targeting

want to view if there is a specific target area the adeversaries are trying to target.


```bash
awk '{ print $7}' acunetix.txt | sort | uniq -c | sort -nr
```
---
### Step 5 — Investigating Status Codes
Now Im investigating status code to track adversarie movement.

```bash
awk '{print $9}' acunetix.txt | sort | uniq -c | sort -nr
```
---
### Step 6 — Targeting 500 error breakdown

Analyzing 500 error responses, I want to view any endpoints that generate the highest volume of server error under malicious input conditions. 
This suggests insufficient input validation and highlights a potentially exploitable attack surface.

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
---
## What I learned

This project helped me understand that effective log analysis goes far beyond running simple commands like grep. While filtering logs is important, meaningful investigation requires organizing and structuring the data to build a clear timeline of adversary activity.
One of the biggest takeaways was learning to focus on behavior patterns rather than isolated log entries. For example:
Repeated ../ sequences indicated potential directory traversal attempts.
<script> tags suggested possible cross-site scripting (XSS) probes.
SQL logic operators such as ' OR 1=1 -- pointed toward SQL injection attempts.
I also observed that high-frequency requests within short time intervals often signal automated scanning tools rather than legitimate user activity. Additionally, analyzing user-agent strings provided insight into whether the traffic was coming from normal browsers or automated frameworks.
This project reinforced the importance of:
Pattern recognition over single-event analysis
Building timelines to understand attacker movement
Differentiating between normal and abnormal behavior
Thinking like an analyst, not just a command-line operator
Overall, this experience strengthened my understanding of how web-based attacks appear in real log data and how to systematically investigate suspicious activity.
