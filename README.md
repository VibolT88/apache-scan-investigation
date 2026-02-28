# Apache Web Log Investigattion

---

## Incident Overview
This project simulates a SOC Level 1 investigation of suspicious activity identified within Apache web server access logs. During log review, a high volume of HTTP requests originating from a single source IP address was observed, including an unusually large number of POST requests and exploit-style payload patterns.
The objective of this investigation was to determine whether the activity represented automated vulnerability scanning and to assess whether any signs of successful compromise were present.

## Environment

- Analysis Platform: Ubuntu
- Log Type: Apache access logs
- Tools Used: grep, awk, sort, uniq, wc

## Investigation Objectives

- Identify suspicious traffic patterns
- Determine whether the activity was automated scanning
- Detect possible exploit attempts
- Assess whether any successful compromise occurred

## Key Findings

- Total log entries analyzed: 6,538
- All traffic originated from a single source
- Unusually high POST volume observed
- Detected 4 Shellshock-style payload attempts
- No confirmed evidence of compromise based on access logs
