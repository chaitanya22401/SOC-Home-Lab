# Investigation 02: Windows Successful Logon

## 1. Investigation Overview

| Attribute | Value |
|---|---|
| Investigation ID | INV-002 |
| Endpoint | WIN11-SOC-ENDPOINT |
| Agent ID | 001 |
| Windows Event ID | 4624 |
| Wazuh Rule ID | 60118 |
| Wazuh Alert Level | 3 |
| Event Channel | Security |
| Account | Host-001 |
| Investigation Status | Successful authentication observed |

## 2. Investigation Objective

The objective of this investigation is to examine a successful Windows authentication event collected by Wazuh.

The investigation identifies the authenticated account, logon type, source address, authentication package, associated process, and relevant event information.

It also examines the relationship between this successful authentication event and the failed authentication event documented in Investigation 01.

## 3. Event Details

| Field | Observed Value |
|---|---|
| Event ID | 4624 |
| Event Timestamp (UTC) | 2026-11-15 09:29:01.336 |
| Wazuh Alert Timestamp (UTC) | 2026-11-15 09:29:02.540 |
| Computer | Host-001-Laptop |
| Account Name | Host-001 |
| Account Domain | Host-001-LAPTO |
| Logon Type | 2 |
| Source Address | ::1 |
| Source Port | 0 |
| Process ID | 0x2d14 |
| Process Name | C:\Windows\System32\svchost.exe |
| Logon Process | seclogo |
| Authentication Package | Negotiate |
| Event Severity | AUDIT_SUCCESS |

## 4. Wazuh Detection Details

| Field | Value |
|---|---|
| Wazuh Rule ID | 60118 |
| Rule Description | Windows Workstation Logon Success |
| Rule Level | 3 |
| Rule Groups | windows, windows_security, authentication_success |
| Decoder | windows_eventchannel |
| Location | EventChannel |
| MITRE ATT&CK Technique | T1078 - Valid Accounts |

Wazuh successfully processed the Windows Security event and generated a successful authentication alert.

## 5. Technical Analysis

### 5.1 Authentication Result

Windows Event ID 4624 indicates that a logon session was successfully created.

The event records the account Host-001 as the authenticated user.

### 5.2 Logon Type

The event recorded Logon Type 2, representing an interactive logon.

This is consistent with a local interactive authentication event rather than a remote network logon.

### 5.3 Source Address

The source address was ::1, which represents the IPv6 loopback address.

The event therefore does not identify an external source IP address.

### 5.4 Authentication Information

The authentication package was Negotiate, and the logon process was seclogo.

The associated process was:

C:\Windows\System32\svchost.exe

The available event data does not indicate malicious activity by this process.

## 6. Correlation with Investigation 01

The successful authentication event occurred at:

2026-11-15 09:29:01.336 UTC

The failed authentication event documented in Investigation 01 occurred at:

2026-11-15 09:29:21.753 UTC

Both records involve:

- Endpoint: WIN11-SOC-ENDPOINT
- Account: Host-001
- Logon Type: 2
- Source Address: ::1
- Associated Process: svchost.exe
- Logon Process: seclogo

The successful authentication preceded the failed authentication by approximately 20 seconds.

This establishes a temporal relationship between the two events. It does not establish that they were part of the same authentication session or that the later failed attempt was malicious.

## 7. Security Assessment

The event confirms that the local account Host-001 successfully authenticated through an interactive logon.

The event was collected and classified by Wazuh under the successful authentication rule.

Successful authentication is not inherently suspicious. However, SOC analysts should examine successful logons in context, especially when correlated with failed authentication attempts, unusual account activity, unexpected logon times, or abnormal source addresses.

Based on the available evidence, the event is consistent with a successful local interactive authentication.

## 8. Recommended Investigation Actions

1. Correlate the event with nearby failed authentication events.
2. Review additional successful and failed logons involving the same account.
3. Examine the event timestamps and logon types.
4. Investigate any unexpected authentication patterns.
5. Correlate authentication activity with account management and endpoint activity where relevant.

## 9. Investigation Conclusion

Wazuh successfully collected Windows Security Event ID 4624 and generated an alert using Rule ID 60118.

The event confirms a successful interactive authentication involving the local account Host-001 on WIN11-SOC-ENDPOINT.

The source address was ::1, indicating an IPv6 loopback address.

Correlation with Investigation 01 shows a failed authentication event involving the same account and endpoint approximately 20 seconds later.

The available evidence does not establish malicious authentication activity or endpoint compromise.



Additional authentication records and endpoint telemetry would be required to establish a broader activity pattern or determine whether the events were associated with suspicious behavior.
