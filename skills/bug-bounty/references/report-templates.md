# Platform Report Templates

## HackerOne

```
## Summary
[one paragraph, plain language]

## Steps To Reproduce
1.
2.
3.

## Supporting Material/References
[screenshots, request/response pairs]

## Impact
[concrete impact statement]
```

- H1 uses its own severity rating system (CVSS-based, program can override) — always include a CVSS vector if the program requests one.
- Weakness field should map to a CWE if you can identify one; helps triage speed.

## Bugcrowd

```
## Description
[what the vuln is, root cause]

## Steps to Reproduce
1.
2.

## Proof of Concept
[requests, screenshots, or script]

## Impact
[business impact framed against Bugcrowd's VRT category]
```

- Bugcrowd's VRT (Vulnerability Rating Taxonomy) categories are specific — pick the closest matching VRT entry explicitly in your title/summary, it speeds triage significantly.

## Intigriti

```
## Vulnerability details
[technical description]

## Proof of concept
[numbered reproduction steps + evidence]

## Impact
[impact statement]

## Risk / CVSS
[vector + score]
```

- Intigriti triage teams tend to want the PoC self-contained with numbered steps rather than narrative prose — keep it terse.

## YesWeHack

```
## Summary

## Description / Root cause

## Steps to reproduce

## Impact

## Remediation advice
```

- YesWeHack explicitly expects a remediation section in-report (not always required elsewhere) — don't skip it.

## Cross-Platform Rules

- Never include real user PII/data in a PoC — use test accounts or redact.
- One vulnerability per report; don't bundle unrelated findings even if discovered in the same session (bundling slows triage and payout).
- Attach raw request/response text, not just screenshots — triagers need to copy-paste to verify.
