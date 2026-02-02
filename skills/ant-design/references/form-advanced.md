# 表单（Form）复杂场景参考

## 适用场景边界
- 动态表单（`Form.List`）、多级嵌套 `name`、跨字段联动校验
- 复杂校验与性能优化（`dependencies` / `shouldUpdate` / `Form.useWatch`）
- 表单值由外部状态管理驱动（受控 `fields` / `form.setFieldsValue`）

## 推荐模式（1–2 种）
- **表单作为数据源**：不要在每个表单控件上用 `value` 或 `defaultValue` 管理值，而是通过 `Form` 的 `initialValues` 或 `form.setFieldsValue` 进行。`initialValues` 不能通过 `setState` 动态更新。
- **增量更新**：Form 只更新改动的字段。若需要实时渲染依赖值，用 `Form.useWatch` 或 `Form.Item` 的 `renderProps`。
- **依赖优先**：字段间联动优先用 `dependencies`。`dependencies` 不建议与 `shouldUpdate` 同时使用，避免更新逻辑冲突。

## 必须避免的反模式
- 在控件上混用 `value`/`defaultValue` 与 Form 管理。
- 动态表单靠 `setState` 直接改 `initialValues`。
- 同时使用 `dependencies` 和 `shouldUpdate` 做同一联动。

## 常见实践

### 1. 动态字段

- 使用 `Form.List` 生成动态字段组。
- 用 `name` 的数组路径表达嵌套结构，例如 `name={['user', 'address', 'city']}`。
- 对于需要纯粹控制校验与数据、不渲染额外 DOM 的场景，用 `Form.Item` 的 `noStyle`。

### 2. 跨字段校验与联动

- `dependencies`: 当上游字段变化时自动触发校验/更新。
- `shouldUpdate`: 仅在需要自定义渲染逻辑时使用，且子节点必须是函数。

### 3. 观察字段变化

- `Form.useWatch(namePath, form)`：监听字段值，适用于请求联动、联想搜索等场景。
- 当组件被 `Form.Item` 包裹时可省略 `form` 参数。
- 监听未注册字段需要 `Form.useWatch('field', { form, preserve: true })`。

### 4. 表单实例与上下文

- `Form.useForm()` 创建实例，通过 `form` 传递给 `<Form form={form}>`。
- `Form.useFormInstance()` 从上下文获取实例，避免层层传参。

### 5. 值映射与规范化

- `valuePropName`：处理非 `value` 的受控字段（如 `Switch` / `Checkbox`）。
- `getValueFromEvent`：自定义从事件提取值的逻辑。
- `normalize`：同步规范化输入（不支持异步）。

## 常见问题与建议

- **初始化与重置**：`initialValues` 仅在初始化或 `form.resetFields()` 时生效；动态初始值用 `setFieldsValue`。
- **隐藏字段**：`hidden` 字段仍会收集与校验；移除字段后是否保留值由 `preserve` 控制。
- **校验节奏**：`validateTrigger`、`validateDebounce`、`validateFirst` 组合使用以控制体验与性能。
- **统一文案**：使用 `Form` 的 `validateMessages` 或 `ConfigProvider` 的 `form.validateMessages` 统一校验提示。

## 最小示例
```tsx
const [form] = Form.useForm();

<Form form={form} initialValues={{ type: "A" }}>
  <Form.Item name="type">
    <Select options={[{ value: "A" }, { value: "B" }]} />
  </Form.Item>
  <Form.Item dependencies={["type"]} noStyle>
    {({ getFieldValue }) =>
      getFieldValue("type") === "B" ? (
        <Form.Item name="extra" rules={[{ required: true }]}>
          <Input />
        </Form.Item>
      ) : null
    }
  </Form.Item>
</Form>
```

## 与主 Skill 的回跳说明
- 若问题仅是“是否让 Form 托管”或“是否需要外部状态”，回到主 Skill 的决策链即可。

## 参考文档

- `https://ant.design/components/form`
