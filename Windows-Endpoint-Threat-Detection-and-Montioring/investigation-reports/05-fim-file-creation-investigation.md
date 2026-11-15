# Investigation 05: FIM File Creation

## 1. Investigation Overview

| Field | Details |
|---|---|
| Detection Type | File Integrity Monitoring |
| Event | File Added |
| Endpoint | WIN11-SOC-ENDPOINT |
| Monitored File | `E:\SOC-FIM-Test\fim-test.txt` |
| Detection Mode | Realtime |
| Event Time (UTC) | 2026-11-15 09:20:53.986 |
| Wazuh Rule ID | 554 |
| Wazuh Rule Level | 5 |

## 2. Objective

Verify that Wazuh File Integrity Monitoring detects the creation of a new file in the configured monitoring directory.

## 3. Event Details

Wazuh recorded a file creation event for:

`E:\SOC-FIM-Test\fim-test.txt`

The alert identified the event as `added` and confirmed that it was detected in realtime mode.

- **File Size:** 30 bytes
- **SHA1:** `29ad36c8667ff0de4xxxx56c074406cf6e8xxxxx`
- **MD5:** `9e5159xxxx9b15d889d4e0a7e7exxxxxx`
- **SHA256:** `3fc627213ddb86xxxxx786142524da82ee82ff46a76c193ac201178b164dxxxx`

## 4. Technical Analysis

The Wazuh agent detected the creation of `fim-test.txt` inside the configured FIM directory.

Wazuh generated Rule ID 554, with the description **File added to the system**, at severity level 5.

The alert included the file's initial size and cryptographic hashes. These values provide a baseline that can be compared against subsequent file modifications.

The realtime detection mode demonstrates that Wazuh monitored the configured directory and reported the file creation without relying solely on a scheduled scan.

## 5. Conclusion

Wazuh successfully detected the creation of a new file in the monitored Windows directory.

The event confirms that File Integrity Monitoring is operational and can record newly added files along with their initial integrity information.
