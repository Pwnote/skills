> **Note:** This repository contains Pwnote's implementation of skills for pentest workflow automation. For information about the Agent Skills standard, see [agentskills.io](http://agentskills.io).

# Pwnote Skills

Skills are folders of instructions, scripts, and resources that agents load dynamically to improve performance on specialized tasks. Skills teach agents how to complete specific pentest workflows in a repeatable way - generating engagement files, automating recon, formatting findings, and integrating with external tooling.

## About This Repository

This repository contains skills for Pwnote's pentest platform. Each skill is self-contained in its own folder with a `SKILL.md` file containing instructions and metadata.

## Installation

```bash
npx skills add https://github.com/Pwnote/skills --skill pwnote-engagement-file
```

## Available Skills

- `bug-bounty` - [Bug bounty workflow](./skills/bug-bounty/SKILL.md). Program intake, recon, vulnerability class playbooks, report writing (H1/Bugcrowd/Intigriti/YesWeHack), triage disputes.
- `cve-research` - [CVE research and responsible disclosure](./skills/cve-research/SKILL.md). Disclosure timeline tracking, CNA/MITRE submission, advisory writing, CWE mapping.
- `tryhackme` - [TryHackMe room notes and writeups](./skills/tryhackme/SKILL.md). Structured note-taking per task, public writeup format, flag tracking.
- `hackthebox` - [HackTheBox machine notes](./skills/hackthebox/SKILL.md). Recon/foothold/privesc note structure, enumeration checklist, linux/windows privesc references.
- `offsec-pen200` - [Offsec PEN-200 / OSCP workflow](./skills/offsec-pen200/SKILL.md). Exam report structure, screenshot/evidence discipline, proof file conventions.
- `offsec-web300` - [Offsec WEB-300 / OSWE workflow](./skills/offsec-web300/SKILL.md). Whitebox source review, exploit chain documentation, PoC scripting conventions.
- `offsec-osai` - [Offsec OSAI / AI Red Teaming workflow](./skills/offsec-osai/SKILL.md). Prompt injection taxonomy, agent trajectory documentation, two-axis severity model.
- `pwnote-engagement-file` - [Engagement import/export JSON files](./skills/pwnote-engagement-file/SKILL.md). Bundles metadata, notebook documents, code/host/credential blocks, findings with CVSS/CWE/CVE, attack-path boards.

## Adding a Skill

Drop a folder under `skills/` with a `SKILL.md` and any scripts/resources it needs. The frontmatter `name` must match the folder name.
