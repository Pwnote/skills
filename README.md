> **Note:** This repository contains Pwnote's implementation of skills for pentest workflow automation. For information about the Agent Skills standard, see [agentskills.io](http://agentskills.io).

[![skills.sh](https://skills.sh/b/Pwnote/skills)](https://skills.sh/Pwnote/skills)

# Pwnote Skills

Skills are folders of instructions, scripts, and resources that agents load dynamically to improve performance on specialized tasks. Skills teach agents how to complete specific pentest workflows in a repeatable way - generating engagement files, automating recon, formatting findings, and integrating with external tooling.

## About This Repository

This repository contains skills for Pwnote's pentest platform. Each skill is self-contained in its own folder with a `SKILL.md` file containing instructions and metadata.

## Installation

```bash
npx skills add https://github.com/Pwnote/skills --skill pwnote-engagement-file
```

## Available Skills

- `pwnote-engagement-file` - [Create or validate engagement import/export JSON files](./skills/pwnote-engagement-file/SKILL.md). Bundles metadata, notebook documents, code/host/credential blocks, findings with CVSS/CWE/CVE, attack-path boards, and activity history.

## Adding a Skill

Drop a folder under `skills/` with a `SKILL.md` and any scripts/resources it needs. The frontmatter `name` must match the folder name.
