> **Note:** This repository contains Pwnote's implementation of skills for pentest workflow automation. For information about the Agent Skills standard, see [agentskills.io](http://agentskills.io).

[![skills.sh](https://skills.sh/b/Pwnote/skills)](https://skills.sh/Pwnote/skills)

# Pwnote Skills

Skills are folders of instructions, scripts, and resources that agents load dynamically to improve performance on specialized tasks. Skills teach agents how to complete specific pentest workflows in a repeatable way — generating engagement files, automating recon, formatting findings, and integrating with external tooling.

## About This Repository

This repository contains skills for Pwnote's pentest platform. Each skill is self-contained in its own folder with a `SKILL.md` file containing instructions and metadata.

## Installation

```bash
npx skills add Pwnote/skills
```

## Available Skills

- `pwnote-engagement-file` — [Create or validate engagement import/export JSON files](./skills/pwnote-engagement-file/SKILL.md). Bundles metadata, notebook documents, code/host/credential blocks, findings with CVSS/CWE/CVE, attack-path boards, and activity history.

## Creating a Skill

Skills are simple to create — just a folder with a `SKILL.md` file containing YAML frontmatter and instructions:

```markdown
---
name: my-skill-name
description: A clear description of what this skill does and when to use it
---

# My Skill Name

[Instructions the agent follows when this skill is active]
```

The frontmatter requires two fields:
- `name` — Unique identifier (lowercase, hyphens for spaces)
- `description` — What the skill does and when to use it

See the [engagement-file skill](./skills/pwnote-engagement-file/SKILL.md) for a reference implementation.
