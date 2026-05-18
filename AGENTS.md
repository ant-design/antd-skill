# Ant Design Skills - Agent Guide

Generate and maintain Agent Skills for the Ant Design ecosystem.

## Core principles

- Focus on agent decision-making and practical usage patterns.
- Avoid end-user tutorials, getting-started steps, and obvious basics.
- Do not invent APIs or rely on undocumented behaviors.
- Keep `SKILL.md` concise; move advanced detail to `references/*.md`.
- Prefer short, focused examples when needed.

## Repo structure

```
.
└── skills/
    ├── ant-design-v5/
    │   ├── SKILL.md
    │   └── references/
    ├── ant-design-v6/
    │   ├── SKILL.md
    │   └── references/
    └── antd/
        └── SKILL.md
```

## Scope by skill

- **ant-design-v5**: antd 5.x + React 16.9-18 (React 19 via `@ant-design/v5-patch-for-react-19`), CSS-in-JS via `@ant-design/cssinjs`, plus Pro 5 layouts/routing/access/CRUD and X (AI/chat UI) patterns.
- **ant-design-v6**: antd 6.x + React 18-19, component selection, theming/tokens, SSR, a11y, performance, plus Pro 5 layouts/routing/access/CRUD and X (AI/chat UI) patterns.
- **antd**: offline `@ant-design/cli` workflow (v4/v5/v6) — API lookup, lint, migrate, doctor, usage, changelog, and bug reporting. Version-agnostic; complements both `ant-design-v*` skills.

The two `ant-design-v*` skills form a version router: each declares its supported antd major in its `description` and at the top of its `SKILL.md`, and Claude picks the matching one for the project. When updating either, keep their structure parallel so the router behavior stays predictable.

## Updating skills

1. Read the existing `SKILL.md` and relevant `references/*.md` first.
2. Keep the main skill as a decision guide; add new details as references.
3. Add or update reference files with kebab-case names.
4. Update the `Reference` index table in `SKILL.md` when adding references.
5. Ensure version scope and assumptions are explicit and consistent.

## Adding a new skill

- Create `skills/<name>/SKILL.md` and `skills/<name>/references/`.
- Include a clear scope, process, and output format in `SKILL.md`.
- Keep references short and task-oriented.
