# Linux Adversary Simulation & Detection Engineering

## 1. Project Overview

This project aims to build a practical Linux-based Security Operations Center (SOC) detection and response environment.

The objective is to simulate controlled adversary activities against an isolated Ubuntu Linux endpoint using **Atomic Red Team**, collect relevant security telemetry, and use **Wazuh SIEM** to develop detection and event correlation rules.

The project focuses on demonstrating the defensive capabilities of a SOC Analyst, including:

- Linux security monitoring and log analysis.
- Adversary simulation using MITRE ATT&CK techniques.
- Custom SIEM detection engineering.
- Event correlation and suspicious activity identification.
- Security alert triage and investigation.
- L0/L1 SOC analyst response procedures.
- Incident remediation and validation.

Rather than simply generating security alerts, this project focuses on the complete detection-to-response lifecycle.

**Project status:** Planning and architecture finalized. Implementation and detection validation are pending.

## 2. Project Objectives

The primary objectives are:

1. Establish a Linux endpoint monitoring environment.
2. Generate controlled adversary-like activities using Atomic Red Team.
3. Collect relevant security telemetry from Ubuntu Linux.
4. Integrate endpoint telemetry with an existing Wazuh SIEM deployment.
5. Develop custom Wazuh detection rules.
6. Implement event correlation to identify suspicious activity patterns.
7. Investigate generated security alerts using an L0/L1 SOC workflow.
8. Develop practical incident response and remediation playbooks.
9. Validate detection effectiveness through controlled simulations.
10. Document the complete investigation and response process.

### Architecture Components

| Component | Responsibility |
|---|---|
| Ubuntu Server | Isolated Linux endpoint and simulation target |
| Atomic Red Team | Controlled adversary simulation |
| Wazuh Agent | Endpoint telemetry collection |
| Auditd | Linux security auditing |
| Wazuh Server | Security event analysis and detection |
| Wazuh Indexer | Security event storage and indexing |
| Wazuh Dashboard | Alert monitoring and investigation |
| MITRE ATT&CK | Adversary technique classification |

### Proposed Data Flow

1. Atomic Red Team executes selected tests against the isolated Ubuntu endpoint.
2. Linux generates relevant security events.
3. Auditd and other configured telemetry sources record endpoint activity.
4. Wazuh Agent collects configured security events.
5. Wazuh Server processes the incoming events.
6. Custom detection and correlation rules identify suspicious activity.
7. Security alerts are investigated using documented SOC playbooks.
8. Appropriate remediation actions are recommended or performed with authorization.


## 3. Adversary Simulation Scenarios

The project will cover five primary investigation scenarios.

Each scenario will follow a consistent methodology:

**Simulation → Telemetry Collection → Detection → Investigation → Response → Validation**

### 3.1 IR-001: Suspicious Shell Execution

**Objective:** Identify potentially suspicious command execution and shell activity.

Planned activities:
- Controlled shell script execution.
- Suspicious command execution patterns.
- Execution from unusual directories.

Defensive objectives:
- Monitor process execution.
- Identify suspicious command patterns.
- Investigate the executing user and process.
- Correlate relevant security events.

MITRE ATT&CK: T1059.004 – Unix Shell.

### 3.2 IR-002: SSH Authentication Attacks

**Objective:** Detect suspicious authentication activity targeting SSH services.

Planned activities:
- Controlled failed SSH authentication attempts.
- Repeated authentication failures.
- Failure-to-success authentication sequences.

Defensive objectives:
- Identify repeated authentication failures.
- Detect unusual authentication patterns.
- Identify targeted accounts and source addresses.
- Investigate potentially compromised accounts.

MITRE ATT&CK: T1110 – Brute Force.

### 3.3 IR-003: Suspicious Outbound Network Activity

**Objective:** Identify unusual outbound network connections originating from the Linux endpoint.

Planned activities:
- Controlled outbound connections to a lab listener.
- Repeated communication with designated test destinations.
- Suspicious connection patterns.

