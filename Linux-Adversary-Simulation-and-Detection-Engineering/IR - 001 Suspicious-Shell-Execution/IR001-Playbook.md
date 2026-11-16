# IR-001 — Suspicious Shell Execution

**Playbook ID:** IR-001  
**Log Source:** Linux Auditd  
**Detection Rule:** 100100  
**Severity:** Medium — Level 5  
**MITRE ATT&CK:** T1059.004 — Unix Shell  
**Status:** Detection validated in a controlled lab

---

## 1. Alert Overview

This playbook covers the investigation of suspicious shell execution detected through Linux Auditd telemetry and a custom Wazuh detection rule.

The detection identifies matching `execve` system calls recorded by Auditd with the lab-specific key `ir001_exec_test`.

**Wazuh alert description:**

`IR-001: Interactive shell process execution detected`

**Detection conditions:**
- Auditd event grouping rule: `80700`
- Event type: `SYSCALL`
- Audit key: `ir001_exec_test`
- TTY: `pts0`
- System call: `59` (`execve`)

The rule is designed for controlled interactive shell execution in this lab. It is not a general-purpose detection for every suspicious shell process.

## 2. Objective

Enable a SOC analyst to:

1. Validate the suspicious shell execution alert.
2. Identify the executed command and binary.
3. Establish the user and session context.
4. Investigate parent-child process relationships.
5. Determine whether the activity is authorized.
6. Recommend containment and remediation.
7. Verify that the activity has stopped.

## 3. MITRE ATT&CK Mapping

| Attribute | Value |
|---|---|
| Tactic | Execution |
| Technique | T1059 |
| Sub-technique | T1059.004 |
| Name | Unix Shell |

Shells such as Bash, Dash, and other Unix command interpreters can execute commands and scripts. Adversaries may abuse them to execute commands on compromised Linux systems.

## 4. Relevant Alert Fields

| Field | Investigation purpose |
|---|---|
| `rule.id` | Identify the Wazuh detection rule |
| `rule.level` | Understand alert severity |
| `rule.description` | Understand why the alert fired |
| `data.audit.command` | Identify the executed command |
| `data.audit.exe` | Identify the executable path |
| `data.audit.auid` | Identify the original authenticated user |
| `data.audit.uid` | Identify the effective audit user identity |
| `data.audit.pid` | Identify the process |
| `data.audit.ppid` | Identify the parent process |
| `data.audit.tty` | Identify the associated terminal |
| `data.audit.cwd` | Identify the working directory |
| `data.audit.syscall` | Identify the system call |
| `data.audit.success` | Determine whether execution succeeded |
| `data.audit.key` | Identify the Auditd rule key |
| `full_log` | Review the original audit event |

## 5. L1 — Initial Triage

### Step 1: Validate the alert

Open Wazuh Dashboard → Threat Hunting.

Search:

`rule.id: 100100`

Confirm:
- Rule ID is 100100.
- Alert level is 5.
- Description matches IR-001.
- Audit key is `ir001_exec_test`.
- Event type is `SYSCALL`.
- TTY is `pts0`.

### Step 2: Identify the process

Review:
- Executable path.
- Command name.
- PID and PPID.
- User identity.
- Working directory.
- Execution timestamp.

### Step 3: Assess the activity

Determine:
- Is the command expected?
- Is the user authorized to execute it?
- Is the executable located in a legitimate directory?
- Is the working directory expected?
- Is the parent process legitimate?
- Does the activity correlate with other suspicious events?

**L1 decision:**

Escalate to L2 if the execution is unauthorized, unexplained, associated with suspicious parent processes, or accompanied by other indicators of compromise.

Do not classify activity as malicious based only on the shell executable name.

## 6. Indicators to Investigate

Potentially suspicious observations include:

- Unexpected shell execution by a service account.
- Shell processes launched by unusual parent processes.
- Execution from temporary or writeable directories.
- Unexpected privilege changes.
- Commands executed outside normal administrative activity.
- Shell execution associated with suspicious authentication events.

These are investigation indicators, not proof of compromise.

## 7. False-Positive Considerations

Legitimate activities may trigger shell execution telemetry:

- System maintenance scripts.
- Package installation and updates.
- Administrative automation.
- Monitoring and backup scripts.
- Scheduled tasks.
- Service startup scripts.

The lab's TTY condition (`pts0`) excludes events with no terminal, such as the observed `bcache-export-c` event with `tty=(none)`.

**Detection limitation:** TTY filtering is session-specific. It can miss suspicious shell executions through SSH, non-interactive sessions, scripts, and other terminal sessions.

The Auditd key `ir001_exec_test` is also specific to the temporary lab rules. This detection should not be represented as comprehensive Linux shell monitoring.

## 8. Containment

If malicious activity is reasonably suspected:

1. Escalate according to organizational incident-response procedures.
2. Preserve relevant Wazuh alerts and Auditd logs.
3. Identify affected accounts and processes.
4. Coordinate host isolation with the incident-response team.
5. Terminate confirmed malicious processes only after considering evidence preservation and operational impact.
6. Disable or restrict compromised accounts when authorized.
7. Preserve relevant files and timestamps for further investigation.

Do not indiscriminately terminate system processes or disable accounts based only on this alert.

## 9. Remediation

Depending on investigation findings:

- Remove unauthorized scripts or persistence mechanisms.
- Correct excessive permissions.
- Rotate compromised credentials.
- Restrict unnecessary shell access.
- Patch affected software.
- Review privileged access.
- Improve Auditd coverage.
- Tune Wazuh detection logic to reduce false positives without excluding important attack paths.

## 10. Post-Remediation Verification

Confirm:

- The suspicious process is no longer running.
- Unauthorized execution paths have been removed.
- Affected credentials have been secured.
- Relevant Auditd telemetry is being collected.
- Wazuh is ingesting the required events.
- Detection rules continue to work.
- No related suspicious activity remains unexplained.

Record the verification evidence and any remaining risks.


## 11. Lab Validation Evidence

The controlled lab simulation used the documented Atomic Red Team T1059.004 test command, executed manually:

```bash
sh -c 'for i in $(seq 1 5); do echo "$i, Atomic Red Team was here!"; sleep 1; done'
```

Observed Wazuh alert:

| Attribute | Observed value |
|---|---|
| Rule ID | 100100 |
| Rule level | 5 |
| Description | IR-001: Interactive shell process execution detected |
| Decoder | auditd |
| Executable | `/usr/bin/sleep` |
| Command | `sleep` |
| System call | 59 |
| TTY | `pts0` |
| Audit key | `ir001_exec_test` |
| Working directory | `/home/linux001/AtomicRedTeam` |
| Audit UID | 1000 |
| Audit AUID | 1000 |

The custom Wazuh rule successfully generated a live alert from the simulation.

A negative Logtest case using `bcache-export-c` with `tty=(none)` matched only rule 80700, level 0, rather than the custom rule 100100.

**Validation scope:** This confirms the configured lab detection and the tested negative case. It does not establish detection coverage for all Unix shell execution techniques.
