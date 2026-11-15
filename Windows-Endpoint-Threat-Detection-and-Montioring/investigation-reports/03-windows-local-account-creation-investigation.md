# Investigation 03: Windows Local Account Creation

## 1. Investigation Overview

| Field | Details |
|---|---|
| Event ID | 4720 |
| Event Description | A user account was created |
| Endpoint | Host-001-Laptop |
| Wazuh Agent | WIN11-SOC-ENDPOINT |
| Account Created | SOC-TestUser |
| Created By | Host-001 |
| Event Time (UTC) | 2026-11-15 08:59:01.093 |
| Wazuh Rule ID | 60109 |
| Wazuh Rule Level | 8 |

## 2. Objective

Investigate Windows Event ID 4720 to verify local user account creation and examine the configuration of the newly created account.

## 3. Event Details

Windows Security Event ID 4720 recorded the creation of the local account `SOC-TestUser`.

- **Initiating Account:** Host-001
- **Target Account:** SOC-TestUser
- **Target SID:** S-1-5-21-2882432209-247939120-2058478334-1008
- **Primary Group ID:** 513
- **Wazuh Alert:** User account enabled or created
- **Wazuh Rule ID:** 60109
- **Wazuh Rule Level:** 8

## 4. Technical Analysis

The event confirms that the account `SOC-TestUser` was created on the monitored Windows endpoint.

The account's `userAccountControl` value was recorded as `0x15`. The event details indicate the following flags:

- Account Disabled
- Password Not Required — Enabled
- Normal Account — Enabled

The password was never set at the time of the event.

Although the account creation was successfully detected, the account was recorded as disabled. The Password Not Required flag is a security-relevant configuration that should be reviewed if encountered on an account outside a controlled lab exercise.

Wazuh generated Rule ID 60109 at level 8 and associated the alert with MITRE ATT&CK technique T1098 — Account Manipulation.

## 5. Conclusion

Wazuh successfully detected the creation of the local test account through Windows Event ID 4720.

The event confirms account creation and records its initial configuration. The account was disabled, with the Password Not Required flag enabled and no password set.

The activity was part of the controlled lab testing.
