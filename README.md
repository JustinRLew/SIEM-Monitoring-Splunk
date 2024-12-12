# SIEM Monitoring Project with Splunk

This project demonstrates the implementation of a Security Information and Event Management (SIEM) system using **Splunk**. The purpose of the project is to monitor a simulated network, detect security threats, and respond to incidents in real-time. This project showcases skills in deploying and configuring a SIEM solution, creating detection rules, visualizing data, and automating alerts.

---

## Project Overview

A SIEM system collects and analyzes log data from devices like servers, workstations, and firewalls. In this project:
- **Splunk** is used as the SIEM tool.
- Logs from Windows clients are forwarded to the Splunk server hosted on an AWS EC2 instance.
- Detection rules identify potential threats, and alerts notify the user of suspicious activity.
- Dashboards provide real-time visualizations of network security events.

---

## Features

- **Log Collection:** Centralized logging from Windows client machines.
- **Threat Detection:** Rules to detect brute force attacks, unauthorized access, and other suspicious activities.
- **Alerting:** Real-time alerts via Splunk for critical incidents.
- **Visualization:** Interactive dashboards showing trends, geolocations, and activity summaries.
- **Scalability:** Configurable for larger networks with distributed Splunk architecture.

---

## Architecture

The project uses a simulated network hosted on AWS:
- **SIEM Server:** Windows Server EC2 instance with Splunk installed.
- **Client Machines:** Windows EC2 instances forwarding logs to the SIEM server.
- **Network:** Private VPC with restricted access and encrypted log transmission.

---

## Setup and Installation

### Prerequisites

1. AWS account with access to create EC2 instances.
2. Windows Server 2019 or later for the SIEM server.
3. Splunk Enterprise and Universal Forwarder installers.
4. Basic understanding of Windows Event Logs and networking.

---

### Steps

#### 1. **Set Up AWS Environment**
- Launch an EC2 instance for the SIEM server (Windows Server).
- Launch additional EC2 instances for Windows clients.
- Configure VPC and security groups to allow necessary traffic (e.g., RDP and Splunk ports).

#### 2. **Install Splunk**
- Download and install Splunk on the SIEM server.
- Set up an admin account and start the Splunk service.

#### 3. **Configure Log Forwarding**
- Install Splunk Universal Forwarder on each client machine.
- Configure the forwarder to send logs to the SIEM server.

#### 4. **Create Detection Rules**
- Define rules in Splunk to detect specific security events, such as:
  - Failed login attempts (Event ID 4625).
  - Unauthorized file access (Event ID 4656).

#### 5. **Build Dashboards**
- Use Splunk’s search and reporting features to create visual dashboards for real-time monitoring.

---

## Detection Rules

### 1. Brute Force Attack Detection
**Rule:**  
Trigger an alert when there are more than 5 failed login attempts within 5 minutes.  
**Query:**  
```spl
index="windows-security" EventCode=4625 | stats count by Account_Name
```

### 2. Unauthorized Access
Rule:
Alert when sensitive files or directories are accessed without proper permissions.
Query:

spl
index="windows-security" EventCode=4656 Accesses="WRITE_DAC" | table Account_Name, Object_Name

### Dashboards and Visualization

**Key Dashboards**
Login Failure Trends: Shows failed login attempts over time.
Geolocation of Access Attempts: Maps login attempts by source IP.
Top Threats: Highlights the most frequent alerts and affected accounts.

Example Dashboard Screenshot


### Testing and Validation  
Simulated Security Events
Brute Force Attack Simulation:

Use a PowerShell script to generate failed login attempts.
Verify if alerts are triggered in Splunk.

Unauthorized Access Simulation:

Attempt to access restricted files or directories.

Results
Alerts triggered as expected.
Dashboards updated in real-time with logged events.

Future Enhancements
Distributed Architecture:
Add indexers and search heads for scalability.
Threat Intelligence Integration:
Use external feeds to flag known malicious IPs.
Automated Responses:
Automate IP blocking and account locking for critical alerts.
