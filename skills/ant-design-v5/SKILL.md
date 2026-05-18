---
name: ant-design-v5
description: Decision guide for antd 5.x projects (`antd@^5` in package.json), Ant Design Pro 5/ProComponents, Ant Design X v2, and the offline `@ant-design/cli`. Use for component selection, theming/tokens, CSS-in-JS, SSR, React 19 compatibility, a11y, performance, routing/access/CRUD, AI/chat UI patterns, local API lookup, debugging, and usage analysis on v5 codebases. For antd 6.x projects, use the `ant-design-v6` skill instead.
---

# Ant Design v5

## Version routing (read first)
- This skill targets **antd 5.x only**. Confirm the project's antd version before applying any guidance:
  - Check `package.json` `dependencies.antd` (or `peerDependencies`/`pnpm-lock.yaml`/`package-lock.json`).
  - If the resolved version is `^5.x` / `>=5.0.0 <6.0.0`, continue with this skill.
  - If the resolved version is `^6.x`, **stop** and switch to the `ant-design-v6` skill — v6 changes the styling engine, drops several v5-deprecated props (`dropdownClassName`, `visible`, `bordered` etc.), and ships different theme tokens.
  - If the project has no antd installed yet, ask the user which major version they want to target before proceeding.
- The `antd` CLI skill is version-agnostic and complements this skill via `--version 5.x.x`.

## S - Scope
- Target: `antd@^5` + React 16.9-18 (React 19 requires the patch package, see "Mandatory rules"). Pro: `@ant-design/pro-components` (v5 line). X: `@ant-design/x@^2`.
- Styling engine: `@ant-design/cssinjs` (CSS-in-JS). Less is no longer supported; `babel-plugin-import` is no longer supported; `antd/dist/antd.css` no longer exists — use `antd/dist/reset.css` for base styles only.
- Tooling: `@ant-design/cli` for offline component metadata, demos, changelogs, migrations, linting, doctor checks, and usage analysis (pass `--version 5.x.x`).
- Focus: decision guidance only; no end-user tutorials.
- Source policy: official v5 docs only; no undocumented APIs or internal `.ant-*` coupling.

### Default assumptions
- Language: TypeScript.
- Styling: design tokens first via `ConfigProvider` `theme`, then component `classNames`/`styles`; avoid global overrides.
- Provider: one root `ConfigProvider` unless strict isolation is required.
- Date library: Day.js (v5 default — Moment.js was removed; use `@ant-design/moment-webpack-plugin` only if migration constraints force it).

### Mandatory rules
- Before writing or changing antd component code, query the component API first with `antd info <Component> --version 5.x.x --format json`. Do not rely on memory when the CLI can answer it offline.
- Always pass `--version 5.x.x` (or rely on auto-detect from `node_modules`) and `--format json` to `antd` CLI commands so the output matches the project's exact v5 minor version.
- After changing antd code, run `antd lint <changed-path> --format json`.
- If an `antd` CLI command crashes, returns wrong data, or violates its documented behavior, prepare an `antd bug-cli` preview for user confirmation instead of silently working around it.
- For component questions, map the component name to the kebab-case route slug `{components}` (e.g. `TreeSelect -> tree-select`, `Button -> button`) and request docs in this order (CN first, EN fallback):
  1. `https://5x.ant.design/components/{components}-cn`
  2. `https://5x.ant.design/components/{components}`
  - Fallback source (pinned commit): `https://github.com/ant-design/ant-design/tree/5.29.3/components/{components}`.
- Use only documented antd/Pro/X APIs. Do not invent props/events/component names. Do not rely on internal DOM or `.ant-*` selectors.
- Use the renamed v5 props, not the v4 ones:
  - `popupClassName` (not `dropdownClassName` / `tooltipClassName`) for AutoComplete, Cascader, Select, TreeSelect, TimePicker, DatePicker, Mentions.
  - `open` (not `visible`) for Modal, Drawer, Dropdown, Tooltip; `Table` column `filterDropdownOpen` (not `filterDropdownVisible`); Slider `tooltip={{ open, placement }}` (not `tooltipVisible`/`tooltipPlacement`).
  - `message.warning()` (not `message.warn()`); `notification.destroy()` (not `notification.close()`).
- Removed-from-core components (handle explicitly):
  - `Comment` → import from `@ant-design/compatible`.
  - `PageHeader` → import from `@ant-design/pro-components`.
  - `BackTop` → use `FloatButton.BackTop`.
