---
name: ant-design
description: Ant Design 6.x guidance for selecting components, theming/tokens, css-in-js/SSR setup, and resolving antd component behavior in React/Next.js/Umi/Vite apps. Use when building or reviewing UI with antd, configuring ConfigProvider/theme, or troubleshooting Ant Design UI/SSR/performance issues.
---

# Ant Design

## S - Scope
- Target: antd@^6 with React 18-19 (per official docs).
- Cover: core components, theming/tokens, css-in-js, SSR, a11y, and performance patterns.
- Avoid: Pro routing/layout and ProComponents (use ant-design-pro skill).
- Avoid: AI chat/copilot UI (use ant-design-x skill).

### Default assumptions (when not specified)
- Language: TypeScript.
- Styling: prefer tokens, `classNames`, and `styles`; avoid global overrides.
- Provider: a single `ConfigProvider` at app root, unless isolation is required.
- Dependencies: do not add new packages unless required or requested.

### Scope rules (must follow)
- Use only officially documented antd APIs and patterns.
- Do not invent props, events, or component names.
- Assume v6 by default; do not mix v5 APIs unless explicitly requested.
- Do not add global `.ant-*` overrides; prefer tokens and component tokens.
- Keep examples short; no long, multi-screen samples in the main skill.
- Do not rely on internal `.ant-*` classes or DOM details; if unavoidable, state risk and alternatives.
- Theme priority is fixed: global tokens -> component tokens -> alias tokens.
- For SSR, provide the minimal provider setup and verification points (hydration, style order, duplication).
- Route complex issues to `Reference` files; main skill gives only decisions and entry points.

### Complex triggers (must open a `Reference`)
- More than 3 interaction states or cross-field linkage (Form).
- Remote search, large data, or custom rendering (Select).
- Server sorting/filtering/pagination, virtualization, fixed columns/headers (Table).
- Async load, checkStrictly, or virtualization (Tree).
- Controlled `fileList`, `customRequest`, preview/auth edge cases (Upload).
- SSR style order, streaming/hydration errors, or performance bottlenecks.

### `Reference` index (Chinese)
Topic | Description | `Reference`
--- | --- | ---
Core v6 | Version scope, migration notes, theming/SSR overview | `references/antd-v6.md`
Legacy v5 | Existing v5 projects and migration guardrails | `references/antd-v5.md`
Form advanced | Dynamic forms, dependencies, validation perf | `references/form-advanced.md`
Table advanced | Sorting/filtering/virtualization patterns | `references/table-advanced.md`
Upload advanced | Controlled upload, customRequest, edge cases | `references/upload-advanced.md`
Select advanced | Remote search, tags, rendering and a11y | `references/select-advanced.md`
Tree advanced | Async load, checkStrictly, virtual | `references/tree-advanced.md`

### Reference routing rule
- Do not expand advanced topics in the main skill.
- Jump to a `Reference` if any condition matches:
  - More than 3 interaction states.
  - Async flows or large data sets.
  - Virtualization or performance tuning.
  - Complex accessibility requirements.

## P - Process
### 1) Clarify context before advising
- Framework and rendering: Next.js / Umi / Vite? CSR / SSR / streaming?
- antd version: confirm v6 if unclear.
- Theming depth: small token changes or component-level overrides?
- Data scale: large lists/tables/trees/selects?
- Interaction complexity: controlled state, linkage, async, auth, upload flows?

### 2) Provider minimal set
- CSR: usually `ConfigProvider` only.
- SSR or strict style order: add `StyleProvider` as per `references/antd-v6.md`.
- One app, one root provider; local themes only for isolation needs.

### 3) Component selection rules
- Form: prefer `Form` as source of truth unless external state is required.
- Overlay: `Modal` for blocking flows; `Drawer` for side context or long content.
- Lists: structured data uses `Table`, light lists use `List`; `Table` needs stable `rowKey`.
- Large data: use virtualization (see `references/table-advanced.md`).
- Select: local filter uses `filterOption`; remote search uses `showSearch` + `filterOption={false}` + `onSearch` (see `references/select-advanced.md`).
- Upload: controlled flow uses `fileList`; complex flow uses `customRequest` (see `references/upload-advanced.md`).

### 4) Theming decision chain
1. Use global tokens for most cases.
2. Use component tokens or `classNames`/`styles` for differences.
3. Only if unavoidable, use scoped CSS overrides and state the risk.
4. Never rely on global `.ant-*` overrides.

### 5) Shunt complexity to `Reference`
- If any complex trigger matches, provide decision + minimal skeleton + `Reference` path.
- Details live in the corresponding `references/*.md`.

### 6) a11y and performance checks
- a11y: keyboard access, focus management for overlays, icon buttons with `aria-label`, not color-only states.
- perf: stable keys, memoized columns, avoid frequent setState, use virtualization and throttling as needed.

## O - Output
### Output should include (as needed)
- Component and layout recommendations with 1-3 sentence rationale.
- Minimal provider and theming strategy.
- SSR, perf, and a11y risks with concrete mitigations.
- A `Reference` path when complex triggers match.
- Advice only (no code) when the request is selection or decision guidance.

### Output forbidden
- Inventing antd APIs, tokens, or relying on internal classes without calling out risk.
- Replacing tokens with global CSS overrides.
- Vague SSR/hydration advice without verification points.

### Regression checklist (prefer 5-10 items)
- [ ] Provider: one root `ConfigProvider`; SSR style order is controlled.
- [ ] Theming: tokens first, no broad global `.ant-*` overrides.
- [ ] Form: validation and linkage are within `Form` and reproducible.
- [ ] Table: stable `rowKey`; pagination/sort/filter entry points are consistent.
- [ ] Select: remote search disables local filter; a11y checks pass.
- [ ] Upload: controlled vs uncontrolled mode is clear; failure and retry flows defined.
- [ ] Overlays: close and destroy behavior is defined (`destroyOnClose` etc).
- [ ] Performance: stable keys and memoization; virtualization or throttling when needed.
