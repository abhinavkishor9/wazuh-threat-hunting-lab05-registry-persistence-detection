# wazuh-threat-hunting-lab05-registry-persistence-detection
## Overview

This lab demonstrates how Windows Registry Run Keys can be used for persistence and how Sysmon together with Wazuh detects registry modifications associated with this technique.

The objective was to simulate Registry Run Key persistence, verify Sysmon logging, investigate the event in Wazuh Threat Hunting, and clean up the registry entry after validation.

---

## Lab Objectives

- Verify Sysmon service
- Verify Wazuh agent
- Create a Registry Run Key
- Confirm Sysmon Event ID 13 generation
- Detect the event in Wazuh Threat Hunting
- Review registry modification details
- Remove the registry entry

---

## Environment

- Windows 11
- Sysmon
- Wazuh Agent
- Wazuh Manager
- Wazuh Dashboard

---

## Attack Technique

MITRE ATT&CK

**T1547.001 — Registry Run Keys / Startup Folder**

Adversaries use Registry Run Keys to automatically launch malicious programs whenever a user logs on.

---

## Detection Workflow

1. Verify Sysmon is running.
2. Verify Wazuh Agent is connected.
3. Create a Registry Run Key.
4. Sysmon logs Event ID 13.
5. Wazuh receives the event.
6. Investigate the event inside Threat Hunting.
7. Validate registry values.
8. Remove the persistence mechanism.

---

## Commands Used

Verify Sysmon

```powershell
Get-Service Sysmon64
```

Verify Wazuh

```powershell
Get-Service WazuhSvc
```

Create Registry Run Key

```cmd
reg add HKCU\Software\Microsoft\Windows\CurrentVersion\Run /v WazuhLab /t REG_SZ /d "notepad.exe" /f
```

Verify Registry Key

```cmd
reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Run
```

Check Sysmon Event ID 13

```powershell
Get-WinEvent -LogName "Microsoft-Windows-Sysmon/Operational" -FilterXPath "*[System[(EventID=13)]]" -MaxEvents 20
```

Cleanup

```cmd
reg delete HKCU\Software\Microsoft\Windows\CurrentVersion\Run /v WazuhLab /f
```

---

## Detection Results

- Registry Run Key successfully created
- Sysmon generated Event ID 13
- Wazuh successfully ingested the event
- Rule mapped to Registry Run Key persistence
- Registry modification visible in Threat Hunting
- Persistence removed successfully

---

## Skills Practiced

- Windows Registry Analysis
- Persistence Detection
- Sysmon Event Analysis
- Wazuh Threat Hunting
- IOC Investigation
- MITRE ATT&CK Mapping
- Registry Forensics

---

## MITRE ATT&CK Mapping

| Technique | Description |
|------------|-------------|
| T1547.001 | Registry Run Keys / Startup Folder |

---

## Outcome

Successfully simulated Registry Run Key persistence and validated end-to-end detection using Sysmon and Wazuh.
