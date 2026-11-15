# Investigation 06: FIM File Modification

## 1. Investigation Overview

| Field | Details |
|---|---|
| Detection Type | File Integrity Monitoring |
| Event | File Modified |
| Endpoint | WIN11-SOC-ENDPOINT |
| Monitored File | `E:\SOC-FIM-Test\fim-test.txt` |
| Detection Mode | Realtime |
| Event Time (UTC) | 2026-11-15 09:22:34.572 |
| Wazuh Rule ID | 550 |
| Wazuh Rule Level | 7 |

## 2. Objective

Verify that Wazuh detects modifications to files in the configured FIM monitoring directory and records changes to their integrity attributes.

## 3. Event Details

Wazuh detected a modification to:

`E:\SOC-FIM-Test\fim-test.txt`

The file size changed from **30 bytes to 75 bytes**.

The following attributes were reported as changed:

- File size
- Modification time
- MD5 hash
- SHA1 hash
- SHA256 hash

**Previous hashes:**

| Algorithm | Hash |
|---|---|
| MD5 | `9e515xxxx15d889d4e0a7e7ea64787` |
| SHA1 | `29ad3xxxx67ff0de445756c0xxxxxcf6e89cd013` |
| SHA256 | `3fc627213ddb86bfb5786xxxxda82ee82ff46a76c193ac201178b164d19dad` |

**New hashes:**

| Algorithm | Hash |
|---|---|
| MD5 | `dcc2b00b033b4bffe8a3xxxd6221b1ea` |
| SHA1 | `9b776dxxxx4b4ba5114ca673546056c4a7b4cb75e` |
| SHA256 | `24cc4a700ac91de3a4a03bc7de3a43ad2f8xxxxxxea9d943bdcbaac7df960c25` |

## 4. Technical Analysis

The Wazuh agent detected changes to the monitored file in realtime mode.

Wazuh generated Rule ID 550, **Integrity checksum changed**, at severity level 7.

The change in file size and all three cryptographic hashes confirms that the file's contents or metadata changed between observations. The alert was associated with MITRE ATT&CK technique T1565.001 — Stored Data Manipulation.

The alert establishes that a modification occurred, but does not identify the process or user responsible for making the change.

## 5. Conclusion

Wazuh successfully detected the modification of `fim-test.txt` and recorded the before-and-after integrity values.

This validates the FIM capability to identify file changes and provide hash information that can support further investigation.
