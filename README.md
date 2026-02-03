# Ant Design Skills

English | [简体中文](README.zh.md)

A curated collection of Agent Skills and references for the Ant Design ecosystem.

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
2. Use references for advanced cases: `skills/<skill>/references/*.md`

## Scope

- antd v6 + React 18–19
- Ant Design Pro 5 + ProComponents (layouts, routing, access, CRUD)
- Ant Design X v2 (AI/chat UI, streaming, tool rendering)
- antd v5 maintenance and migration notes: `skills/ant-design/references/antd-v5.md`

## Structure

- `skills/ant-design/`

## Skills Backed by Official Documentation

Each skill is a decision-focused guide derived from the official Ant Design ecosystem docs, with deeper details in `skills/*/references/*.md`.

| Skill | Description | Source |
| --- | --- | --- |
| ant-design | antd v6, Pro 5 + ProComponents, and X v2 decision guide | ant.design / pro.ant.design / procomponents.ant.design / x.ant.design |

## FAQ

### What Makes This Collection Different?

It focuses on agent decision-making for Ant Design projects, not end-user tutorials. The main `SKILL.md` files stay concise, while advanced topics live in `references/*.md` with official-doc links.

### Which Skill Should I Use?

Use `ant-design` for core antd components, Pro layouts/routing/access/CRUD, and X chat/streaming/tool UI. Complex cases should jump to the relevant `references/*.md` within that skill.

### How Do I Extend It?

Fork this repo, copy an existing skill folder, and update `SKILL.md` plus the `references/` files. Then update the tables in both readmes so the catalog stays accurate.
