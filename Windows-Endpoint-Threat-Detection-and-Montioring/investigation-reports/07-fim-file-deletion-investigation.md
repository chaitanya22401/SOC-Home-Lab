# Investigation 07: FIM File Deletion

## 1. Investigation Overview

| Field | Details |
|---|---|
| Detection Type | File Integrity Monitoring |
| Event | File Deleted |
| Endpoint | WIN11-SOC-ENDPOINT |
| Monitored File | `E:\SOC-FIM-Test\fim-test.txt` |
| Detection Mode | Realtime |
| Event Time (UTC) | 2026-11-15 09:23:48.327 |
| Wazuh Rule ID | 553 |
| Wazuh Rule Level | 7 |

## 2. Objective

Verify that Wazuh detects the deletion of files from the configured FIM monitoring directory.

## 3. Event Details

Wazuh recorded the deletion of:

`E:\SOC-FIM-Test\fim-test.txt`

- **FIM Event:** `deleted`
- **Detection Mode:** Realtime
- **Wazuh Alert:** File deleted
- **Wazuh Rule ID:** 553
- **Wazuh Rule Level:** 7

## 4. Technical Analysis

The Wazuh agent detected that `fim-test.txt` had been deleted from the monitored directory.

Wazuh generated Rule ID 553, **File deleted**, at severity level 7.

The alert was associated with MITRE ATT&CK techniques T1070.004 — File Deletion and T1485 — Data Destruction.

The deletion event followed the previously observed creation and modification events for the same file. This confirms that Wazuh recorded the file's lifecycle during the lab test.

## 5. Conclusion

Wazuh successfully detected the deletion of `fim-test.txt` in realtime.

Together, the file creation, modification, and deletion events demonstrate that the configured File Integrity Monitoring capability can detect and report these file-system changes.