Defensive objectives:
- Monitor outbound connections.
- Identify unusual destinations and ports.
- Correlate network activity with available process telemetry.
- Recommend appropriate network containment.

MITRE ATT&CK: Techniques will be selected according to the actual simulation and observed behaviour.

### 3.4 IR-004: Suspicious Sudo and Privilege Activity

**Objective:** Detect potentially unauthorized privilege-related activities.

Planned activities:
- Sudo enumeration.
- Suspicious privileged command execution.
- Controlled sudo configuration changes where safe.

Defensive objectives:
- Monitor privileged command execution.
- Identify suspicious privilege changes.
- Investigate affected accounts.
- Recommend appropriate privilege remediation.

MITRE ATT&CK: T1548.003 – Sudo and Sudo Caching.

### 3.5 IR-005: Unauthorized File Permission Changes

**Objective:** Identify suspicious changes to Linux file permissions and ownership.

Planned activities:
- Controlled permission modifications.
- File ownership changes.
- Changes to designated test files.

Defensive objectives:
- Monitor file and permission modifications.
- Identify affected files and users.
- Correlate changes with process execution.
- Recommend restoration of approved permissions.

MITRE ATT&CK: T1222.002 – Linux and Mac File and Directory Permissions Modification.

**Important:** The exact Atomic Red Team test identifiers, prerequisites and execution procedures will be documented after validating the selected tests. Scenarios without a suitable Atomic test will use clearly identified controlled lab simulations.

## 4. Detection Engineering

A major component of this project is developing custom Wazuh detection and correlation rules.

The detection engineering process will include:

1. Identify the security event required for detection.
2. Configure the appropriate Linux telemetry source.
3. Generate controlled test activity.
4. Examine the resulting raw event.
5. Identify the actual decoded fields.
6. Develop an individual detection rule.
7. Develop correlation rules where appropriate.
8. Validate the rules using Wazuh Logtest.
9. Perform end-to-end detection validation.
10. Evaluate false positives and detection limitations.

### 4.1 Individual Event Detection

Examples of planned detection use cases:

- Repeated SSH authentication failures.
- Suspicious privileged command execution.
- Unauthorized permission changes.
- Suspicious process execution.
- Unexpected outbound network connections.

### 4.2 Event Correlation

Where supported by the available telemetry, multiple related events will be correlated to identify broader attack patterns.

Example:

**Potential SSH Compromise**

1. Repeated failed SSH authentication attempts.
2. Successful authentication from the same source.
3. Suspicious command execution.
4. Unexpected sudo activity.

The objective is to generate a higher-context security alert instead of treating every event independently.

Wazuh correlation capabilities will be used according to the actual available event fields and rule dependencies.

## 5. Incident Response Playbooks

A dedicated SOC playbook will be developed for each investigation scenario.

Each playbook will include:

- Alert description.
- Detection rule reference.
- Initial triage checklist.
- Investigation procedure.
- Relevant Linux commands and log sources.
- Indicators of compromise, where applicable.
- MITRE ATT&CK mapping.
- Severity assessment.
- False-positive considerations.
- Containment recommendations.
- Remediation procedure.
- Verification steps.
- Escalation criteria.

Planned playbooks:

| Playbook | Scenario |
|---|---|
| SOC-PLAYBOOK-001 | Suspicious Shell Execution |
| SOC-PLAYBOOK-002 | SSH Authentication Attacks |
| SOC-PLAYBOOK-003 | Suspicious Network Activity |
| SOC-PLAYBOOK-004 | Sudo and Privilege Activity |
| SOC-PLAYBOOK-005 | File Permission Modifications |

## 6. Validation Methodology

Every detection use case undergoes practical validation.

Validation will include:

- Confirming the expected endpoint telemetry is generated.
- Confirming the events reach Wazuh.
- Testing individual detection rules.
- Testing correlation conditions.
- Verifying alert contents.
- Evaluating false positives.
- Confirming remediation effectiveness where applicable.
- Recording detection limitations.
