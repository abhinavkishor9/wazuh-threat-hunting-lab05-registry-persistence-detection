# Troubleshooting Notes

## Issue 1

No Event ID 13 generated.

### Resolution

Verify Sysmon configuration includes Registry Event monitoring.

---

## Issue 2

Registry key created but no Wazuh alert.

### Resolution

- Verify Wazuh Agent service
- Confirm agent connectivity
- Wait briefly for log ingestion
- Refresh Threat Hunting

---

## Issue 3

Threat Hunting returns no results.

### Resolution

- Increase time range
- Refresh index
- Verify search query
- Confirm correct agent selected

---

## Issue 4

Registry key not found.

### Resolution

Verify the registry path:

HKCU\Software\Microsoft\Windows\CurrentVersion\Run

Confirm the command executed successfully.

---

## Issue 5

Sysmon service stopped.

### Resolution

```powershell
Get-Service Sysmon64
```

Start if required:

```powershell
Start-Service Sysmon64
```

---

## Issue 6

Wazuh Agent stopped.

### Resolution

```powershell
Get-Service WazuhSvc
```

Start if necessary:

```powershell
Start-Service WazuhSvc
```

---

## Issue 7

Cleanup failed.

### Resolution

Remove the registry entry manually:

```cmd
reg delete HKCU\Software\Microsoft\Windows\CurrentVersion\Run /v WazuhLab /f
```

Verify removal:

```cmd
reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Run
```

---

## Lessons Learned

- Registry Run Keys are a common persistence mechanism.
- Sysmon Event ID 13 provides detailed registry modification telemetry.
- Wazuh can detect and classify Registry persistence activity.
- Reviewing registry details helps distinguish legitimate from suspicious modifications.
- Always remove persistence artifacts after testing.
