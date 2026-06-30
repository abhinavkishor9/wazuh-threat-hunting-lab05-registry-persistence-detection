# Investigation Notes

## Scenario

A Registry Run Key was intentionally created to simulate a persistence technique commonly used by attackers.

The objective was to determine whether Sysmon and Wazuh successfully detected the registry modification.

---

## Initial Checks

Verified:

- Sysmon service running
- Wazuh Agent running

---

## Activity Performed

Created the following Registry Run Key:

HKCU\Software\Microsoft\Windows\CurrentVersion\Run

Value Name:

WazuhLab

Value Data:

notepad.exe

---

## Detection

Sysmon generated:

Event ID 13

Registry Value Set

---

## Wazuh Findings

Threat Hunting detected:

- Registry entry modified
- Registry persistence technique identified
- Registry path
- Modified value
- Process responsible for modification

---

## Evidence Collected

- Registry key creation
- Sysmon Event ID 13
- Wazuh detection
- Event details
- Registry verification
- Registry cleanup

---

## MITRE ATT&CK

Technique

T1547.001

Registry Run Keys / Startup Folder

---

## Indicators Observed

Registry Path

HKCU\Software\Microsoft\Windows\CurrentVersion\Run

Value Name

WazuhLab

Value Data

notepad.exe

Process

reg.exe

Event

Sysmon Event ID 13

---

## Severity

Medium

Registry Run Keys are a common persistence mechanism frequently used by malware.

---

## Conclusion

The persistence mechanism was successfully detected by Sysmon and forwarded to Wazuh.

The registry entry was reviewed, validated, and removed after investigation.
