---
name: pwnote-offsec-osai
description: Use whenever the user is working on Offsec's OSAI / AI Red Teaming certification track, or on AI/LLM/agentic security engagements generally — prompt injection findings, tool-use abuse, agent trajectory documentation, or writing up AI-specific security findings that don't map cleanly to traditional CVSS. Trigger on "OSAI", "AI Red Teaming", "LLM pentest", "prompt injection engagement", or "agentic AI exploitation", even without the word "skill".
---

# Offsec OSAI / AI Red Teaming Workflow

Reference for running and documenting an AI/LLM security assessment — prompt injection, tool-use abuse, and agent-specific findings that need a different taxonomy and severity model than traditional web/infra findings.

## 1. AI-Specific Finding Taxonomy

Categorize findings by the underlying attack predicate rather than a generic "prompt injection" label — this keeps findings comparable across engagements and maps directly onto a structured attack-algorithm taxonomy if one is in use:

| Category | Description |
|---|---|
| **EXFILTRATION** | The system is induced to leak data it shouldn't (system prompt, other users' context, tool outputs, secrets in context) to the attacker or an external destination |
| **UNTRUSTED_TO_ACTION** | Untrusted input (a document, webpage, tool result) is treated as an instruction and drives a consequential action the legitimate user didn't request |
| **PRIVILEGE_ESCALATION** | The agent is induced to use a tool/permission beyond what the current user/context should allow |
| **PERSISTENCE** | The injected behavior survives beyond the single turn/session (e.g., written to memory, a file, or a scheduled task the agent later reads back) |
| **DENIAL_OF_SERVICE** | The agent is induced into a resource-exhausting loop, excessive tool calls, or a stuck state |
| **JAILBREAK / POLICY_BYPASS** | Model safety/policy constraints are circumvented, independent of any tool-use consequence |

Tag every finding with a primary category (and secondary if it chains, e.g. UNTRUSTED_TO_ACTION → EXFILTRATION).

## 2. Test Harness / Trajectory Documentation

Agent findings need the full trajectory, not just an input/output pair, since the vulnerability is often in *how* the agent got there:

```
- Turn-by-turn transcript (user input, model reasoning if visible, tool calls + arguments, tool results)
- Point of deviation — the exact turn where the agent's behavior diverged from expected/authorized behavior
- Root cause — which trust boundary was crossed (e.g., tool output treated as trusted instruction)
- Reproducibility — does it require a specific model version/temperature, or is it deterministic
```

If session replay/recording tooling is available in the environment being tested, capture the full replay artifact alongside the transcript — a static screenshot loses the tool-call sequence that's usually the actual finding.

## 3. Report Format

AI findings often don't map cleanly to CVSS since impact depends heavily on what tools/permissions the agent has, which varies by deployment. Use a two-part severity model:

```
## Finding: [Name]
Category: [EXFILTRATION / UNTRUSTED_TO_ACTION / etc.]

### Technical Severity
[How reliably the injection/bypass works, in isolation — independent of deployment]

### Deployment Impact Severity
[What this actually enables GIVEN the tools/permissions/data this specific agent has access to]

### Trajectory
[turn-by-turn evidence]

### Root Cause
[trust boundary crossed]

### Remediation
[e.g., input/output trust segmentation, tool permission scoping, human-in-the-loop gating for consequential actions]
```

Separating technical severity from deployment impact avoids both over- and under-stating risk — the same injection technique can be a non-issue in a read-only agent and critical in one with write/send/purchase tools.

See `references/ai-severity-model.md` for the full severity rubric.

## 4. Reusing Existing Taxonomy Work

If prior work already defines an attack-algorithm class or predicate taxonomy for this kind of engagement, reuse that taxonomy directly for consistency rather than inventing a parallel one per engagement.
