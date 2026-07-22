# Vulnerability Class Notes

Methodology-level notes per class: what distinguishes a real finding from noise, and how to document it. Not a payload cookbook — payload/technique specifics belong in your own private notes, not in a shared skill.

## IDOR / BOLA

- Root cause: object reference (ID, UUID, filename) is trusted from the client without an authorization check tying it to the requesting principal.
- What makes it a strong finding vs a weak one: cross-tenant/cross-user data exposure is strong; same-user-different-session is usually not reportable.
- Document: two accounts, the exact request that crosses the boundary, and what data/action was exposed.

## SSRF

- Root cause: server-side component fetches a URL/resource whose destination is influenced by user input, without an allowlist.
- Strong finding: reaches internal-only infrastructure (metadata endpoints, internal admin panels, other internal services) or achieves protocol smuggling.
- Weak finding: blind SSRF to an external collector with no internal reach demonstrated — still reportable but expect lower severity.
- Document: the exact parameter, the callback/collector evidence, and — if possible — what internal resource was actually reached.

## Auth / Session Bypass

- Root cause categories: missing server-side checks after a client-side gate, JWT validation gaps (algorithm confusion, missing signature verification, weak secret), session fixation, password reset token predictability/leakage.
- Document: the specific check that's missing or bypassed, and a reproducible before/after (unauthenticated request succeeding where it should 401/403).

## Business Logic Abuse

- Root cause: the app enforces *how* a workflow is used but not *what states* are reachable — e.g., a multi-step checkout or approval flow lets a step be skipped or replayed out of order.
- Hardest class to automate discovery for; comes from actually mapping the state machine of a workflow, not scanning.
- Document: the intended flow, the deviation, and the concrete business impact (price manipulation, privilege escalation via workflow skip, quota bypass).

## Race Conditions

- Root cause: a check-then-act sequence (balance check → deduct, coupon validity → redeem) isn't atomic.
- Document: the exact concurrent request pattern used, the number of successful duplicate actions achieved, and the resulting inconsistent state (e.g., balance below zero, coupon redeemed N times).

## General Documentation Standard

For every class, a report should let a reviewer reproduce the finding without asking a single clarifying question. If your steps-to-reproduce require tribal knowledge of your recon, add it explicitly.
