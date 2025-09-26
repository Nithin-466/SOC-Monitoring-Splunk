# SOC Monitoring and Log Analysis using Splunk

## Project Overview
This project demonstrates how to analyze logs from multiple sources (Auth logs, Access logs, Wireshark logs, and Firewall logs) using **Splunk**.  
The goal is to detect suspicious activity and visualize attack trends through dashboards.

## Tools & Data Sources
- Splunk Enterprise / Cloud
- Logs:
  - `Auth_task` – Authentication logs
  - `accesslogs` – Web access logs
  - `wireshark.csv` – Network traffic captures
  - `firewalllogs` – Firewall alerts

## Final SOC Dashboard
**Purpose:** Combines all logs into 3 panels:
1. Top Suspicious IPs
2. Most Targeted Ports
3. Top Attack Types
4. <img width="1904" height="916" alt="SOC-Dashboard" src="https://github.com/user-attachments/assets/3059d01d-efad-4106-b536-bb82fd42e289" />


## SPL Queries

**1. Top Suspicious IPs**
index="main"(sourcetype="Auth_task" OR sourcetype="accesslogs" OR source="wireshark.csv" OR sourcetype="firewalllogs") 
| stats count by src_ip 
| sort - count 
| head 10

**2. Most Targeted Ports**

index="main"(source="wireshark.csv" OR sourcetype="firewalllogs") 
| stats count by dst_port 
| sort - count 
| head 10

**3. Top Attack Types**

index="main"(sourcetype="Auth_task" OR sourcetype="accesslogs" OR sourcetype="firewalllogs") 
| stats count by msg 
| sort - count 
| head 10


## Findings / Analysis
- **Top Suspicious IPs:** Identified IPs responsible for most login failures and attacks.
- **Most Targeted Ports:** Ports 80 (HTTP) and 22 (SSH) were attacked most.
- **Top Attack Types:** DoS and brute-force attacks were the most common.

## Conclusion
The SOC Final Dashboard provides a clear view of network and authentication threats, enabling proactive monitoring and mitigation.

## Recommendations
- Block or monitor suspicious IPs.
- Apply stricter authentication policies.
- Regularly monitor frequently targeted ports.
  
## Skills Learned
-Log ingestion and parsing in Splunk
-Building dashboards and panels
-Detecting DoS, brute-force, and scan activity
-Creating professional SOC reports
