# 选择器（Select）复杂场景参考

## 适用场景边界
- 远程搜索、异步加载选项
- 多选/标签模式、复杂渲染
- 大数据量下的虚拟滚动与可访问性

## 推荐模式（1–2 种）
- **搜索逻辑**：
  - `showSearch` 启用搜索输入。
  - 远程搜索建议设置 `showSearch` 且 `filterOption={false}`，在 `onSearch` 中发起请求。
- **选项数据**：
  - 使用 `options`（对象数组）比 JSX `Option` 具有更好性能。
  - 当使用 `options` 时，搜索字段应设置 `showSearch.optionFilterProp="label"`。
- **值结构**：
  - `labelInValue` 会将值变为 `{ value, label }` 结构，需要在业务层处理。

## 必须避免的反模式
- 远程搜索时仍开启本地过滤，导致结果被二次过滤。
- 选项数量大仍用 JSX `Option`，导致性能问题。
- 自定义 `suffixIcon` 可点击但阻断下拉打开。

## 常见实践

### 1. 多选与标签

- `mode="multiple" | "tags"` 开启多选/标签。
- `maxCount` 限制最大选中数量，`maxTagCount` 控制显示数量（`responsive` 会增加渲染成本）。
- `tokenSeparators` 用于 tags 模式的自动分词输入。

### 2. 自定义渲染

- `optionRender` 定制下拉选项渲染。
- `tagRender` 定制多选/标签的 tag 渲染。
- `popupRender` 可包裹自定义内容，需注意交互不应阻止下拉关闭逻辑。

### 3. 大数据与虚拟滚动

- 默认开启虚拟滚动，`virtual={false}` 可关闭。
- `popupMatchSelectWidth={false}` 会禁用虚拟滚动（注意性能）。
- 选项高度明显不同于默认值时，可使用内部参数 `listItemHeight` / `listHeight` 调整滚动体验（仅必要时使用）。

### 4. 可访问性

- 若需要屏幕阅读器完整访问列表，可设置 `virtual={false}`。
- 自定义 `suffixIcon` 时，若该图标需要点击，应处理 `pointer-events` 以避免阻断打开行为。

## 最小示例
```tsx
<Select
  showSearch
  filterOption={false}
  onSearch={(q) => fetchOptions(q)}
  options={options}
/>;
```

## 与主 Skill 的回跳说明
- 若问题只涉及“本地还是远程搜索”或“是否多选”，回到主 Skill 的组件选型规则。

## 参考文档

- `https://ant.design/components/select`
