---
name: ant-design
description: Ant Design ecosystem guidance covering antd 6.x, Ant Design Pro 5/ProComponents, and Ant Design X v2 (AI/chat UI). Use when making component/layout decisions, theming/tokens, SSR, routing/access, CRUD patterns, or AI chat UI integrations.
---

# Ant Design

## S - Scope
- Target: antd@^6 with React 18-19, plus ant-design-pro@^5 / @ant-design/pro-components and @ant-design/x@^2 when applicable.
- Cover: core components, theming/tokens, css-in-js, SSR, a11y, performance, Pro layouts/routing/access/CRUD, and X (AI/chat UI) patterns.
- Avoid: undocumented APIs, internal `.ant-*` class coupling, or cross-version mixing without explicit request.

### Default assumptions (when not specified)
- Language: TypeScript.
- Styling: prefer tokens, `classNames`, and `styles`; avoid global overrides.
- Provider: a single `ConfigProvider` at app root, unless isolation is required.
- Dependencies: do not add new packages unless required or requested.

### Scope rules (must follow)
- Use only officially documented antd APIs and patterns.
- Do not invent props, events, or component names.
- Use only officially documented Pro/X APIs and patterns.
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
- Pro layouts, route-driven menus, or access control (Layout/Access).
- ProTable/ProForm with request coupling, dynamic fields, or perf tuning.
- X streaming, tool rendering, or Markdown extensions beyond the defaults.

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
Pro v5 | Pro 5 scope and baseline guidance | `references/pro-v5.md`
Pro layout | Layouts, menus, access, multi-layout patterns | `references/pro-layout-advanced.md`
ProTable | Query/table coupling, request patterns, perf | `references/protable-advanced.md`
ProForm | Step forms, dynamic fields, table linkage | `references/proform-advanced.md`
X v2 | X v2 scope and baseline guidance | `references/x-v2.md`
X components | Message/tool component patterns | `references/x-components-advanced.md`
X SDK | Streaming integration and state model | `references/x-sdk-advanced.md`
X Markdown | X Markdown extensions and rendering | `references/x-markdown-advanced.md`

### Reference routing rule
- Do not expand advanced topics in the main skill.
- Jump to a `Reference` if any condition matches:
  - More than 3 interaction states.
  - Async flows or large data sets.
  - Virtualization or performance tuning.
  - Complex accessibility requirements.

## P - Process
### 1) Identify the layer first
- Core antd UI, Pro admin app, or X chat/agent UI?
- If Pro or X is involved, route to the relevant `Reference` when complexity triggers match.

### 2) Clarify context before advising
- Framework and rendering: Next.js / Umi / Vite? CSR / SSR / streaming?
- antd version: confirm v6 if unclear.
- Theming depth: small token changes or component-level overrides?
- Data scale: large lists/tables/trees/selects?
- Interaction complexity: controlled state, linkage, async, auth, upload flows?

### 3) Provider minimal set
- CSR: usually `ConfigProvider` only.
- SSR or strict style order: add `StyleProvider` as per `references/antd-v6.md`.
- One app, one root provider; local themes only for isolation needs.

### 4) Component selection rules (core antd)
- Form: prefer `Form` as source of truth unless external state is required.
- Overlay: `Modal` for blocking flows; `Drawer` for side context or long content.
- Lists: structured data uses `Table`, light lists use `List`; `Table` needs stable `rowKey`.
- Large data: use virtualization (see `references/table-advanced.md`).
- Select: local filter uses `filterOption`; remote search uses `showSearch` + `filterOption={false}` + `onSearch` (see `references/select-advanced.md`).
- Upload: controlled flow uses `fileList`; complex flow uses `customRequest` (see `references/upload-advanced.md`).

### 5) Pro decision shortcuts (when Pro is in scope)
- Routes are the menu source of truth; avoid hand-built menus.
- Access control is page-first; UI hides are secondary; backend still enforces.
- CRUD uses ProTable/ProForm schemas as the source of truth (see Pro references).

### 6) X decision shortcuts (when X is in scope)
- Model messages/tools as serializable data; JSX is a pure view.
- Streaming needs stable keys, throttled updates, and scroll management (see X references).

### 7) Theming decision chain
1. Use global tokens for most cases.
2. Use component tokens or `classNames`/`styles` for differences.
3. Only if unavoidable, use scoped CSS overrides and state the risk.
4. Never rely on global `.ant-*` overrides.

### 8) Shunt complexity to `Reference`
- If any complex trigger matches, provide decision + minimal skeleton + `Reference` path.
- Details live in the corresponding `references/*.md`.

### 9) a11y and performance checks
- a11y: keyboard access, focus management for overlays, icon buttons with `aria-label`, not color-only states.
- perf: stable keys, memoized columns, avoid frequent setState, use virtualization and throttling as needed.

## O - Output
### Output should include (as needed)
- Component and layout recommendations with 1-3 sentence rationale.
- Minimal provider and theming strategy.
- SSR, perf, and a11y risks with concrete mitigations.
- Pro: route/layout plan, access model, and ProTable/ProForm schema when relevant.
- X: message/tool schema and streaming state model when relevant.
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
- [ ] Pro: route-driven menus/access are consistent with backend enforcement.
- [ ] X: streaming state, stop/retry, and tool rendering are deterministic.
