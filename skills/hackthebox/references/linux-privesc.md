# Linux Privilege Escalation — Enumeration Categories

Categories of things to check, not specific exploit commands. This is standard, widely-taught methodology (matches OSCP/PEN-200 curriculum) for orienting enumeration, not a technique cookbook.

## Kernel & OS
- Kernel version and known exploit applicability for that specific version
- Distribution and patch level

## Credentials & Secrets
- World-readable config files containing credentials (app configs, `.env` files, backup files)
- Shell history files for leaked commands/passwords
- SSH keys with overly permissive access left in unexpected locations
- Password reuse between discovered service credentials and system accounts

## SUID / SGID / Capabilities
- Binaries with SUID/SGID bits set that aren't part of the standard OS baseline
- Linux capabilities set on binaries that grant more than intended
- Whether any such binary is known to have a documented privilege-escalation use case for its specific version

## Sudo Misconfiguration
- What the current user can run via sudo (`sudo -l`) and whether any entry is broader than intended
- Whether any sudo-permitted binary is known to allow escaping to a shell or file read/write outside its intended scope

## Scheduled Tasks
- Cron jobs, systemd timers, or other scheduled tasks running as a higher-privileged user
- Whether the script/binary they invoke is writable by the current user, or invoked via a relative/unqualified path (PATH hijack potential)

## Writable System Paths
- World-writable directories in `PATH`
- Writable service unit files, writable binaries invoked by privileged processes

## Container / Namespace Context
- Whether the current shell is inside a container, and what escape surface exists (privileged mode, mounted host paths, exposed sockets)

## Process & Network
- Processes running as root that the current user can interact with or influence
- Locally-bound services not reachable externally but reachable now that there's local access

## General Approach
Run one of the well-known automated enumeration scripts to surface candidates quickly, then manually verify each candidate rather than acting on automated output blindly — automated tools produce false positives, especially around "possible" kernel exploits.
