# Ant Design CLI (v5)

Use this reference when the task involves Ant Design v5 component APIs, demos, docs, project analysis, or debugging and the local `@ant-design/cli` can answer it offline.

## Rules
- Check install first: `which antd || npm install -g @ant-design/cli`
- If any command prints an update notice, run `npm install -g @ant-design/cli` before continuing.
- Always use `--format json`.
- **Always pass `--version 5.x.x`** (matching the project's exact antd minor), unless `node_modules/antd` auto-detect already resolves to a v5 range. Without `--version`, the CLI may answer with v6 metadata that does not apply.
- Query before writing antd code. Do not guess props from memory.
- After changing antd code, run `antd lint` on the changed path.

## Core workflows

### Writing component code (v5)
1. `antd info Button --version 5.21.4 --format json`
2. `antd demo Button basic --version 5.21.4 --format json`
3. Optionally inspect styling hooks:
   - `antd semantic Button --version 5.21.4 --format json`
   - `antd token Button --version 5.21.4 --format json`

### Full docs
- `antd doc Table --version 5.21.4 --format json`
- `antd doc Table --version 5.21.4 --lang zh --format json`

### Debugging
1. `antd doctor --format json`
2. `antd info Select --version 5.12.0 --format json` (confirm prop existed in the project's exact minor)
3. `antd lint ./src/components/MyForm.tsx --format json`

### Upgrading to v6 (handoff)
1. `antd migrate 5 6 --format json` for the full checklist.
2. `antd migrate 5 6 --component <Name> --format json` for a single component.
3. `antd changelog 5.21.4 6.0.0 --format json` to read breaking changes between the project's current v5 and target v6.
4. After applying changes, re-run `antd lint` and switch the project to the `ant-design-v6` skill.

### Project analysis
- `antd usage ./src --version 5.21.4 --format json`
- `antd usage ./src --filter Form --version 5.21.4 --format json`
- `antd lint ./src --format json`
- `antd lint ./src --only deprecated --format json` (catches v4-era props still living in a v5 codebase)
- `antd lint ./src --only a11y --format json`
- `antd lint ./src --only performance --format json`

### Changelog and versions
- `antd changelog 5.22.0 --format json`
- `antd changelog 5.21.0..5.24.0 --format json`

### Component discovery
- `antd list --version 5.21.4 --format json`

## Bug reporting

### antd component bugs
Preview first, then ask the user before submitting. Include the exact v5 minor in the title.

```bash
antd bug --title "[v5.21.4] DatePicker crashes when selecting date" \
  --reproduction "https://codesandbox.io/s/xxx" \
  --steps "1. Open DatePicker 2. Click a date" \
  --expected "Date is selected" \
  --actual "Component crashes with error" \
  --format json
```

Submit only after confirmation by re-running with `--submit` (replace `--format json`).

### CLI bugs
Prepare a report whenever an `antd` command crashes, returns incorrect data, ignores `--version 5.x.x`, or is inconsistent with other commands.

```bash
antd bug-cli --title "antd info Button returns v6 props when --version 5.12.0 is set" \
  --description "Querying Button for version 5.12.0 returns props introduced in v6" \
  --steps "1. Run: antd info Button --version 5.12.0 --format json" \
  --expected "Props matching antd 5.12.0 Button API" \
  --actual "Output includes v6-only props" \
  --format json
```

Submit only after user confirmation (re-run with `--submit`).

## MCP mode
If the environment supports MCP, run the CLI as an MCP server pinned to the project's v5 minor:

```json
{
  "mcpServers": {
    "antd": {
      "command": "antd",
      "args": ["mcp", "--version", "5.21.4"]
    }
  }
}
```

This exposes structured Ant Design v5 knowledge tools through MCP without network access.