- React 19 compatibility: if the project uses React 19 and any code calls `message.*`, `notification.*`, `Modal.*` static methods or relies on wave/ripple effects, require `@ant-design/v5-patch-for-react-19` (imported once at the entry). See `references/cssinjs-ssr.md`. Prefer the hook forms (`App.useApp()` / `message.useMessage()` / `notification.useNotification()` / `Modal.useModal()`) regardless.
- Theme priority: global tokens → component tokens → `classNames`/`styles`. Drive everything through `ConfigProvider`'s `theme` prop; do not override compiled cssinjs class names.

## P - Process
### 1) Classify
- Identify layer: core antd, Pro, or X.
- Confirm exact v5 minor (e.g. `5.21.4`), React major (16/17/18/19), rendering mode (CSR / SSR / streaming / static export), data scale, and whether `@ant-design/cli` should be the primary lookup path.

### 2) Query authoritative sources
- Prefer local `@ant-design/cli` first for structured lookup (pass `--version 5.x.x`):
  - `antd info` for props/API
  - `antd demo` for a working baseline
  - `antd doc` for full docs
  - `antd token` / `antd semantic` for theming and styling hooks
  - `antd doctor`, `antd lint`, `antd usage`, `antd changelog` when debugging or auditing
- Then request the official v5 component docs (`5x.ant.design`, CN first) when narrative docs or cross-checking are needed.
- For upgrade questions to v6, hand off to the `antd` CLI workflow: `antd migrate 5 6 --format json` and `antd changelog 5.x.x 6.0.0 --format json`.

### 3) Decide
- Provider baseline: CSR → `ConfigProvider`; SSR → `ConfigProvider` + `StyleProvider` from `@ant-design/cssinjs` with `createCache`/`extractStyle` (see `references/cssinjs-ssr.md`).
- Theming baseline: `ConfigProvider` `theme` tokens (global → component) → `classNames`/`styles`.
- React 19 baseline: install `@ant-design/v5-patch-for-react-19` and import once; only fall back to `unstableSetRender` for UMD / micro-frontend hosts where the patch can't run.
- Legacy browser baseline (Chrome <88 / `:where` unsupported): wrap with `<StyleProvider hashPriority="high" transformers={[legacyLogicalPropertiesTransformer]}>`.
- Output recommendation + risk + verification points (SSR/a11y/perf), citing CLI findings when used.

## O - Output
- Provide short decision rationale (1-3 sentences).
- Include minimal provider/theming strategy (ConfigProvider + StyleProvider when SSR).
- Include concrete SSR/a11y/perf checks (style extraction, hydration order, React 19 patch presence).
- For Pro: include route/menu/access and CRUD schema direction.
- For X: include message/tool schema and streaming state direction.

## References

| File | Use when |
| --- | --- |
| `references/antd-cli.md` | You need the exact offline CLI workflow scoped to v5 for API lookup, demos, linting, doctor checks, changelog review, usage analysis, or bug reporting. |
| `references/cssinjs-ssr.md` | You need the v5 CSS-in-JS, SSR (Next.js Pages/App Router), legacy-browser compatibility, or React 19 patch setup. |

## Regression checklist
- [ ] One root `ConfigProvider`; `theme` tokens defined there, not via global CSS.
- [ ] SSR style extraction wired (`createCache` → render → `extractStyle(cache)` injected into `<head>`); hydration order verified.
- [ ] Tokens first; no broad global `.ant-*` overrides; no `babel-plugin-import` in build config.
- [ ] All deprecated v4 props removed: no `dropdownClassName`, `visible` (where renamed), `bordered`-as-boolean on inputs (use `variant`), `filterDropdownVisible`, `message.warn`.
- [ ] Table has stable `rowKey`; sort/filter/pagination entry is unified.
- [ ] Select remote mode disables local filter when using remote search.
- [ ] Upload controlled/uncontrolled mode is explicit with failure/retry path.
- [ ] If React 19 is in use, `@ant-design/v5-patch-for-react-19` is imported at the entry; static method usages are still reviewed for migration to hook forms.
- [ ] Legacy-browser targets (if required) wrapped with `StyleProvider hashPriority="high"` + `legacyLogicalPropertiesTransformer`.
- [ ] Pro route/menu/access remain consistent with backend enforcement.
- [ ] X streaming supports stop/retry and deterministic tool rendering.
- [ ] If `antd` CLI was used, commands ran with `--version 5.x.x --format json` and any CLI defect was escalated via `antd bug-cli` preview.
