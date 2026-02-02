# 树形控件（Tree）复杂场景参考

## 适用场景边界
- 异步加载节点（`loadData`）
- 勾选联动、严格勾选（`checkStrictly`）
- 大数据量、虚拟滚动、拖拽

## 推荐模式（1–2 种）
- **数据来源**：优先使用 `treeData`，无需手写 `TreeNode`。
- **字段映射**：通过 `fieldNames` 映射 `title` / `key` / `children` 字段。
- **默认属性仅初始化生效**：`defaultExpandAll` 等 `default*` 属性仅在初始化时生效，异步加载场景应使用 `expandedKeys` 受控。

## 必须避免的反模式
- 异步加载场景仍依赖 `defaultExpandAll`。
- 大数据量使用 `TreeNode` 手写结构，导致性能与维护成本上升。
- 忽视 `checkStrictly` 的数据结构差异。

## 常见实践

### 1. 异步加载

- 使用 `loadData` + `loadedKeys` 控制异步节点。
- 对于首次渲染为空的异步数据，建议数据加载后再渲染 `Tree`，以避免 `defaultExpandAll` 失效。

### 2. 勾选逻辑

- `checkable` + `checkedKeys` 控制勾选状态。
- `checkStrictly` 为 `true` 时，`checkedKeys` 结构为 `{ checked, halfChecked }`，父子节点互不联动。

### 3. 虚拟滚动与大数据

- `virtual` 默认启用，可通过 `virtual={false}` 关闭。
- 设置 `height` 开启虚拟滚动容器高度（开启后不支持横向滚动自适应）。

### 4. 拖拽与交互

- `draggable` 可全局启用或按节点控制。
- `allowDrop` 定义是否允许放置到目标节点。

## 常见问题与建议

- **禁用节点传导**：当节点为 `disabled`，勾选/展开状态不会向其父子节点传导。
- **虚拟滚动限制**：虚拟滚动仅渲染可视区域，超长标题可能需要额外样式处理。

## 最小示例
```tsx
<Tree
  treeData={data}
  loadData={onLoad}
  expandedKeys={expandedKeys}
  onExpand={setExpandedKeys}
/>;
```

## 与主 Skill 的回跳说明
- 若问题只涉及“是否需要异步或严格勾选”，回到主 Skill 的分流与组件选型规则。

## 参考文档

- `https://ant.design/components/tree`
