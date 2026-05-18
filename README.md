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
cp -R /tmp/antd-skill/skills/ant-design-v5 ~/.claude/skills/
cp -R /tmp/antd-skill/skills/ant-design-v6 ~/.claude/skills/
cp -R /tmp/antd-skill/skills/antd          ~/.claude/skills/
```

Install into a single project:

```bash
mkdir -p .claude/skills
cp -R /tmp/antd-skill/skills/ant-design-v5 .claude/skills/
cp -R /tmp/antd-skill/skills/ant-design-v6 .claude/skills/
cp -R /tmp/antd-skill/skills/antd          .claude/skills/
```

You only need to copy the version-specific skill that matches your project (`ant-design-v5` **or** `ant-design-v6`). The `antd` CLI skill is version-agnostic and complements either one.

Verify in a Claude Code session:

```
/skills
```

The installed skills (`ant-design-v5` and/or `ant-design-v6`, plus `antd`) should appear in the list. They auto-load when the conversation matches their `description` triggers — version-specific skills key off the project's `package.json` antd version, and the `antd` CLI skill triggers on any antd-related task.

To update later, re-pull the repo and re-copy, or replace the folders with symlinks to a local clone.

## Skills

| Skill | Description | Path |
| --- | --- | --- |
| ant-design-v5 | antd 5.x + Ant Design Pro 5 + Ant Design X v2 decision guidance (CSS-in-JS, SSR, React 19 patch) | `skills/ant-design-v5/` |
| ant-design-v6 | antd 6.x + Ant Design Pro 5 + Ant Design X v2 decision guidance | `skills/ant-design-v6/` |
| antd | Offline Ant Design CLI workflow for API lookup, debugging, migration, and usage analysis (v4/v5/v6) | `skills/antd/` |

The two `ant-design-v*` skills act as a version router: each declares its supported antd major in its `description` and at the top of its `SKILL.md`, and Claude picks the one that matches the project's `package.json`.

## Usage

1. Read the main skill entry: `skills/<skill>/SKILL.md`
2. Follow the single SOP in that `SKILL.md`.

## Scope

- antd 5.x (React 16.9–18, with React 19 supported via `@ant-design/v5-patch-for-react-19`)
- antd 6.x (React 18–19)
- Ant Design Pro 5 + ProComponents (layouts, routing, access, CRUD) — usable from either version skill
- Ant Design X v2 (AI/chat UI, streaming, tool rendering) — usable from either version skill
- `@ant-design/cli` offline workflows for v4/v5/v6 via the `antd` skill

## Structure

- `skills/ant-design-v5/`
- `skills/ant-design-v6/`
- `skills/antd/`

## Skills Backed by Official Documentation

Each skill is a decision-focused guide derived from the official Ant Design ecosystem docs, maintained as a single `SKILL.md`.

| Skill | Description | Source |
| --- | --- | --- |
| ant-design-v5 | antd 5.x, Pro 5 + ProComponents, and X v2 decision guide | 5x.ant.design / pro.ant.design / procomponents.ant.design / x.ant.design |
| ant-design-v6 | antd 6.x, Pro 5 + ProComponents, and X v2 decision guide | ant.design / pro.ant.design / procomponents.ant.design / x.ant.design |
| antd | Ant Design CLI workflow for offline metadata and migration tasks (v4/v5/v6) | @ant-design/cli |

## FAQ

### What Makes This Collection Different?

It focuses on agent decision-making for Ant Design projects, not end-user tutorials. A single `SKILL.md` stays concise and points to official-doc links.

### Which Skill Should I Use?

Pick by your project's antd major:
- antd 5.x → `ant-design-v5` (covers v5 CSS-in-JS, SSR, React 19 patch, Pro 5, X v2).
- antd 6.x → `ant-design-v6` (covers v6 tokens/SSR, Pro 5, X v2).

Add `antd` alongside whichever version skill you chose when you want the offline `@ant-design/cli` workflow for API lookup, linting, migration (`antd migrate 5 6`), and changelog analysis. The version skills include a "version routing" preamble at the top of their `SKILL.md` so Claude can confirm the project's antd version before applying guidance.

### How Do I Extend It?

Fork this repo, copy an existing skill folder, and update `SKILL.md`. Then update the tables in both readmes so the catalog stays accurate.

### How Do I Use It in Claude Code?

Copy the desired skill folder(s) into `~/.claude/skills/` (user scope) or `<repo>/.claude/skills/` (project scope), then run `/skills` in a Claude Code session to confirm they are listed. Skills auto-load when the conversation matches their `description` triggers.
