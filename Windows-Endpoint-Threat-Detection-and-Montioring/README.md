# Windows Endpoint Threat Detection and Monitoring

## Project Overview

This project demonstrates practical Windows endpoint monitoring using Wazuh.

The implemented use cases cover authentication activity, local account management, file integrity monitoring, and PowerShell event collection.

The environment is an educational home lab with a limited virtual machine resource allocation.

## 1. Project Objectives

The main objectives of this project are:

- Deploy and configure Wazuh for endpoint security monitoring.
- Integrate a Windows 11 endpoint with the Wazuh server.
- Collect and examine Windows security events.
- Monitor successful and failed authentication attempts.
- Detect local user account creation and deletion activities.
- Configure File Integrity Monitoring to monitor file activities.
- Collect PowerShell operational events.
- Examine collected security events through the Wazuh dashboard.
- Understand how endpoint telemetry supports SOC monitoring and investigation workflows.

## 2. Included Activities:

1. Wazuh server deployment on Ubuntu Server.
2. Windows endpoint agent installation and enrollment.
3. Windows Security, System, and Application event collection.
4. Authentication event monitoring.
5. Local user account management monitoring.
6. File Integrity Monitoring.
7. PowerShell operational event collection.
8. Reviewing collected events through the Wazuh dashboard.

## 3. Implemented Use Cases

| Security activity | Windows event |
|---|---|
| Failed logon attempts | Event ID 4625 
| Successful logons | Event ID 4624 
| Local user account creation | Event ID 4720 
| Local user account deletion | Event ID 4726 
| File creation, modification and deletion | Wazuh FIM 
| PowerShell script block activity | Event ID 4104 

## 4. Tools and Technologies

| Tool / Technology | Purpose |
|---|---|
| Wazuh 4.14.10 | Centralized SIEM |
| Ubuntu Server 24.04.5 LTS | Wazuh server operating system |
| Windows 11 | Monitored endpoint |
| Wazuh Agent 4.14.10 | Endpoint event collection |
| Oracle VirtualBox 7.2.4 | Virtual machine environment |
| Windows Event Viewer | Windows event log verification |
| PowerShell | Endpoint activity generation and event testing |
| Wazuh Dashboard | Security event monitoring and analysis |

## 5. Lab Environment

### 5.1 Host Machine

| Component | Specification |
|---|---|
| Operating System | Windows 11 |
| Processor | Intel Core i5-13450HX |
| RAM | 16 GB |
| Storage | 1 TB SSD |
| Virtualization Platform | Oracle VirtualBox 7.2.4 |

### 5.2 Wazuh Server Virtual Machine

| Component | Configuration |
|---|---|
| VM Name | Ubuntu-SOC-Lab |
| Operating System | Ubuntu Server 24.04.5 LTS |
| RAM | 6 GB |
| CPU | 4 vCPUs |
| Storage | 80 GB dynamically allocated |
| Wazuh Version | 4.14.10 |
| Deployment | All-in-one |

The Wazuh server runs the manager, indexer, and dashboard components.

**Lab limitation:** The server VM has 6 GB RAM, below the commonly recommended 8 GiB baseline for a small Wazuh Quickstart deployment. This is a constrained educational environment and not a production sizing recommendation.

### 5.3 Monitored Endpoint

| Component | Configuration |
|---|---|
| Operating System | Windows 11 |
| Agent Name | WIN11-SOC-ENDPOINT |
| Wazuh Agent Version | 4.14.10 |
| Agent Status | Active and connected |

### 5.4 Network Configuration

The virtual machine uses VirtualBox NAT networking with port forwarding.

| Service | Host Address and Port | Guest Port |
|---|---|---|
| Wazuh Dashboard | 127.0.0.1:8443 | 443 |
| SSH | 127.0.0.1:2222 | 22 |
| Wazuh Agent Communication | Host port 1514 | 1514 |
| Wazuh Agent Enrolment | Host port 1515 | 1515 |

The Wazuh dashboard is accessed locally through:

`https://127.0.0.1:8443`

## 6. Technical Architecture

The lab follows a centralized endpoint monitoring architecture.

### 6.1 Architecture Components

- **Windows 11 Endpoint:** Generates authentication, account management, file activity, and PowerShell events.
- **Wazuh Agent:** Collects configured endpoint telemetry and forwards it to the Wazuh server.
- **Wazuh Manager:** Receives and processes endpoint security data.
- **Wazuh Indexer:** Stores indexed security information.
- **Wazuh Dashboard:** Provides a centralized interface to examine collected events.

