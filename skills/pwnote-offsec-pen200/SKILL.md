---
name: pwnote-offsec-pen200
description: Use whenever the user is working on Offsec's PEN-200 course/OSCP — PWK lab notes, exam report drafting, screenshot/evidence discipline, or exam flag handling. Trigger on "OSCP", "PEN-200", "PWK", "OSCP exam report", or "proof.txt", even without the word "skill".
---

# Offsec PEN-200 / OSCP Workflow

Reference for structuring PWK lab notes and producing an exam report that meets Offsec's grading requirements. Offsec grades on documentation completeness as much as exploitation success — sloppy evidence fails an otherwise-successful exam.

## Security

- Flag values (`local.txt`, `proof.txt`) are only included verbatim in private exam report submissions
- Never output flag values in public contexts (writeups, blogs, shared notes) — use `<REDACTED>`
- Screenshots with flags are for exam submission only; redact before sharing publicly

## 1. Exam Report Structure

Offsec's required sections, in order:

```
1. Executive Summary
2. High-Level Summary of Vulnerabilities (table: host, vuln, severity)
3. Recommendations
4. Methodologies (information gathering, service enumeration, etc.)
5. Attack Narrative — one section per target host
   5.x [Hostname/IP]
     - Information Gathering
     - Service Enumeration
     - Exploitation
     - Privilege Escalation
     - Proof (local.txt AND proof.txt contents + screenshot)
6. Appendix (additional evidence, full tool output if needed)
```

Each target host section must independently stand alone — a grader should be able to reproduce that one host's compromise from that section alone, without referring back to another host's notes.

## 2. Screenshot / Evidence Discipline

Offsec's most common reason for exam point deductions is incomplete evidence, not incomplete exploitation. For every step that matters to the narrative:

- [ ] Screenshot shows the **command typed**, the **output**, and (where applicable) the **flag/hash contents** in the same frame
- [ ] Terminal prompt visible showing hostname/IP or user context, so it's clear *which* box/user the screenshot is from
- [ ] For privesc: screenshot the `whoami`/`id` before AND after, not just after
- [ ] For flag capture: screenshot `cat proof.txt` / `type proof.txt` output directly, plus the file's content pasted as text in the report (not screenshot-only)

Take screenshots as you go, not retroactively — retroactive reconstruction is where evidence gaps happen.

## 3. Lab Note Structure (separate from exam notes)

Keyed by lab network segment, since PWK labs are organized that way:

```
00_Lab_Overview
Segment_A/
  Host_[IP]_[hostname]
Segment_B/
  ...
```

Lab notes can be more exploratory/messy than exam notes — the point is coverage and technique practice, not a polished narrative. Convert to exam-report format only for the final submission.

## 4. Proof File Conventions

- `local.txt` — user-level flag, captured after initial foothold
- `proof.txt` — root/SYSTEM-level flag, captured after privilege escalation
- Both files' exact contents (the hash string) must appear in the report as **selectable text**, not only inside a screenshot — Offsec's grading checks this explicitly
- Never modify, delete, or attempt to read these files' contents through any means other than their intended access — tampering is a code-of-conduct violation

## 5. Common Point-Loss Patterns to Avoid

- Skipping the "Information Gathering" subsection because it feels redundant with "Service Enumeration" — Offsec grades them as distinct
- Not explaining *why* a vulnerability exists, only that it was exploited
- Missing the offline/standalone target requirement in the report (some point categories are host-independent)
- Forgetting the local.txt/proof.txt text pasted alongside screenshots
