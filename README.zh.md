# Ant Design Skills

[English](README.md) | 简体中文

为 Ant Design 生态维护的 Agent Skills 集合。

## 安装

```bash
pnpx skills add ant-design/antd-skill
# or
npx skills add ant-design/antd-skill
```

## 技能列表

| Skill | 说明 | 目录 |
| --- | --- | --- |
| ant-design | antd v6 + Ant Design Pro 5 + Ant Design X v2 的决策指南 | `skills/ant-design/` |
| antd | 基于离线 Ant Design CLI 的 API 查询、排障、迁移与分析工作流 | `skills/antd/` |

## 使用方式

1. 阅读主 Skill：`skills/<skill>/SKILL.md`
2. 直接按该 `SKILL.md` 的单一 SOP 执行。

## 覆盖范围

- antd v6 + React 18–19
- Ant Design Pro 5 + ProComponents（布局、路由、权限、CRUD）
- Ant Design X v2（AI/Chat UI、流式输出、工具渲染）
- 含 antd v5 维护与迁移指引：`skills/ant-design/SKILL.md`

## 目录结构

- `skills/ant-design/`
- `skills/antd/`

## 基于官方文档整理的技能

每个 Skill 都是面向决策的指南，内容来自 Ant Design 生态官方文档，并以单一 `SKILL.md` 维护。

| 技能 | 描述 | 来源 |
| --- | --- | --- |
| ant-design | antd v6、Pro 5 + ProComponents、X v2 决策指南 | ant.design / pro.ant.design / procomponents.ant.design / x.ant.design |
| antd | 用于离线元数据和迁移任务的 Ant Design CLI 工作流 | @ant-design/cli |

## 常问问题

### 这个系列有何独特之处？

它专注于 Ant Design 项目的决策支持，而不是面向终端用户的教程。主 `SKILL.md` 保持简洁，并附带官方文档链接。

### 应该选择哪个技能？

使用 `ant-design` 处理核心 antd 组件、Pro 的布局/路由/权限/CRUD，以及 X 的 AI/Chat UI、流式状态与工具渲染。需要离线 `@ant-design/cli` 查询 API、执行 lint、做迁移或查看 changelog 时，使用 `antd`。

### 如何扩展？

Fork 此仓库，复制一个 skill 目录并更新 `SKILL.md`，同时更新两份 readme 的表格以保持目录准确。