### 6.2 Event Monitoring Flow

1. Security-relevant activity occurs on the Windows endpoint.
2. Windows records the activity in its event logs.
3. The Wazuh agent collects configured event channels and FIM activity.
4. The agent communicates with the Wazuh manager.
5. Wazuh processes and indexes the collected information.
6. The analyst reviews available event information through the dashboard.

## 7. Installation and Configuration

### 7.1 Wazuh Server Deployment

Wazuh was deployed as an all-in-one installation on an Ubuntu Server 24.04.5 LTS virtual machine.

The deployment includes:

- Wazuh Manager
- Wazuh Indexer
- Wazuh Dashboard

After installation, the service health was checked to confirm that the central components were operational.

### 7.2 Windows Agent Integration

The Wazuh 4.14.10 agent was installed on the Windows 11 endpoint.

The endpoint was enrolled with the Wazuh manager and assigned the agent name:

`WIN11-SOC-ENDPOINT`

Agent connectivity was verified through the Wazuh dashboard.

### 7.3 Windows Event Channel Collection

The Windows agent configuration was reviewed in:

`C:\Program Files (x86)\ossec-agent\ossec.conf`

The configured event channels included:

- Application
- Security
- System
- Microsoft-Windows-PowerShell/Operational

The PowerShell Operational channel was configured for event collection.

### 7.4 File Integrity Monitoring Configuration

File Integrity Monitoring was configured to monitor the test directory:

`E:\SOC-FIM-Test`

Real-time monitoring was enabled for this path.

File creation, modification, and deletion activities were generated to verify that FIM events were collected.

### 7.5 PowerShell Logging Configuration

PowerShell Script Block Logging was enabled through Windows policy configuration.

The PowerShell Operational event channel was configured for collection by the Wazuh agent.

PowerShell activity was generated using commands such as:

- `Get-Process`
- `Get-Service`
- `Get-LocalUser`
- `Get-NetTCPConnection`

Event ID 4104 was generated and observed through the monitoring environment.

**Security note:** Configuration files and screenshots must be reviewed before publication. Do not expose passwords, enrollment credentials, authentication keys, tokens, or other sensitive values.

## 8. Implementation and Testing

The following activities were performed to validate endpoint monitoring:

### 8.1 Authentication Monitoring

- Generated failed logon attempts.
- Generated successful logon activity.
- Examined Windows Security events 4625 and 4624.

### 8.2 Local Account Management Monitoring

- Created a local Windows test account.
- Verified Event ID 4720.
- Deleted the test account.
- Verified Event ID 4726.

### 8.3 File Integrity Monitoring

- Created test files in the monitored directory.
- Modified existing files.
- Deleted test files.
- Examined the resulting FIM events in Wazuh.

### 8.4 PowerShell Activity Collection

- Enabled PowerShell Script Block Logging.
- Configured collection of the PowerShell Operational channel.
- Executed basic PowerShell commands.
- Verified collection of Event ID 4104.

## 9. Screenshots and Supporting Evidence

Screenshots will be maintained in the `screenshots/` directory.

Evidence demonstrate:

- Wazuh server component health.
- Wazuh dashboard access.
- Windows agent connectivity.
- Windows event collection configuration.
- Failed and successful logon events.
- Local account creation and deletion events.
- File Integrity Monitoring events.
- PowerShell logging configuration and collected events.

All screenshots are genuine captures from the lab environment. Sensitive information is redacted before uploading.

## 10. Investigation Reports

Investigation reports are maintained in the `investigation-reports/` directory.

Each report includes:

- Investigation objective.
- Relevant event information.
- Event timestamps.
- Observed activity.
- Analysis and interpretation.
- Supporting evidence.
- Investigation conclusion.
- Limitations or unanswered questions.

Investigation conclusions will be added after reviewing the actual collected event data.

## 11. Challenges and Troubleshooting

This section documents technical issues encountered during implementation, including:

- Wazuh server service health and connectivity.
- VirtualBox NAT port forwarding.
- Windows agent connectivity.
- Windows audit policy configuration.
- Event channel collection.
- File Integrity Monitoring configuration.
- PowerShell event collection.

Only issues actually encountered and their verified resolutions are documented.
