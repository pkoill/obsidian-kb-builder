# Obsidian KB Builder

面向 Claude Code 的 Agent Skill，用于构建和维护个人 Obsidian 知识库。

## 定位

本 Skill 面向使用 Obsidian 进行个人知识管理的用户，提供一套经过实际使用验证的知识库组织方法，涵盖目录结构、笔记分类、命名规范、写作原则、资源选择规则与健康检查。其目标是将零散的笔记沉淀为结构清晰、可长期复用、链接完整的知识系统。

## 功能特性

- **笔记二分法**：学习笔记（问题解决）与主题笔记（通用知识）的明确区分，以及两者之间的抽取判定标准；
- **规范命名**：顶级目录、学习笔记、主题笔记三类命名规则，避免 wikilink 断链；
- **写作方法论**：定义→原理→应用的三段式结构、类比先行的表达方式、知识密度自检标准；
- **资源选择规则**：参考资源与实操建议的分区、分层与条数约束，以及学习计划类笔记的特例；
- **计划类笔记结构**：步骤驱动，每步附学习资源与实操建议；
- **健康检查**：断链、孤立文件、重复待办、空任务等检查与修复流程；
- **Obsidian CLI 集成**：通过命令行高效完成搜索、反向链接、属性操作等。

## 前置依赖

本 Skill 依赖以下工具，**不随本 Skill 自动安装**，请按需自行安装：

| 依赖 | 用途 | 安装方式 |
|------|------|----------|
| [Obsidian CLI](https://obsidian.md/cli) | vault 搜索、反向链接、断链检查等命令行操作 | Obsidian 1.12.7+，设置 → 选项 → 高级 → 命令行界面 |
| [kepano/obsidian-skills](https://github.com/kepano/obsidian-skills) | Obsidian 语法、Canvas、Bases 的细粒度 Skill | `/plugin marketplace add kepano/obsidian-skills` |
| [Playwright MCP](https://github.com/microsoft/playwright-mcp) | Agent 浏览器自动化，用于网页搜索与内容提取 | `npx @playwright/mcp@latest` |

> 若运行时检测到缺少上述依赖，Agent 应先检查是否需要安装。

## 安装

本仓库以 Skill 形式发布，不依赖插件市场，克隆后手动复制即可：

```
git clone https://github.com/pkoill/obsidian-kb-builder
```

将克隆下来的 `skills/obsidian-kb-builder/` 目录（含 `SKILL.md` 与 `references/`）复制到 Claude Code 的 skills 目录：

- 用户级：`~/.claude/skills/obsidian-kb-builder/`
- 项目级：`.claude/skills/obsidian-kb-builder/`

## 用法

安装后，本 Skill 支持以下知识库操作：

| 操作 | 说明 |
|------|------|
| 创建学习笔记 | 问题驱动，先搜索后新建/并入 |
| 每周复盘 | 汇总进展、决策、沉淀、下周重点 |
| 快速捕获 | 把零散想法捕获到收件箱 |
| 搜索知识库 | 按关键词检索 |
| 健康检查 | 断链、孤立文件、重复待办、空任务 |

## 文件结构

```
obsidian-kb-builder/
├── .claude-plugin/
│   └── plugin.json              # Plugin 清单（name / description / author）
├── skills/
│   └── obsidian-kb-builder/
│       ├── SKILL.md             # Skill 主文件（核心原则 + 支持的操作 + 前置依赖）
│       └── references/
│           ├── structure.md     # 目录结构与命名规范
│           ├── writing.md       # 写作原则与笔记结构
│           ├── resources.md     # 资源选择规则
│           ├── operations.md    # 笔记创建/复盘/捕获/搜索操作流程
│           ├── cli.md           # Obsidian CLI 命令表
│           └── health-check.md  # 健康检查流程
├── README.md
└── LICENSE
```

## 设计说明

本 Skill 遵循 [Agent Skills 规范](https://agentskills.io/specification)，适用于任何兼容该规范的 Agent，包括 Claude Code、Codex 与 Open Code。

依赖处理遵循「声明依赖 + 缺失时提示 + 不自动安装」的原则，不静默安装任何工具。

## 许可

[MIT License](LICENSE)
