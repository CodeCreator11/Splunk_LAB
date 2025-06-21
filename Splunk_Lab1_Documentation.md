
# Lab 1: Splunk Log Monitoring & Alerting - Documentation

## 🧠 Executive Summary

This lab focused on configuring Splunk to collect system logs from a Windows 11 machine and building an alert to detect suspicious authentication events. The purpose was to simulate a basic but critical SOC function: identifying brute force attacks through event log monitoring. I installed Splunk, configured data inputs, tested some detection searches, and created an alert—all from scratch and on my own machine.

---

## 🛠️ Environment Details

- **SIEM Platform:** Splunk Enterprise (installed on local Windows PC)
- **System Monitored:** Windows 11 Admin PC (192.xxx.xx.xxx)
- **Data Source:** Local Windows Event Logs (Application, System, Security)
- **Network Layout:** Isolated VLAN 10 (Admin/Defender Zone)

---

## 🔍 Steps Performed

### 1. Installed Splunk Enterprise
- Chose C:\Program Files\Splunk as install path
- Used ports: 8000 (UI), 8089 (mgmt), 8191 (KV Store)

### 2. Configured Splunk Web
- Accessed via Brave browser at `http://localhost:8000`
- Skipped SSL to avoid certificate issues

### 3. Enabled Data Input
- Went to Settings > Data Inputs > Local Event Logs
- Selected: **Application**, **System**, and **Security**
- Indexed using `main` index

### 4. Confirmed Log Ingestion
- Ran search: `index=main`
- Verified events were streaming in with relevant metadata

### 5. Built Detection Query
```spl
index=main ("failed" OR "invalid password" OR "authentication failure")
```
- Detected Windows failed logons, system failures, MSI errors

### 6. Created an Alert
- Type: Real-Time
- Title: `BruteForce Attack`
- Triggered: If results > 0
- Alert Action: Saved for now, can be expanded with email/webhook

---

## 📊 What I Learned

- How to configure and use Splunk from scratch
- How log data is parsed and indexed
- What typical brute-force logs look like on a Windows host
- How to create meaningful alerts from high-volume logs

---

## 🗺️ Network Diagram

```
+-------------------+        +---------------------+         +--------------------+
|   Internet (ISP)  |<-----> |  TP-Link Router     | <-----> | TP-Link Switch     |
|                   |        | Port 1 (WAN)        |         | Port 1 = Router    |
+-------------------+        | Port 2 = Switch     |         | Port 2 = Kali      |
                             | Port 3 = PC Admin   |         | Port 3 = PC Admin  |
                             +---------------------+         +--------------------+

             VLAN 10: Admin Zone (PC - 192.xxx.xx.x)
             VLAN 20: Attack Zone (Kali - 192.xxx.xx.x)
```

---

## 📌 TL;DR for Hiring Manager

In this lab, I installed and configured Splunk from scratch on my own PC to simulate a real-world SIEM setup. I configured it to ingest system and security logs from Windows and built a working detection rule that would trigger alerts on brute-force attempts. This showcases my ability to:
- Set up log collection infrastructure
- Parse and query logs using SPL
- Create SOC-style detection and alerting pipelines
- Work independently and document it clearly

---

✅ **Lab Complete** | 💾 Splunk Logs Collected | 🚨 Alert Operational
