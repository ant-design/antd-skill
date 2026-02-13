# Ant Design Skills

English | [简体中文](README.zh.md)

A curated collection of Agent Skills for the Ant Design ecosystem.

## Installation

```bash
pnpx skills add ant-design/antd-skill
# or
npx skills add ant-design/antd-skill
```

## Skills

| Skill | Description | Path |
| --- | --- | --- |
| ant-design | antd v6 + Ant Design Pro 5 + Ant Design X v2 decision guidance | `skills/ant-design/` |

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

## Skills Backed by Official Documentation

Each skill is a decision-focused guide derived from the official Ant Design ecosystem docs, maintained as a single `SKILL.md`.

| Skill | Description | Source |
| --- | --- | --- |
| ant-design | antd v6, Pro 5 + ProComponents, and X v2 decision guide | ant.design / pro.ant.design / procomponents.ant.design / x.ant.design |

## FAQ

### What Makes This Collection Different?

It focuses on agent decision-making for Ant Design projects, not end-user tutorials. A single `SKILL.md` stays concise and points to official-doc links.

### Which Skill Should I Use?

Use `ant-design` for core antd components, Pro layouts/routing/access/CRUD, and X chat/streaming/tool UI, all from one `SKILL.md`.

### How Do I Extend It?

Fork this repo, copy an existing skill folder, and update `SKILL.md`. Then update the tables in both readmes so the catalog stays accurate.
