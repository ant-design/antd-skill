# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A catalog of Agent Skills for the Ant Design ecosystem. There is no application code, no build, and no test suite — the deliverables are the `SKILL.md` files (and their `references/`) under `skills/`. Consumers install skills either via `pnpx skills add ant-design/antd-skill` (the `skills` CLI), or by copying folders directly into `~/.claude/skills/` (user scope) or `<repo>/.claude/skills/` (project scope) for Claude Code. See `README.md` "Installation" for the exact commands.

`package.json` is a stub (`private: true`, no scripts, no dependencies). Do not add a toolchain.

## Skill layout

```
skills/<name>/
  SKILL.md           # entry point — single SOP, decision-focused
  references/        # optional, kebab-case .md files for advanced detail
```

`SKILL.md` requires YAML frontmatter:
- `name` — must match the folder name
- `description` — single-line trigger description (what kinds of tasks should load this skill)
- `allowed-tools` — optional, list shell commands the skill is permitted to run (see `skills/antd/SKILL.md`)

Existing skills:
- `skills/ant-design/` — decision guide spanning antd v6, Pro 5/ProComponents, X v2, and the offline CLI. Uses an "S-P-O" (Scope / Process / Output) section structure plus a regression checklist.
- `skills/antd/` — focused workflow around `@ant-design/cli` for offline API lookup, lint, migrate, doctor, usage, changelog, and bug reporting (`antd bug`, `antd bug-cli`).

The two skills overlap intentionally: `ant-design` is the broader decision guide and links to the CLI workflow as a reference; `antd` is the standalone CLI-only entry point.

## Authoring rules (from AGENTS.md)

- Skills are for **agent decision-making**, not end-user tutorials. Skip getting-started steps and obvious basics.
- Do not invent APIs or document undocumented behavior. Cite the official Ant Design docs (`ant.design`, `pro.ant.design`, `procomponents.ant.design`, `x.ant.design`) or `@ant-design/cli` output.
- Keep `SKILL.md` concise. Push advanced detail into `references/*.md` and add a row to the `## References` table in `SKILL.md`.
- Reference filenames are kebab-case.
- Make version scope and assumptions explicit (e.g., "antd v6 + React 18–19, TypeScript").

## When updating a skill

1. Read the existing `SKILL.md` and any `references/*.md` first — don't duplicate content that already lives in a reference.
2. Preserve the skill's structure (the S-P-O headings in `ant-design`, the numbered Scenarios in `antd`).
3. If you add a reference file, update the `## References` table in the corresponding `SKILL.md`.
4. If you add or rename a skill, update the tables in **both** `README.md` and `README.zh.md` so the catalog stays in sync (the Chinese readme mirrors the English one).

## When working on antd code (not on this repo)

If a task in this repo involves writing/checking antd component code (e.g., examples inside a skill), follow the skills' own rules: query `antd info <Component> --format json` and `antd demo <Component> <name> --format json` via `@ant-design/cli` before writing component code, and run `antd lint <path> --format json` after. Don't rely on memory for antd APIs.
