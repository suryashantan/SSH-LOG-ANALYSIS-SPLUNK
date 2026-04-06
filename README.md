# 🔐 SSH Log Analysis using Splunk (SOC Project)

## 📌 Overview

This project demonstrates SSH log analysis using Splunk SIEM to detect brute-force attacks, failed logins, successful logins, and suspicious connections.

It simulates a real-world SOC investigation scenario and maps detections to MITRE ATT&CK.

---

## 🎯 Objectives

* Detect failed SSH login attempts
* Identify brute-force attacks
* Track successful logins
* Detect suspicious unauthenticated connections
* Build visualizations and alerts in Splunk

---

## 🛠️ Lab Setup

* Splunk Enterprise (SIEM)
* Windows Virtual Machine
* SSH logs dataset (JSON format)
* Kali Linux (optional attacker machine)

---

## ⚙️ Data Ingestion

* Uploaded `ssh_logs.json` into Splunk
* Configured:

  * `sourcetype = _json`
  * `index = ssh_logs`

📸 Screenshot:
![Data Ingestion](screenshots/task1_log_parsing.jpg)

---

## 🔍 Task 1: Log Parsing

Extracted fields:

* event_type
* id.orig_h (Source IP)
* id.resp_h (Destination IP)

**Query:**

```
index=ssh_logs 
| stats count by event_type
```

📸 Screenshot:
![Log Parsing](screenshots/task1_log_parsing.jpg)

---

## 🔍 Task 2: Failed Login Detection

**Query:**

```
index=ssh_logs event_type="Failed SSH Login"
| stats count by id.orig_h 
| sort -count 
| head 10
```

📸 Screenshots:
![Failed Login Stats](screenshots/task2_failed_logins_stats.jpg)
![Failed Login Chart](screenshots/task2_failed_logins_chart.jpg)

---

## 🔍 Task 3: Brute Force Detection

**Query:**

```
index=ssh_logs event_type="Multiple Failed Authentication Attempts"
| stats count by id.orig_h, id.resp_h
```

📸 Screenshot:
![Brute Force](screenshots/task3_bruteforce.jpg)

---

## 🔍 Task 4: Successful Login Tracking

**Query:**

```
index=ssh_logs event_type="Successful ssh login"
| stats count by id.orig_h, id.resp_h
```

📸 Screenshot:
![Successful Logins](screenshots/task4_successful_logins.jpg)

---

## 🔍 Task 5: Suspicious Connections

**Query:**

```
index=ssh_logs event_type="Connection Without Authentication"
| timechart count by id.orig_h
```

📸 Screenshot:
![Suspicious Connections](screenshots/task5_suspicious_connections.jpg)

---

## 📊 Key Outcomes

* Detected brute-force attack patterns
* Identified suspicious login behavior
* Created alerts for SOC monitoring
* Visualized attack trends

---

## 🧠 MITRE ATT&CK Mapping

* T1110 – Brute Force

---

## 🚀 Skills Demonstrated

* Splunk SIEM
* Log analysis & threat detection
* SPL query writing
* Security monitoring
* Data visualization

---

## 📌 Future Improvements

* Add geo-IP enrichment
* Integrate threat intelligence
* Build advanced correlation rules
* Create SOC dashboard

---

## 👨‍💻 Author

Surya
Aspiring SOC Analyst / VAPT Enthusiast

---

## ⭐ Support

If you found this useful, give this repo a star ⭐


this is readme file , i want u to add screenshots links in it ,
