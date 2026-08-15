# Obsidian CLI 命令表

Obsidian CLI 让 agent 用命令行操作运行中的 Obsidian vault，比文件读写/Grep 更快更准（走 Obsidian 的索引）。

## 前置条件

1. Obsidian **installer 版本 ≥ 1.12.7**；
2. 已在 Obsidian 内启用：设置 → 选项 → 高级 → **命令行界面**；
3. **Obsidian 应用必须正在运行**（CLI 连接到运行中的实例）；
4. 启用后 `obsidian` 命令注册进用户 PATH（重启终端生效）。

> Windows 上 `obsidian` 命令对应安装目录下的 `Obsidian.com`（终端重定向器）；若 PATH 未刷新，可用完整路径调用。

## 目标定位

- 默认目标 = 最近聚焦的 vault；用 `vault=<name>` 指定；
- `file=<name>` 按 wikilink 规则解析（只写名字，不写路径/扩展名）；`path=<path>` 写完整路径。

## 知识库健康检查常用命令

| 命令 | 作用 | 例子 |
|------|------|------|
| `unresolved` | 列出断链（指向不存在笔记的 wikilink） | `obsidian unresolved verbose` |
| `orphans` | 列出孤儿文件（无反向链接） | `obsidian orphans` |
| `deadends` | 列出死胡同文件（无外向链接） | `obsidian deadends` |
| `backlinks` | 查某文件的反向链接 | `obsidian backlinks file="6. 笔记名"` |
| `links` | 查某文件的外向链接 | `obsidian links file="笔记名"` |

> 迁移/改名笔记后必做：`unresolved` 应为空；`orphans` 应只剩「首页、个人档案、附件、README」等本就不该被链接的文件。

## 内容操作命令

| 命令 | 作用 | 例子 |
|------|------|------|
| `search` | 全库搜索 | `obsidian search query="关键词" limit=10` |
| `search:context` | 带上下文搜索（grep 风格） | `obsidian search:context query="关键词"` |
| `read` | 读文件内容 | `obsidian read file="笔记名"` |
| `create` | 创建文件 | `obsidian create name="新笔记" content="# 标题"` |
| `append` / `prepend` | 追加/前置内容 | `obsidian append file="笔记" content="新行"` |
| `rename` / `move` | 改名/移动（自动更新内链，若开启） | `obsidian rename file="旧名" name="新名"` |

## 属性操作命令

| 命令 | 作用 | 例子 |
|------|------|------|
| `property:read` | 读属性 | `obsidian property:read name="status" file="笔记"` |
| `property:set` | 设属性 | `obsidian property:set name="status" value="evergreen（常青）" file="笔记"` |
| `properties` | 列出 vault 所有属性 | `obsidian properties sort=count` |

## 任务操作命令

| 命令 | 作用 | 例子 |
|------|------|------|
| `tasks` | 列出任务 | `obsidian tasks todo`（未完成）、`verbose`（按文件分组带行号） |
| `task` | 操作单个任务 | `obsidian task ref="笔记.md:8" toggle` |

> 检查重复待办：`obsidian tasks todo verbose` 后比对同一描述是否在多个文件出现。

## 其它常用命令

| 命令 | 作用 |
|------|------|
| `vault` / `vaults` | 库信息 / 列出已知库 |
| `tags` | 列出标签及计数 |
| `files` / `folders` | 列出文件 / 文件夹 |
| `diff` / `history` | 文件版本历史对比 |
| `templates` / `template:read` | 列出/读模板 |

完整命令列表用 `obsidian help` 查看（始终最新）。
