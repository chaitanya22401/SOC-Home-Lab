# SOC-Home-Lab

A practical cybersecurity portfolio documenting hands-on Security Operations Center (SOC) and Blue Team projects.

This repository showcases the implementation of security monitoring environments, SIEM technologies, endpoint telemetry collection, threat detection, security event analysis, and investigation workflows.

The objective is to demonstrate practical technical competencies relevant to SOC Analyst L1/L2 responsibilities through documented lab implementations and verifiable evidence.

## Portfolio Objectives

- Implement and configure security monitoring technologies.
- Collect and analyze Windows, Linux, and network security telemetry.
- Investigate authentication and endpoint security events.
- Develop practical threat detection and monitoring capabilities.
- Understand SIEM architecture and security event pipelines.
- Apply MITRE ATT&CK concepts to security investigations.
- Document technical implementations, challenges, findings, and limitations.

## SOC Projects

| No. | Project | Primary Focus |
|---|---|---|
| 01 | Windows Endpoint Threat Detection and Monitoring| Wazuh, SIEM, Windows telemetry, FIM 
| 02 | Windows Endpoint Attack Simulation and Threat Detection | Windows attack simulation and detection
| 03 | Linux Endpoint Attack Simulation and Threat Detection | Linux security monitoring and detection 
| 04 | Network Security Monitoring and Threat Hunting | Security Onion, Zeek, Suricata, Wireshark 


## Project 01: Windows Endpoint Threat Detection and Monitoring
[View Project 01](./Windows-Endpoint-Threat-Detection-and-Montioring/)

## Project 02: Linux Adversary Simulation and Detection Engineering
[View Project 02](./Linux-Adversary-Simulation-and-Detection-Engineering/)

## Project 03: Linux Endpoint Threat Detection

Planned implementation of Linux authentication monitoring, suspicious activity investigation, system auditing, and endpoint threat detection.

## Project 04: Network Security Monitoring

Planned network monitoring and threat hunting using Security Onion, Zeek, Suricata, and Wireshark.

---

## Technologies and Tools

| Category | Technologies |
|---|---|
| SIEM | Wazuh |
| Operating Systems | Windows 11, Ubuntu Server |
| Virtualization | Oracle VirtualBox |
| Endpoint Monitoring | Wazuh Agent |
| Windows Logging | Windows Security Events, PowerShell Operational Logs |
| File Monitoring | Wazuh File Integrity Monitoring |
| Network Monitoring | Security Onion, Zeek, Suricata, Wireshark |
| Documentation | Markdown, Git, GitHub |

---

## Lab Environment

The initial SIEM project uses the following environment:

| Component | Configuration |
|---|---|
| Host OS | Windows 11 |
| Hypervisor | Oracle VirtualBox 7.2.4 |
| SIEM Server OS | Ubuntu Server 24.04.5 LTS |
| SIEM Platform | Wazuh |
| SIEM Server RAM | 6 GB |
| SIEM Server CPU | 4 vCPUs |
| Virtual Disk | 80 GB dynamically allocated |
| Endpoint | Windows 11 |
| Endpoint Agent | Wazuh Agent 4.14.10 |
| Network | VirtualBox NAT with port forwarding |

**Resource limitation:** The Wazuh server VM has 6 GB RAM, below the 8 GB RAM recommendation in Wazuh's Quickstart requirements. This is a constrained educational lab deployment, not a production sizing recommendation.

---

## Repository Structure

```text
SOC-Home-Lab-Portfolio/
│
├── README.md
│
├── 01-Windows-Endpoint-Threat-Detection-and-Monitoring/
│   ├── README.md
│   ├── architecture/
│   ├── configurations/
│   ├── investigation-reports/
│   ├── screenshots/
│
├── 02-Windows-Endpoint-Threat-Detection/
│   └── README.md
│
├── 03-Linux-Endpoint-Threat-Detection/
│   └── README.md
│
└── 04-Network-Security-Monitoring/
    └── README.md
```

---

## Documentation and Evidence Standards

Each project will include:

- Project objectives and scope.
- Technical architecture.
- Tools and technologies.
- Lab environment details.
- Installation and configuration procedures.
- Implementation walkthrough.
- Detection and monitoring methodology.
- Screenshots and supporting evidence.
- Investigation findings.
- Challenges and troubleshooting.
- Results and limitations.
- Lessons learned.

---

**Disclaimer:** This repository documents authorized educational lab environments and controlled security simulations. It is intended for cybersecurity learning and professional portfolio development.
