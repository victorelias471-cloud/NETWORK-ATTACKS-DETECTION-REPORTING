Network Attack Detection & Reporting

📌 Project Overview

This project demonstrates a controlled cybersecurity lab for network reconnaissance, honeypot monitoring, and network traffic analysis.

The lab uses:

* Kali Linux for reconnaissance and security testing
* Ubuntu 26.04.1 LTS (WSL 2) as the honeypot host
* Cowrie as an SSH honeypot
* Nmap for network reconnaissance
* Wireshark for packet and traffic analysis

The objective is to simulate and document a controlled attack workflow and identify suspicious network activity.

Ethical Notice: All testing is performed in a controlled lab environment against systems owned or authorized for testing.

⸻

🏗️ Lab Architecture

Windows Host
│
├── Kali Linux — VirtualBox
│   └── NAT IP: 10.0.2.15
│
└── Ubuntu 26.04.1 LTS — WSL 2
    └── IP: 172.20.177.139
        │
        └── Cowrie SSH Honeypot

Current Lab IPs

System	Role	IP Address
Kali Linux	Attacker / Reconnaissance	10.0.2.15
Ubuntu WSL 2	Honeypot Host	172.20.177.139

Note: These are the current IP addresses assigned to the lab. WSL 2 IP addresses can change after restarting WSL or Windows, so verify them before future scans.

⸻

🐧 Ubuntu / Cowrie Deployment

Cowrie will run on the Ubuntu WSL 2 environment.

1. Update Ubuntu

sudo apt update

2. Install Required Packages

sudo apt install git python3-venv python3-pip -y

3. Clone Cowrie

git clone https://github.com/cowrie/cowrie.git

4. Enter the Cowrie Directory

cd cowrie

5. Create a Python Virtual Environment

python3 -m venv cowrie-env

6. Activate the Environment

source cowrie-env/bin/activate

7. Upgrade pip

python -m pip install --upgrade pip

8. Install Cowrie Requirements

python -m pip install -r requirements.txt

9. Install Cowrie

python -m pip install -e .

10. Start Cowrie

cowrie start

11. Check Cowrie Status

cowrie status

⸻

🔎 Nmap Reconnaissance

Kali Linux is used to perform reconnaissance against the Ubuntu honeypot.

Target

Ubuntu: 172.20.177.139

Basic Connectivity Test

From Kali:

ping -c 4 172.20.177.139

Service Detection

nmap -sV 172.20.177.139

More Detailed Scan

nmap -sC -sV 172.20.177.139

The scan results can be used to identify exposed services and determine whether Cowrie is reachable.

⸻

🦠 Cowrie SSH Honeypot

Cowrie is used to emulate an SSH service and record interaction with the honeypot.

After starting Cowrie, verify its listening ports:

ss -tulpn

Check Cowrie status:

cowrie status

Cowrie logs can then be reviewed to identify connection attempts and attacker activity.

⸻

📡 Wireshark Traffic Analysis

Wireshark can be used to capture and inspect network traffic between Kali and Ubuntu.

Filter by Ubuntu IP

ip.addr == 172.20.177.139

Filter SSH-related traffic

ip.addr == 172.20.177.139 && tcp.port == 222

The capture can be used to document:

* Connection attempts
* TCP handshakes
* Port scanning activity
* SSH-related traffic
* Suspicious network behaviour

⸻

🧪 Attack / Detection Workflow

1. Start Ubuntu WSL 2
        ↓
2. Start Cowrie
        ↓
3. Confirm Ubuntu IP
   172.20.177.139
        ↓
4. Start Kali Linux
        ↓
5. Test connectivity
        ↓
6. Perform Nmap reconnaissance
        ↓
7. Capture traffic with Wireshark
        ↓
8. Review Cowrie logs
        ↓
9. Document findings
        ↓
10. Produce incident report

⸻

📊 Evidence Collection

The project should contain screenshots/evidence showing:

Cowrie

* Cowrie installation
* Cowrie running
* Cowrie status
* Cowrie logs
* Listening ports

Nmap

* Target IP
* Nmap scan command
* Detected services
* Scan results

Wireshark

* Captured traffic
* Source and destination IP addresses
* TCP/SSH-related traffic
* Relevant packet details

⸻

📁 Repository Structure

Network-Attack-Detection/
│
├── README.md
│
├── screenshots/
│   ├── cowrie-running.png
│   ├── nmap-scan.png
│   └── wireshark-capture.png
│
├── captures/
│   └── cowrie-network-attack-capture.pcap
│
└── reports/
    └── incident-report.md

⸻

📝 Findings

The lab demonstrates how network reconnaissance and honeypot monitoring can be combined to identify suspicious activity.

Example Findings

* Kali successfully communicated with the Ubuntu honeypot.
* Nmap was used to identify exposed services.
* Wireshark provided packet-level visibility into network traffic.
* Cowrie provided logging of SSH interaction attempts.
* Combining network scanning, packet analysis, and honeypot logs provides multiple sources of security evidence.

⸻

🛡️ Recommendations

1. Restrict unnecessary exposed services.
2. Monitor authentication attempts.
3. Use network segmentation for sensitive systems.
4. Maintain centralized security logs.
5. Monitor unusual scanning activity.
6. Use strong authentication and access controls.
7. Regularly review firewall and network rules.
8. Deploy IDS/IPS solutions where appropriate.

⸻

🎯 Learning Outcomes

Through this project, I practiced:

* Linux administration
* Virtualized cybersecurity labs
* WSL 2 networking
* Network reconnaissance
* Nmap
* SSH security concepts
* Cowrie honeypot deployment
* Wireshark packet analysis
* Security evidence collection
* Incident documentation

⸻

⚠️ Ethical Notice

All reconnaissance, scanning, packet capture, and security testing in this project are performed against systems that I own or have explicit authorization to test.

The techniques demonstrated should not be used against unauthorized systems or networks.

⸻

👤 Author

Ismail Victor Elias

Cybersecurity Learner | Network Security | Ethical Hacking