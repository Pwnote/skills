<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="media/icon.svg">
    <source media="(prefers-color-scheme: light)" srcset="media/icon.svg">
    <img src="media/logo.webp" alt="Pwnote" width="320">
  </picture>
</p>

<p align="center">
  <a href="https://skills.sh/Pwnote/skills"><img src="https://skills.sh/b/Pwnote/skills" alt="skills.sh"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-blue?style=flat" alt="License"></a>
</p>

> **Note:** This repository contains Pwnote's implementation of skills for pentest workflow automation. For information about the Agent Skills standard, see [agentskills.io](http://agentskills.io).

# Pwnote Skills

Skills are folders of instructions, scripts, and resources that agents load dynamically to improve performance on specialized tasks. They teach AI agents how to complete specific pentest workflows in a repeatable way — generating engagement files, automating recon, formatting findings, and integrating with external tooling.

Pwnote Skills extend the [Pwnote](https://pwnote.com) pentest platform, giving agents domain-specific knowledge for security assessments, bug bounty hunting, certification exams, and CVE research.

## Installation

```bash
# Install all skills
npx skills add https://github.com/Pwnote/skills

# Install a specific skill
npx skills add https://github.com/Pwnote/skills --skill pwnote-bug-bounty
```

> **Prerequisite:** You need a Pwnote account and an AI agent that supports the Agent Skills protocol.

## Available Skills

> All skills are prefixed with `pwnote-` to avoid name conflicts with similar skills from other repositories.

| Skill | Description |
|-------|-------------|
| [pwnote-bug-bounty](./skills/pwnote-bug-bounty/SKILL.md) | Bug bounty workflow. Program intake, recon, vulnerability class playbooks, report writing (HackerOne / Bugcrowd / Intigriti / YesWeHack), triage disputes. |
| [pwnote-cve-research](./skills/pwnote-cve-research/SKILL.md) | CVE research and responsible disclosure. Disclosure timeline tracking, CNA/MITRE submission, advisory writing, CWE mapping. |
| [pwnote-tryhackme](./skills/pwnote-tryhackme/SKILL.md) | TryHackMe room notes and writeups. Structured note-taking per task, public writeup format, flag tracking. |
| [pwnote-hackthebox](./skills/pwnote-hackthebox/SKILL.md) | HackTheBox machine notes. Recon / foothold / privesc note structure, enumeration checklist, Linux and Windows privesc references. |
| [pwnote-offsec-pen200](./skills/pwnote-offsec-pen200/SKILL.md) | Offsec PEN-200 / OSCP workflow. Exam report structure, screenshot and evidence discipline, proof file conventions. |
| [pwnote-offsec-web300](./skills/pwnote-offsec-web300/SKILL.md) | Offsec WEB-300 / OSWE workflow. Whitebox source review, exploit chain documentation, PoC scripting conventions. |
| [pwnote-offsec-osai](./skills/pwnote-offsec-osai/SKILL.md) | Offsec OSAI / AI Red Teaming workflow. Prompt injection taxonomy, agent trajectory documentation, two-axis severity model. |
| [pwnote-engagement-file](./skills/pwnote-engagement-file/SKILL.md) | Engagement import/export JSON files. Bundles metadata, notebook documents, code/host/credential blocks, findings with CVSS/CWE/CVE, attack-path boards. |

## Adding a Skill

Drop a folder under `skills/` with a `SKILL.md` file and any scripts or resources it needs. The frontmatter `name` field must match the folder name.

```
skills/
  pwnote-your-skill/
    SKILL.md
    scripts/
    resources/
```

Refer to the [Agent Skills specification](https://agentskills.io) for the full schema and conventions.
