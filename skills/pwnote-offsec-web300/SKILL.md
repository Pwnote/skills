---
name: pwnote-offsec-web300
description: Use whenever the user is working on Offsec's WEB-300 course/OSWE — whitebox source code review methodology, exploit chain documentation, PoC scripting, or OSWE exam report writing. Trigger on "OSWE", "WEB-300", "whitebox", "source code review" in a pentest context, or "exploit chain", even without the word "skill".
---

# Offsec WEB-300 / OSWE Workflow

Reference for structuring a whitebox web application security review from source review through exploit chain PoC and exam-style report.

## 1. Source Review Workflow

Whitebox review is systematic, not exploratory — follow this order rather than jumping straight to a suspected sink:

1. **Entry point mapping** — enumerate every externally-reachable route/controller/handler in the application; this is your complete attack surface inventory before you look for bugs
2. **Auth/session code paths** — trace how authentication and authorization are enforced across those entry points; note any entry point where the check is inconsistent or missing relative to similar routes
3. **Data flow / taint tracing** — for each entry point, trace user-controlled input from source (request parameter) to sink (DB query, file operation, template render, deserialization call, shell invocation, outbound request)
4. **Sink classification** — group findings by sink type since remediation and exploitability differ significantly by sink class

Document this as a structured `table` block per entry point: route, input source, sinks reached, auth requirement, notes.

## 2. Exploit Chain Documentation

WEB-300 findings are frequently *chains* (e.g., an authenticated low-privilege bug combined with a logic flaw to reach unauthenticated RCE) rather than single-step bugs. Document chains as:

```
Step 1: [primitive gained] — [how]
Step 2: [primitive gained] — [how, building on step 1]
...
Final: [end impact]
```

Use a pwnote `killchain` board with each step as a node and edges showing the dependency between primitives — this is the same shape as an exploit-chain visualizer, so if a chain visualization tool is available, generate the chain diagram directly from this step list rather than re-deriving it.

## 3. PoC Scripting Conventions

Standard PoC skeleton shape for web exploit chains (language-agnostic structure, adapt to your usual scripting language):

```
1. Session/auth setup — obtain whatever starting credential/session the chain requires
2. Step functions — one function per chain step, each returning what the next step needs
3. Chain orchestration — calls steps in order, asserts expected intermediate state at each step
4. Final impact demonstration — the observable proof (e.g., file read contents, command output, admin action performed)
5. Output — clear pass/fail statement plus captured evidence
```

Keep each step function independently testable/re-runnable so a reviewer can verify any single link in the chain, not just the end-to-end run.

## 4. Report Format

OSWE reports differ from PEN-200 reports: heavier on code snippets and data-flow explanation, lighter on host-by-host screenshots.

```
1. Executive Summary
2. Vulnerability Summary Table
3. Methodology (source review approach used)
4. Findings — one per exploit chain
   4.x [Chain name]
     - Affected code (file/line references, snippet)
     - Data flow explanation (source → sink)
     - Exploit chain steps
     - PoC script / commands
     - Proof (flag/impact evidence)
     - Remediation (specific code-level fix, not generic advice)
5. Appendix
```

Include actual code snippets (the vulnerable lines) inline in the finding — this is expected and different from PEN-200 norms, where narrative + screenshots dominate.
