# Investigation 01: Windows Failed Logon

## 1. Investigation Overview

| Attribute | Value |
|---|---|
| Investigation ID | INV-001 |
| Endpoint | WIN11-SOC-ENDPOINT |
| Agent ID | 001 |
| Windows Event ID | 4625 |
| Wazuh Rule ID | 60122 |
| Wazuh Alert Level | 5 |
| Event Channel | Security |
| Account | Host001 |
| Investigation Status | Inconclusive |

## 2. Investigation Objective

The objective of this investigation is to examine a failed Windows authentication event collected by Wazuh and identify the account involved, authentication failure reason, logon type, source address, and associated process information.

## 3. Event Details

| Field | Observed Value |
|---|---|
| Event ID | 4625 |
| Event Timestamp (UTC) | 2026-11-15 09:29:21.753 |
| Wazuh Alert Timestamp (UTC) | 2026-11-15 09:29:22.958 |
| Computer | Host001-Laptop |
| Target Username | Host001 |
| Target Domain | Host001-LAPTOP |
| Logon Type | 2 |
| Status | 0xc000006d |
| SubStatus | 0xc000006a |
| Failure Reason | Unknown user name or bad password |
| Source Address | ::1 |
| Source Port | 0 |
| Process Name | C:\Windows\System32\svchost.exe |
| Logon Process | seclogo |
| Authentication Package | Negotiate |

## 4. Wazuh Detection Details

| Field | Value |
|---|---|
| Wazuh Rule ID | 60122 |
| Rule Description | Logon Failure - Unknown user or bad password |
| Rule Level | 5 |
| Rule Groups | windows, windows_security, authentication_failed |
| Decoder | windows_eventchannel |
| Location | EventChannel |

Wazuh successfully processed the Windows Security event and generated an authentication failure alert.

## 5. Technical Analysis

### Authentication Failure

The Windows event recorded an unsuccessful authentication attempt against the local account Host001.

The general status was 0xc000006d, while the sub-status was 0xc000006a.

The sub-status indicates an incorrect password.

### Logon Type

The event recorded Logon Type 2, representing an interactive logon.

### Source Address

The source address was ::1, which is the IPv6 loopback address.

This indicates a local source address rather than an identified external network source.

### Process Information

The event recorded C:\Windows\System32\svchost.exe as the associated process and seclogo as the logon process.

The available evidence does not establish malicious process activity.

## 6. Security Assessment

The event confirms a failed interactive authentication attempt caused by an incorrect password.

Although repeated failed authentication attempts can indicate password guessing or brute-force activity, this individual event does not establish such an attack.

The source address was the local IPv6 loopback address, and no external source was identified in this event.

## 7. Recommended Investigation Actions

1. Search for additional Event ID 4625 records involving the same account.
2. Correlate failed authentication events with successful Event ID 4624 records.
3. Examine the timestamps and frequency of authentication failures.
4. Review the logon type and source address of related events.
5. Determine whether the activity corresponds to expected local user activity.

## 8. Investigation Conclusion

Wazuh successfully collected and generated an alert for Windows Security Event ID 4625.

The event indicates an unsuccessful interactive authentication attempt against the local account Host001, with an incorrect-password sub-status.

The source address was ::1, indicating a local loopback address.

Based on the available event evidence, the activity is classified as an observed authentication failure with an inconclusive security assessment. 

## 9. Supporting Evidence

- Wazuh alert: Event ID 4625
- Wazuh Rule ID: 60122
- Endpoint: WIN11-SOC-ENDPOINT
