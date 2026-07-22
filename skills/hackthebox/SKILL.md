---
name: hackthebox
description: Use whenever the user is working a HackTheBox (HTB) machine or challenge — structuring recon/foothold/privesc notes, building an enumeration checklist, tracking a multi-hop attack path, or writing a writeup (respecting HTB's retirement rules before publishing). Trigger on "HTB", "HackTheBox box", "pwn this machine", or "root this box", even without the word "skill".
---

# HackTheBox Workflow

Reference for structuring notes on an HTB machine from initial recon through root, and for producing writeups once the box is eligible for public writeups.

## 1. Machine Note Structure

One pwnote doc per phase:

```
01_Recon           — port scan, service enum, initial findings
02_Foothold        — initial access vector and how it was gained
03_PrivEsc         — privilege escalation path
04_Flags           — user.txt / root.txt with timestamps
```

For multi-target/Pro Labs-style engagements, add a `00_Network_Overview` doc and use a `topology` board to track hosts and pivot paths.

## 2. Enumeration Checklist

Standard checklist block to run against every new box before diving into a specific service:

```json
{
  "title": "Initial Enumeration",
  "items": [
    { "text": "Full TCP port scan (all 65535)", "done": false },
    { "text": "Service/version detection on open ports", "done": false },
    { "text": "UDP scan of common ports", "done": false },
    { "text": "Web: directory/vhost enumeration if HTTP(S) present", "done": false },
    { "text": "Web: identify tech stack/CMS/framework", "done": false },
    { "text": "SMB/NFS/FTP: check for anonymous/guest access", "done": false },
    { "text": "Check for default/weak credentials on any discovered service", "done": false },
    { "text": "Note OS fingerprint for privesc reference selection", "done": false }
  ]
}
```

## 3. Privilege Escalation Reference

Keep OS-specific privesc *categories* in reference files rather than inline — load the relevant one once you know the target OS:

- `references/linux-privesc.md` — enumeration categories for Linux privesc
- `references/windows-privesc.md` — enumeration categories for Windows privesc

These are checklists of *what to look for*, not exploit code — the actual technique/command should come from your own tooling/notes at execution time.

## 4. Writeup vs Private Note Distinction

**Before generating a public-facing writeup, confirm the box is retired.** HTB's terms prohibit publishing writeups (including spoilers/flags) for active machines. If the user asks for a writeup and hasn't confirmed retirement status, ask before producing public-facing content — private working notes are fine regardless of retirement status.

Public writeup structure once eligible:

```
# HTB: [Machine Name] ([Difficulty])

## Recon
[methodology, not just raw scan output]

## Foothold
[vulnerability class + how it was identified and exploited, explained]

## Privilege Escalation
[misconfiguration/technique class explained]

## Flags
[redact actual flag values]
```

## 5. Attack-Path Board

For boxes with a non-linear path (multiple services chained, credential reuse across hosts), use a `killchain` or `topology` board with nodes for each host/credential/finding and edges labeled by relationship (`"credential"`, `"pivot"`, `"exploits"`) — matches the pwnote board schema directly.
