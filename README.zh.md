# Ant Design Skills

[English](README.md) | 简体中文

为 Ant Design 生态维护的 Agent Skills 与参考文档集合。

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

## 使用方式

1. 阅读主 Skill：`skills/<skill>/SKILL.md`
2. 复杂场景细节查阅：`skills/<skill>/references/*.md`

## 覆盖范围

- antd v6 + React 18–19
- Ant Design Pro 5 + ProComponents（布局、路由、权限、CRUD）
- Ant Design X v2（AI/Chat UI、流式输出、工具渲染）
- antd v5 维护与迁移见：`skills/ant-design/references/antd-v5.md`

## 目录结构

- `skills/ant-design/`

## 基于官方文档整理的技能

每个 Skill 都是面向决策的指南，内容来自 Ant Design 生态的官方文档，复杂细节放在 `skills/*/references/*.md`。

| 技能 | 描述 | 来源 |
| --- | --- | --- |
| ant-design | antd v6、Pro 5 + ProComponents、X v2 决策指南 | ant.design / pro.ant.design / procomponents.ant.design / x.ant.design |

## 常问问题

### 这个系列有何独特之处？

它专注于 Ant Design 项目的决策支持，而不是面向终端用户的教程。主 `SKILL.md` 保持简洁，复杂细节通过 `references/*.md` 补充，并附带官方文档链接。

### 应该选择哪个技能？

统一使用 `ant-design`：涵盖 antd 核心组件、Pro 布局/路由/权限/CRUD，以及 X 的 AI/Chat UI、流式状态与工具渲染。复杂场景请跳转对应的 `references/*.md`。

### 如何扩展？

Fork 此仓库，复制一个 skill 目录并更新 `SKILL.md` 与 `references/`，同时更新两份 readme 的表格以保持目录准确。
