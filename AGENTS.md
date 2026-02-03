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
    ├── ant-design/
    │   ├── SKILL.md
    │   └── references/
```

## Scope by skill

- **ant-design**: antd v6 + React 18-19, component selection, theming/tokens, SSR, a11y, performance, plus Pro 5 layouts/routing/access/CRUD and X (AI/chat UI) patterns.

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
