# 🔐 Intrusion Detection System (IDS) using Snort + ELK Stack

## 📌 Project Overview

This project implements a **Network-based Intrusion Detection System (NIDS)** using **Snort IDS** integrated with the **ELK Stack (Elasticsearch, Logstash, Kibana)** to provide real-time monitoring, log analysis, and attack visualization.

The system is designed to simulate real-world attack scenarios and demonstrate how security events are detected, processed, and visualized in a SOC-like environment.

---

## 🎯 Objectives

* Detect network-based attacks using Snort rules
* Collect and centralize logs using ELK Stack
* Visualize security events in real-time via Kibana
* Simulate real-world attack scenarios for analysis

---

## 🏗️ System Architecture

### Components:

* **Kali Linux (Snort IDS Sensor)**

  * Traffic monitoring
  * Rule-based detection
  * Generate alert logs

* **Ubuntu Server (ELK Stack)**

  * Elasticsearch → Log storage
  * Logstash → Log processing
  * Kibana → Visualization
  * Filebeat → Log forwarding

* **Attacker Machine (Kali)**

  * Simulates attacks

* **Victim Machine (Windows)**

  * Generates normal & malicious traffic

---

## 🔄 Data Flow

1. Network traffic is mirrored to Snort
2. Snort analyzes packets and matches rules
3. Alerts are generated (`alert_fast.txt`)
4. Filebeat forwards logs to Logstash
5. Logstash processes and parses logs
6. Elasticsearch stores structured data
7. Kibana visualizes alerts and dashboards

---

## ⚙️ Technologies Used

* Snort IDS
* ELK Stack (Elasticsearch, Logstash, Kibana)
* Filebeat
* Kali Linux & Ubuntu Server
* Wireshark

---

## 📁 Project Structure

```
ids-project/
├── snort/
│   ├── snort.lua
│   └── local.rules
│
├── elk/
│   ├── elasticsearch/
│   │   └── elasticsearch.yml
│   ├── logstash/
│   │   └── beats.conf
│   ├── kibana/
│   │   └── kibana.yml
│   └── filebeat/
│       └── filebeat.yml
│
├── logs/           # Sample Snort logs
├── screenshots/    # Kibana dashboards & alerts
├── docs/           # Project documentation:
                    # - Experimental results and attack scenarios (with evidence screenshots)
                    # - System design and theoretical background
└── README.md
```

---

## 🚨 Attack Scenarios

### 1. 🎣 Phishing (Social Engineering)

* Simulated phishing via malicious links
* Snort detects suspicious HTTP traffic

---

### 2. 🔓 TCP Hijacking

* ARP Spoofing + Session Hijacking
* Detection based on abnormal session behavior

---

### 3. 💻 Command Injection (DVWA)

* Injected malicious commands into web input
* Snort detects payload patterns in HTTP requests

---

### 4. 🦠 Malware Hidden in JPG

* Embedded Base64 payload inside image file
* Snort detects abnormal encoded content

---

## 🛠️ Sample Snort Rule

```snort
alert tcp any any -> any any (
    msg:"MALWARE-JPG Detection";
    flow:established;
    file_data;
    content:"|FF D9|";
    pcre:"/[A-Za-z0-9+\/]{100,}={0,2}/";
    classtype:trojan-activity;
    sid:1000003;
    rev:1;
)
```

---

## 📊 Results

* Successfully detected multiple attack scenarios
* Logs were centralized and visualized in Kibana
* Real-time monitoring of suspicious activities
* Improved visibility of network threats

---

## 📸 Screenshots

> Add screenshots in `/screenshots` folder:

* Kibana dashboard
* Snort alert logs
* Attack detection results

---

## 🎯 Key Learning Outcomes

* Understanding IDS architecture and deployment
* Experience with SIEM (ELK Stack) integration
* Writing and tuning Snort detection rules
* Log analysis and threat detection
* Simulating real-world cyber attacks

---

## ⚠️ Disclaimer

This project is for **educational purposes only**.
All attack simulations were performed in a controlled lab environment.

---

## 👤 Author

**Phan Duy Khuong**
