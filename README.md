# Ant Design Skills

English | [简体中文](README.zh.md)

A curated collection of Agent Skills for the Ant Design ecosystem.

## Installation

### Option 1: `skills` CLI (recommended)

```bash
pnpx skills add ant-design/antd-skill
# or
npx skills add ant-design/antd-skill
```

This copies the skill folders into your current scope's `.claude/skills/` directory.

### Option 2: Claude Code CLI (manual)

Claude Code discovers skills in two locations:

- **User scope** — `~/.claude/skills/<name>/` (available in every session)
- **Project scope** — `<repo>/.claude/skills/<name>/` (available only in that project; committable)

Install user-wide:

```bash
git clone https://github.com/ant-design/antd-skill.git /tmp/antd-skill
mkdir -p ~/.claude/skills
cp -R /tmp/antd-skill/skills/ant-design ~/.claude/skills/
cp -R /tmp/antd-skill/skills/antd       ~/.claude/skills/
```

Install into a single project:

```bash
mkdir -p .claude/skills
cp -R /tmp/antd-skill/skills/ant-design .claude/skills/
cp -R /tmp/antd-skill/skills/antd       .claude/skills/
```

Verify in a Claude Code session:

```
/skills
```

The `ant-design` and `antd` skills should appear in the list. They auto-load when the conversation matches their `description` triggers (antd component work, CLI lookups, migrations, etc.).

To update later, re-pull the repo and re-copy, or replace the folders with symlinks to a local clone.

## Skills

| Skill | Description | Path |
| --- | --- | --- |
| ant-design | antd v6 + Ant Design Pro 5 + Ant Design X v2 decision guidance | `skills/ant-design/` |
| antd | Offline Ant Design CLI workflow for API lookup, debugging, migration, and usage analysis | `skills/antd/` |

## Usage

1. Read the main skill entry: `skills/<skill>/SKILL.md`
2. Follow the single SOP in that `SKILL.md`.

## Scope

- antd v6 + React 18–19
- Ant Design Pro 5 + ProComponents (layouts, routing, access, CRUD)
- Ant Design X v2 (AI/chat UI, streaming, tool rendering)
- Includes v5 maintenance/migration guidance in `skills/ant-design/SKILL.md`

## Structure

- `skills/ant-design/`
- `skills/antd/`

## Skills Backed by Official Documentation

Each skill is a decision-focused guide derived from the official Ant Design ecosystem docs, maintained as a single `SKILL.md`.

| Skill | Description | Source |
| --- | --- | --- |
| ant-design | antd v6, Pro 5 + ProComponents, and X v2 decision guide | ant.design / pro.ant.design / procomponents.ant.design / x.ant.design |
| antd | Ant Design CLI workflow for offline metadata and migration tasks | @ant-design/cli |

## FAQ

### What Makes This Collection Different?

It focuses on agent decision-making for Ant Design projects, not end-user tutorials. A single `SKILL.md` stays concise and points to official-doc links.

### Which Skill Should I Use?

Use `ant-design` for core antd components, Pro layouts/routing/access/CRUD, and X chat/streaming/tool UI, all from one `SKILL.md`. Use `antd` when you specifically want the offline `@ant-design/cli` workflow for API lookup, linting, migration, and changelog analysis.

### How Do I Extend It?

Fork this repo, copy an existing skill folder, and update `SKILL.md`. Then update the tables in both readmes so the catalog stays accurate.

### How Do I Use It in Claude Code?

Copy the desired skill folder(s) into `~/.claude/skills/` (user scope) or `<repo>/.claude/skills/` (project scope), then run `/skills` in a Claude Code session to confirm they are listed. Skills auto-load when the conversation matches their `description` triggers.
