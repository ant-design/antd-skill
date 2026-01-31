# Ant Design v6 参考

## 适用范围

- 适用于 `antd@^6` 的主线项目。
- React 18–19 是官方支持范围（以 `https://ant.design/docs/react/introduce` 为准）。
- 组件定制优先使用 `classNames` / `styles` 与 token 系统。

## 关键要点

- CSS‑in‑JS 与主题：使用 `@ant-design/cssinjs` 与 `ConfigProvider.theme`。
- 语义化 DOM：更多组件支持语义结构定制，避免全局 `.ant-*` 覆盖。
- SSR：支持 `@ant-design/cssinjs` 的 inline 提取与 `@ant-design/static-style-extract` 的全量导出。

## 迁移与兼容

- 从 v5 升级需按 `https://ant.design/docs/react/migration-v6` 执行。
- 兼容性问题优先查阅 FAQ 与组件文档的版本提示。

## 参考文档

- `https://ant.design/docs/react/introduce`
- `https://ant.design/docs/react/customize-theme`
- `https://ant.design/docs/react/server-side-rendering`
- `https://ant.design/docs/react/migration-v6`
