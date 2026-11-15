# Investigation 04: Windows Local Account Deletion

## 1. Investigation Overview

| Field | Details |
|---|---|
| Event ID | 4726 |
| Event Description | A user account was deleted |
| Endpoint | Host-001-Laptop |
| Wazuh Agent | WIN11-SOC-ENDPOINT |
| Account Deleted | SOC-TestUser |
| Deleted By | Host-001 |
| Event Time (UTC) | 2026-11-15 09:03:41.894 |
| Wazuh Rule ID | 60111 |
| Wazuh Rule Level | 8 |

## 2. Objective

Investigate Windows Event ID 4726 to verify local user account deletion and identify the account and user responsible for the action.

## 3. Event Details

Windows Security Event ID 4726 recorded the deletion of the local account `SOC-TestUser`.

- **Initiating Account:** Host-001
- **Deleted Account:** SOC-TestUser
- **Target SID:** S-1-5-21-2882432209-247939120-2058478334-1008
- **Wazuh Alert:** User account disabled or deleted
- **Wazuh Rule ID:** 60111
- **Wazuh Rule Level:** 8

## 4. Technical Analysis

The event confirms that the local account `SOC-TestUser` was deleted from the monitored Windows endpoint.

The target SID matches the SID recorded in Investigation 03, which documented the creation of this account through Event ID 4720.

The deletion occurred approximately 4 minutes and 41 seconds after the account creation event. This establishes that the same test account was created and subsequently deleted during the lab exercise.

Wazuh generated Rule ID 60111 at level 8. Its associated MITRE ATT&CK mappings include T1098 — Account Manipulation and T1531 — Account Access Removal.

## 5. Conclusion

Wazuh successfully detected the deletion of the local test account through Windows Event ID 4726.

Correlation with Event ID 4720 confirms that `SOC-TestUser` was the same account created earlier during the controlled lab exercise. The account lifecycle activity was successfully captured and monitored by Wazuh.
