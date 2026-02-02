# Ant Design v6 参考

## 适用场景边界
- 新项目或计划迁移到 `antd@^6` 的项目。
- React 18–19 范围内的应用（以官方文档为准）。
- 需要 token 主题、`classNames` / `styles` 定制、SSR 支持的场景。

## 推荐模式（1–2 种）
1. 主题与样式：优先使用 `ConfigProvider.theme` + token 体系，局部差异用 `classNames` / `styles`。
2. SSR：按官方方案组合 `ConfigProvider` 与 `StyleProvider`，并验证 hydration 与样式顺序。

## 必须避免的反模式
- 依赖 `.ant-*` 内部 class 或 DOM 结构做通用定制。
- 用大范围全局 CSS 覆盖替代 token 定制。
- SSR 只给概念，不提供可验证的落地点与检查点。

## 最小示例
```tsx
import { ConfigProvider } from "antd";

export default function App() {
  return (
    <ConfigProvider theme={{ token: { colorPrimary: "#1677ff" } }}>
      {/* app */}
    </ConfigProvider>
  );
}
```

## 与主 Skill 的回跳说明
- 当问题仅涉及“是否采用 v6、主题路径、SSR 方案选择”时，回到主 Skill 的决策链即可。

## 参考文档
- `https://ant.design/docs/react/introduce`
- `https://ant.design/docs/react/customize-theme`
- `https://ant.design/docs/react/server-side-rendering`
- `https://ant.design/docs/react/migration-v6`
