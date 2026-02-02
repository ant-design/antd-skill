# 上传（Upload）复杂场景参考

## 适用场景边界
- 受控文件列表、断点/自定义上传流程
- 图片预览、拖拽上传、目录上传
- 与业务接口深度整合（自定义请求、进度、鉴权）

## 推荐模式（1–2 种）
- **受控与非受控**：
  - 使用 `defaultFileList` 进行非受控初始值。
  - 使用 `fileList` + `onChange` 完全受控。
- **上传前拦截**：`beforeUpload` 返回 `false` 或 reject 可以阻止上传；返回 `Upload.LIST_IGNORE` 会忽略该文件，不进入列表。
- **自定义请求**：使用 `customRequest` 接管默认 XHR 行为，可通过 `info.defaultRequest` 调用默认上传逻辑。

## 必须避免的反模式
- 受控 `fileList` 不同步 `onChange`，导致 UI 与状态不一致。
- `beforeUpload` 返回 `false` 后仍假定 `info.file` 结构固定。
- 自定义上传不处理失败与重试路径。

## 常见实践

### 1. 受控列表管理

- `onChange` 会在上传中、完成、失败阶段多次触发。
- `fileList` 以最新列表为准，删除或过滤列表时注意同步状态。

### 2. 手动或自定义上传

- `beforeUpload` 返回 `false` 可阻止自动上传，配合业务按钮手动触发。
- `customRequest` 可接入自定义上传 SDK 或分片上传。

### 3. 图片与预览

- `listType="picture-card" | "picture" | "picture-circle"` 配合预览。
- `previewFile` 可自定义预览生成逻辑（如转为 dataURL）。

### 4. 安全与兼容

- `withCredentials` 控制跨域携带 Cookie。
- `directory` 可上传目录（浏览器支持需注意）。
- `accept` 或 `AcceptObject` 限制文件类型，必要时加入自定义过滤逻辑。

## 常见问题与建议

- **受控列表不更新状态**：`onChange` 仅对存在于列表中的文件生效，被移除的文件不会触发后续状态变更。
- **返回 File 结构兼容**：`beforeUpload` 返回 `false` 时，`info.file` 是 Upload 组件包装后的对象，建议统一使用 `info.file.originFileObj` 来获取原始的 `File` 对象。
- **禁用状态一致性**：自定义 `Upload` 子元素时需要同步传递 `disabled`。

## 最小示例
```tsx
const [fileList, setFileList] = useState([]);

<Upload
  fileList={fileList}
  onChange={({ fileList: next }) => setFileList(next)}
  beforeUpload={() => false}
>
  <Button>Upload</Button>
</Upload>;
```

## 与主 Skill 的回跳说明
- 若问题只涉及“是否受控/是否 customRequest”，回到主 Skill 的组件选型规则。

## 参考文档

- `https://ant.design/components/upload`
