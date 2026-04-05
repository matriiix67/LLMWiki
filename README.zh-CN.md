<p align="center">
  <a href="README.md">English</a> | <strong>简体中文</strong>
</p>

# BrainForge

一个 Claude Code 插件，让 LLM 从你收集的资料中渐进地构建和维护一个持久化知识 Wiki。

## 它做什么

不同于 RAG（每次查询都重新检索生成），BrainForge **将知识编译一次**，然后持续更新。你把原始资料——文章、论文、代码、PDF——放入文件夹，LLM 阅读它们，提取概念、实体和关系，然后写成结构化、互相链接的 Markdown wiki 页面。随着时间推移，wiki 成为一个可查询、可交叉引用、不断生长的活知识库。

## 三层架构

```
raw/          不可变的原始资料（用户管理，LLM 只读）
wiki/         知识 Wiki（LLM 拥有，结构化 Markdown 页面）
schema.md     模式配置（用户和 LLM 共同演进）
```

## 命令一览

每个命令都是子命令，通过 `/brainforge:<命令>` 调用：

| 命令 | 调用方式 | 说明 |
|------|----------|------|
| **初始化** | `/brainforge:init` | 创建目录结构和配置文件 |
| **摄入** | `/brainforge:ingest` | 阅读原始资料 → 讨论 → 写入 wiki |
| **查询** | `/brainforge:query` | 检索 wiki → 综合回答并标注引用 |
| **回填** | `/brainforge:archive` | 将有价值的查询输出整合回 wiki |
| **检查** | `/brainforge:lint` | 9 维度健康检查 + 自动修复建议 |
| **状态** | `/brainforge:status` | 知识库统计仪表盘 |

## 快速上手

1. **初始化**知识库：
   ```
   /brainforge:init
   ```
   创建目录结构，询问你定义领域。

2. **放入资料**到 `raw/` 文件夹——Markdown、PDF、代码、纯文本均可。

3. **摄入**一个文件：
   ```
   /brainforge:ingest raw/my-paper.pdf
   ```
   LLM 阅读资料，与你讨论关键要点，然后创建/更新 wiki 页面。使用 `/brainforge:ingest batch` 批量处理所有未编译文件。

4. **查询**知识库：
   ```
   /brainforge:query LoRA 和 QLoRA 的主要区别是什么？
   ```
   回答会通过 `[[wikilink]]` 引用具体 wiki 页面。

5. **回填**好的回答到 wiki：
   ```
   /brainforge:archive
   ```

6. **检查** wiki 健康状况：
   ```
   /brainforge:lint
   ```
   报告矛盾、断链、孤岛页面、缺失概念，并建议新的研究方向。

## Wiki 页面类型

| 类型 | 目录 | 用途 |
|------|------|------|
| **实体** | `wiki/entities/` | 人物、项目、产品、公司、工具 |
| **概念** | `wiki/concepts/` | 技术概念、理论、方法论 |
| **来源** | `wiki/sources/` | 每个原始文档的结构化摘要 |
| **分析** | `wiki/analyses/` | 对比分析、趋势分析、矛盾分析 |
| **主题** | `wiki/topics/` | 高层概述，某个研究方向的入口页 |

## 设计原则

- **更新而非追加** — 已有页面获得新信息时，重新综合整个页面，使其始终是该主题的最佳单一文档。
- **默认交互式** — 摄入时先与你讨论发现，再写入。批量模式是可选的快速通道。
- **查询会复利** — 好的问答输出可以回填到 wiki，探索和查询让知识库越用越强。
- **原始资料不可变** — LLM 永远不修改 `raw/` 中的源文件。
- **链接成网** — 每个页面使用 `[[wikilink]]` 双向导航，兼容 Obsidian。

## 安装

### 作为 Claude Code 插件

插件注册为 Claude Code 的 marketplace：

```
~/.claude/plugins/marketplaces/brainforge -> ~/.agents/skills/brainforge
```

在 `~/.claude/settings.json` 中启用：
```json
{
  "enabledPlugins": {
    "brainforge@brainforge": true
  }
}
```

## 文件结构

```
brainforge/
├── .claude-plugin/
│   └── plugin.json               # 插件清单
├── skills/
│   ├── init/SKILL.md             # /brainforge:init
│   ├── ingest/SKILL.md           # /brainforge:ingest
│   ├── query/SKILL.md            # /brainforge:query
│   ├── archive/SKILL.md          # /brainforge:archive
│   ├── lint/SKILL.md             # /brainforge:lint
│   └── status/SKILL.md           # /brainforge:status
├── references/
│   ├── architecture.md           # 共享架构与设计原则
│   ├── templates.md              # index.md, log.md, state.json 模板
│   └── schema-template.md        # schema.md 模板
├── README.md                     # English README
└── README.zh-CN.md               # 本文件
```

## 依赖

- Claude Code（Claude CLI）
- 无外部依赖——纯 LLM 文本处理，使用内置工具（Read、Write、Edit、Grep、Glob）

## 兼容性

- 兼容 Obsidian（wikilink、文件夹结构）
- 所有 wiki 内容都是纯 Markdown
- `schema.md` 人类可读可编辑
