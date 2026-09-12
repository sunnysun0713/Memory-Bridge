# Memory Bridge

让 Claude Code 在任意项目、任意文件夹的会话中共享同一个中央记忆库 —— 跨项目集体记忆（Collective Memory）。

## 组成

| 组件 | 说明 |
|---|---|
| `skills/collective-memory/SKILL.md` | 技能本体：召回 / 沉淀 / 维护记忆的操作规程 |
| 中央记忆库（本机） | `~/.claude/global-memory/`，**永远不进任何 git 仓库** |
| 用户级 `~/.claude/CLAUDE.md` | 每次会话自动加载，保证「开工前召回、收工前沉淀」 |

## 安装

1. 把 `skills/collective-memory/` 复制到 `~/.claude/skills/collective-memory/`；
2. 在 `~/.claude/CLAUDE.md` 中追加：

````markdown
## 集体记忆库（所有项目通用）

中央记忆库：`~/.claude/global-memory/`（操作细则见 `/collective-memory` 技能）。

- **开工前**：读 `MEMORY.md` 索引 → 挑选与当前任务相关的记忆文件读取 → 按其指引工作；记忆与现状矛盾时以现状为准并更正记忆。
- **收工前**：有新经验 / 偏好 / 结论值得沉淀时，按技能规定的格式写入记忆库并更新索引。
- **禁止写入**：密码、API key、token 等敏感信息。
````

## 隐私边界（重要）

- 记忆数据只存在本机 `~/.claude/global-memory/`，**不要**把它提交到任何仓库；
- 记忆里**禁止**写入密码、API key、token 等凭据；
- 本仓库只包含技能文件本身，不包含任何记忆内容。

## 为什么不用「复制记忆到每个项目文件夹」

复制会产生多个副本：一旦某个项目被 push 到 GitHub，其他项目的记忆（可能含敏感信息）会随之泄露；副本之间还会版本分叉。中央文件夹是单一真相源。
