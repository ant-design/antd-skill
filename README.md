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
| ant-design | antd v6 component selection, theming/tokens, SSR, and performance | `skills/ant-design/` |
| ant-design-pro | layouts, routing, access control for Pro 5 + ProComponents | `skills/ant-design-pro/` |
| ant-design-x | AI & chat UI components and patterns | `skills/ant-design-x/` |

## Usage

1. Read the main skill entry: `skills/<skill>/SKILL.md`
2. Use references for advanced cases: `skills/<skill>/references/*.md`

## Scope

- antd v6 + React 18–19
- Ant Design Pro 5 + ProComponents
- Ant Design X (AI/chat UI)
- antd v5 maintenance and migration notes: `skills/ant-design/references/antd-v5.md`

## Structure

- `skills/ant-design/`
- `skills/ant-design-pro/`
- `skills/ant-design-x/`

## Skills Backed by Official Documentation

Each skill is a decision-focused guide derived from the official Ant Design ecosystem docs, with deeper details in `skills/*/references/*.md`.

| Skill | Description | Source |
| --- | --- | --- |
| ant-design | antd v6 component selection, theming/tokens, SSR, a11y, performance | ant.design |
| ant-design-pro | Pro 5 + ProComponents layouts, routing, access control, CRUD patterns | pro.ant.design / procomponents.ant.design |
| ant-design-x | @ant-design/x v2 AI/chat UI, streaming messages, tool rendering | x.ant.design |

## FAQ

### What Makes This Collection Different?

It focuses on agent decision-making for Ant Design projects, not end-user tutorials. The main `SKILL.md` files stay concise, while advanced topics live in `references/*.md` with official-doc links.

### Which Skill Should I Use?

- `ant-design`: core antd components, theming, SSR, a11y, performance
- `ant-design-pro`: admin layouts, routing, access control, CRUD with ProComponents
- `ant-design-x`: AI/chat UI, streaming message state, tool rendering

### How Do I Extend It?

Fork this repo, copy an existing skill folder, and update `SKILL.md` plus the `references/` files. Then update the tables in both readmes so the catalog stays accurate.
