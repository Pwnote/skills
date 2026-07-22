# Windows Privilege Escalation — Enumeration Categories

Categories of things to check, not specific exploit commands. Standard OSCP/PEN-200-aligned methodology for orienting enumeration.

## OS & Patch Level
- Windows version/build and patch level, for known local-exploit applicability to that specific build

## Credentials & Secrets
- Saved credentials in config files, scripts, scheduled task definitions, unattended install files
- Registry locations known to sometimes store plaintext or reversible credentials
- Credential Manager entries accessible to the current user

## Service Misconfiguration
- Services running as SYSTEM/high-privilege where the service binary path is writable by the current user
- Unquoted service paths that could be hijacked
- Services where the current user has permission to reconfigure the service (change binary path, start type)

## Scheduled Tasks
- Tasks running as a higher-privileged account where the invoked script/binary is writable

## Token & Privilege Abuse
- Whether the current user's token holds privileges (e.g., impersonation-capable privileges) that are known to allow escalation when present, and whether tooling exists to leverage that specific privilege

## Registry & AlwaysInstallElevated
- Whether AlwaysInstallElevated policy is set, allowing arbitrary-privilege package installation
- Autorun/autologon entries containing credentials

## File System Permissions
- Writable directories or files owned by/used by privileged processes
- Weak ACLs on binaries or DLLs loaded by privileged services (DLL hijack surface)

## Domain Context (if applicable)
- Current user's group memberships and any nested group paths toward privileged AD groups
- Kerberoastable/AS-REP-roastable accounts if in a domain-joined context

## General Approach
Run a standard enumeration script (e.g. one of the well-known PowerShell/CMD enum scripts) to surface candidates, then manually verify each one — many "findings" from automated tools are informational rather than exploitable in the specific box's context.
