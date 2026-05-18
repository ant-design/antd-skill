# Ant Design Skills

[English](README.md) | 简体中文

为 Ant Design 生态维护的 Agent Skills 集合。

## 安装

### 方式一：`skills` CLI（推荐）

```bash
pnpx skills add ant-design/antd-skill
# or
npx skills add ant-design/antd-skill
```

会把 skill 目录拷贝到当前作用域的 `.claude/skills/` 下。

### 方式二：Claude Code CLI（手动安装）

Claude Code 会从以下两个位置发现 skill：

- **用户级** — `~/.claude/skills/<name>/`（所有会话可用）
- **项目级** — `<repo>/.claude/skills/<name>/`（仅当前项目可用，可提交到仓库共享给团队）

安装到用户级：

```bash
git clone https://github.com/ant-design/antd-skill.git /tmp/antd-skill
mkdir -p ~/.claude/skills
cp -R /tmp/antd-skill/skills/ant-design-v5 ~/.claude/skills/
cp -R /tmp/antd-skill/skills/ant-design-v6 ~/.claude/skills/
cp -R /tmp/antd-skill/skills/antd          ~/.claude/skills/
```

安装到单个项目：

```bash
mkdir -p .claude/skills
cp -R /tmp/antd-skill/skills/ant-design-v5 .claude/skills/
cp -R /tmp/antd-skill/skills/ant-design-v6 .claude/skills/
cp -R /tmp/antd-skill/skills/antd          .claude/skills/
```

通常只需要拷贝与项目匹配的版本 skill（`ant-design-v5` **或** `ant-design-v6`）。`antd` CLI skill 与版本无关，可与其中任意一个配合使用。

在 Claude Code 会话中确认：

```
/skills
```

列表里应能看到已安装的 skill（`ant-design-v5` 和/或 `ant-design-v6`，以及 `antd`）。版本 skill 会根据项目 `package.json` 里 antd 的主版本号自动命中，`antd` CLI skill 对任意 antd 相关任务都会触发。

后续升级：重新拉取仓库再覆盖；或把 `~/.claude/skills/<name>` 改为本地 clone 的软链。

## 技能列表

| Skill | 说明 | 目录 |
| --- | --- | --- |
| ant-design-v5 | antd 5.x + Ant Design Pro 5 + Ant Design X v2 决策指南（CSS-in-JS、SSR、React 19 兼容包） | `skills/ant-design-v5/` |
| ant-design-v6 | antd 6.x + Ant Design Pro 5 + Ant Design X v2 决策指南 | `skills/ant-design-v6/` |
| antd | 基于离线 Ant Design CLI 的 API 查询、排障、迁移与分析工作流（v4/v5/v6） | `skills/antd/` |

两个 `ant-design-v*` skill 充当版本路由：各自在 `description` 与 `SKILL.md` 顶部声明支持的 antd 主版本，Claude 会根据项目 `package.json` 选用对应的那份。

## 使用方式

1. 阅读主 Skill：`skills/<skill>/SKILL.md`
2. 直接按该 `SKILL.md` 的单一 SOP 执行。

## 覆盖范围

- antd 5.x（React 16.9–18，借助 `@ant-design/v5-patch-for-react-19` 可支持 React 19）
- antd 6.x（React 18–19）
- Ant Design Pro 5 + ProComponents（布局、路由、权限、CRUD）—— 两个版本 skill 均可使用
- Ant Design X v2（AI/Chat UI、流式输出、工具渲染）—— 两个版本 skill 均可使用
- `@ant-design/cli` 的 v4/v5/v6 离线工作流由 `antd` skill 覆盖

## 目录结构

- `skills/ant-design-v5/`
- `skills/ant-design-v6/`
- `skills/antd/`

## 基于官方文档整理的技能

每个 Skill 都是面向决策的指南，内容来自 Ant Design 生态官方文档，并以单一 `SKILL.md` 维护。

| 技能 | 描述 | 来源 |
| --- | --- | --- |
| ant-design-v5 | antd 5.x、Pro 5 + ProComponents、X v2 决策指南 | 5x.ant.design / pro.ant.design / procomponents.ant.design / x.ant.design |
| ant-design-v6 | antd 6.x、Pro 5 + ProComponents、X v2 决策指南 | ant.design / pro.ant.design / procomponents.ant.design / x.ant.design |
| antd | 用于 v4/v5/v6 离线元数据和迁移任务的 Ant Design CLI 工作流 | @ant-design/cli |

## 常问问题

### 这个系列有何独特之处？

它专注于 Ant Design 项目的决策支持，而不是面向终端用户的教程。主 `SKILL.md` 保持简洁，并附带官方文档链接。

### 应该选择哪个技能？

按项目 antd 主版本来选：
- antd 5.x → `ant-design-v5`（覆盖 v5 的 CSS-in-JS、SSR、React 19 兼容包、Pro 5、X v2）。
- antd 6.x → `ant-design-v6`（覆盖 v6 的 token/SSR、Pro 5、X v2）。

需要离线 `@ant-design/cli` 查询 API、执行 lint、做迁移（`antd migrate 5 6`）或查看 changelog 时，把 `antd` 与上述版本 skill 一起装上即可。每份版本 skill 在 `SKILL.md` 顶部都内置了"版本判定"段落，Claude 会先确认项目 antd 版本再给建议。

### 如何扩展？

Fork 此仓库，复制一个 skill 目录并更新 `SKILL.md`，同时更新两份 readme 的表格以保持目录准确。

### 如何在 Claude Code 中使用？

把需要的 skill 目录拷贝到 `~/.claude/skills/`（用户级）或 `<repo>/.claude/skills/`（项目级），在 Claude Code 会话中执行 `/skills` 查看是否已加载。命中 `description` 中的触发条件时会自动启用。
