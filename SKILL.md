---
name: pwnote-skills
description: Directory of reusable skills for pwnote pentest platform — engagement import/export, automation workflows, and integration helpers.
---

# pwnote-skills

Directory of reusable skills for the pwnote pentest platform. Each skill file in this repo provides agent instructions for a specific task — engagement file generation, automation workflows, integration helpers, and other pwnote-related operations.

## Usage

Skills are loaded by name via the OpenCode `skill` tool. To use a skill:

1. List available skills: read this directory or use `skill` tool discovery
2. Load a skill: `skill` tool with the skill name matching a file in this repo
3. Follow the skill's instructions for structured output

## Skill Index

| File | Purpose |
|------|---------|
| `pwnote-engagement-file` | Create/validate pwnote engagement JSON files for import/export |

## Adding Skills

Add a new `.md` file with frontmatter (`name`, `description`) followed by markdown instructions. The filename without extension is the skill name used for loading.

### Frontmatter Fields

| Field | Required | Description |
|-------|----------|-------------|
| `name` | yes | Unique skill name, kebab-case, matching filename |
| `description` | yes | Short description shown in skill list, one line |

### Conventions

- Use `---` frontmatter delimiters
- Description should be actionable: "Create or validate..." not "This skill is for..."
- Keep skills focused — one task per file
- Reference related skills in the body as needed
