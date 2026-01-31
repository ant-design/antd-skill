# 表格（Table）复杂场景参考

## 适用范围

- 大数据量表格、虚拟滚动、固定列/表头
- 服务端排序/筛选/分页
- 行选择、可展开行、树形表格

## 关键原则

- **稳定的 `rowKey`**：默认使用 `key`，大型表格务必显式提供 `rowKey` 以避免渲染抖动。
- **受控变更统一入口**：分页、过滤、排序统一通过 `onChange(pagination, filters, sorter, extra)` 管理。
- **性能与布局**：固定列/表头或 `ellipsis` 会触发 `tableLayout="fixed"`。

## 常见实践

### 1. 服务端数据

- 使用 `onChange` 收集分页/排序/筛选参数，将请求结果写回 `dataSource`。
- `pagination={false}` 可关闭内置分页，完全由外部控制。

### 2. 行选择与批量操作

- `rowSelection` 控制选中项，`selectedRowKeys` 受控。
- `preserveSelectedRowKeys` 可在数据源变化时保留勾选状态。
- `rowSelection.type` 控制单选/多选。

### 3. 可展开行与树形表格

- `expandable` 提供 `expandedRowRender`、`expandedRowKeys`、`rowExpandable` 等能力。
- 树形表格使用 `childrenColumnName` 或 `dataSource` 的 `children` 结构。

### 4. 固定表头/列与滚动

- 使用 `scroll={{ x, y }}` 开启滚动。
- `sticky` 可让表头随页面滚动固定。
- 使用 `fixed` 配置列固定位置。

### 5. 虚拟滚动

- `virtual` 开启虚拟列表，适合大数据量。
- 若自定义 `components.body.*`，需使用 `React.forwardRef` 传递 ref，保证虚拟滚动计算正常。

## 常见问题与建议

- **列定义性能**：`columns` 建议用 `useMemo` 缓存，避免重复生成。
- **筛选 UI**：`filterDropdown` 适合自定义筛选面板；`filterSearch` 用于大列表检索。
- **响应式列**：`responsive` 配合断点控制列展示。

## 参考文档

- `https://ant.design/components/table`
