# Phase 1.3 – Detection Hypotheses

## Detection Philosophy
- Detection is behavior-based, not signature-based
- Focus on attacker actions rather than specific tools
- Every attack step must produce at least one observable signal

## Detection Table

| Attack Step            | Observable Signal                          | 
Log Source                 | Why It Matters |
|------------------------|--------------------------------------------|----------------------------|----------------|
| Initial Access         | Repeated HTTP requests / anomalies         | 
Web server access logs     | Indicates possible probing or exploitation 
attempts |
| Execution              | Suspicious command execution               | OS 
/ auth logs             | Shows post-compromise activity |
| Persistence            | New user or scheduled task creation        | 
System logs                | Indicates attempt to maintain access |
| Privilege Escalation   | Use of elevated permissions                | 
Auth / sudo logs           | Critical escalation indicator |
| Lateral Movement       | Internal connection attempts               | 
Network / VPC logs         | Suggests expansion within environment |
| Objective              | Access to sensitive logs or credentials    | 
Splunk / auth logs         | Confirms attacker goal |

## Gaps & Blind Spots
- Encrypted traffic limits deep packet inspection
- Short-lived attacks may evade correlation
- Lab environment does not include full endpoint telemetry (EDR)

## SOC Relevance
- Provides a structured investigation path
- Helps analysts map alerts to attacker intent
- Supports faster triage and escalation decisions

