---
name: bug-bounty
description: Use whenever the user is working a bug bounty program — parsing scope/rules of engagement, planning or running recon, triaging findings, writing up a report for HackerOne/Bugcrowd/Intigriti/YesWeHack, handling program manager pushback or duplicate/N-A disputes, or asking how to structure notes for a bounty target. Trigger on mentions of "bug bounty", "program scope", "recon on [target]", "write this up for H1/Bugcrowd/Intigriti", "triage", or "dupe claim", even if the user doesn't use the words "skill" or "bounty" explicitly.
---

# Bug Bounty Workflow

Reference for running a bug bounty engagement end-to-end: program intake, recon, vulnerability classes, report writing, and triage disputes. Output should be structured so it can be pasted directly into a pwnote engagement file (see the pwnote-engagement-file skill if present) — findings map to the `findings` array, recon steps map to `docs`/`blocks`.

## 1. Program Intake

When given a program's scope page (or a pasted policy), extract into a structured note:

| Field | Notes |
|---|---|
| In-scope assets | domains, IP ranges, app names, mobile app IDs, source repos |
| Out-of-scope | explicit exclusions — always check for staging/subdomains carved out |
| Reward table | severity → payout, so you can prioritize effort against expected value |
| Special rules | rate limits, no-automated-scanning clauses, social engineering restrictions, disclosure timeline requirements |
| Safe harbor language | confirm it exists before doing anything invasive |

Always re-read scope before starting active testing — programs change scope frequently and testing out-of-scope assets voids safe harbor.

## 2. Recon Workflow

Standard funnel, in order:

1. **Asset discovery** — subdomain enumeration (passive + active), ASN/IP range expansion, cloud bucket discovery
2. **Live host probing** — resolve + HTTP probe, screenshot triage for anomalies
3. **Tech fingerprinting** — stack identification to prioritize known-CVE-prone components
4. **Content/endpoint discovery** — JS file parsing for endpoints/secrets, historical URL sources (archive snapshots), directory brute-forcing within scope/rate limits
5. **Asset triage** — rank by attack surface (auth surfaces, file upload, admin panels, API endpoints with IDs in the path) rather than testing everything uniformly

Log each recon step as a `command-output` or `host` block per target so the trail is reproducible later for the report.

## 3. Vulnerability Class Playbooks

Keep class-specific methodology in `references/` rather than inline here — load only the relevant one:

- `references/vuln-classes.md` — IDOR/BOLA, SSRF, auth/session bypass, business logic abuse, race conditions: what to check for and how to structure the finding, at a methodology level (not payload cookbooks)
- `references/report-templates.md` — per-platform report formatting differences (H1 vs Bugcrowd vs Intigriti vs YesWeHack)

## 4. Report Writing

Every report needs, regardless of platform:

- **Title** — specific and severity-signaling ("IDOR on `/api/v1/orders/{id}` allows viewing other users' orders", not "IDOR vulnerability")
- **Summary** — one paragraph, plain language, what an attacker can do
- **Steps to reproduce** — numbered, minimal, reproducible by someone with zero context
- **Impact** — concrete, tied to the program's asset (data exposure scope, account takeover chain, financial impact)
- **PoC** — request/response pairs or a short script; redact any real user data
- **Remediation** — specific enough to be actionable, not "add input validation"
- **CVSS** — vector + score if the program asks for it; be conservative, don't inflate

Use `references/report-templates.md` for the platform-specific field layout.

## 5. Triage & Dispute Handling

If a program pushes back (duplicate claim, N/A, severity downgrade):

- Ask for the duplicate report reference/timestamp before conceding — programs sometimes cite dupes that don't actually match your finding's root cause
- If severity is downgraded, restate impact in terms of the program's own asset criticality rather than re-arguing CVSS abstractly
- Keep disputes factual and low-heat; escalation to platform mediation is a last resort, not a first move

## 6. Output Mapping (pwnote)

When generating structured output for a pwnote import:

- One `finding` object per confirmed vuln (title, severity, cvssScore, cvssVector, cwe, affectedAssets, description, poc, remediation, references, status)
- Recon steps as `host`/`command-output` blocks in a `01_Recon` doc
- Exploitation chain as `code`/`http-request` blocks in a `02_Exploitation` doc
- Use a `topology` or `killchain` board if the finding involves chaining multiple assets/creds
