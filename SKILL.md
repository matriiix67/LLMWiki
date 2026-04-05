---
name: brainforge
description: "Use when user wants to build, maintain, or query a persistent knowledge wiki from collected materials. Triggers: '初始化知识库', 'init kb', '摄入', 'ingest', '处理这个文件', '读一下这篇', '批量摄入', 'batch ingest', '查询', 'query', '回填', 'archive', '归档', '检查', 'lint', '体检', '状态', 'status', or any request to organize research materials into a structured, interlinked wiki."
---

# BrainForge — LLM 知识库

LLM 渐进地构建和维护一个持久化 wiki——结构化、互相链接的 Markdown 文件集合。知识只编译一次，然后持续更新，而不是每次查询都重新推导。

## 何时使用

- 用户想把收集的资料（文章、论文、代码）组织成结构化知识库
- 用户提到"知识库"、"wiki"、"摄入"、"ingest"等关键词
- 用户想对已积累的资料进行交叉查询和综合分析
- 用户想检查知识库的健康状况

**不适用**：一次性翻译、简单问答、不需要持久化的临时分析

## 三层架构

```
raw/          原始资料（不可变，用户管理，LLM 只读）
wiki/         知识 Wiki（LLM 完全拥有，创建/更新/维护）
schema.md     模式配置（用户和 LLM 共同演进）
```

## 知识库目录结构

```
{kb}/
├── raw/                        # 原始资料
├── wiki/
│   ├── index.md                # 内容索引
│   ├── log.md                  # 时间线日志（只追加）
│   ├── entities/               # 人物、项目、产品、公司
│   ├── concepts/               # 技术概念、理论、方法论
│   ├── sources/                # 每个原始文档的摘要
│   ├── analyses/               # 对比、综合、趋势分析
│   └── topics/                 # 研究方向的全局概述
├── output/
│   ├── queries/                # 问答记录
│   ├── reports/                # 报告
│   └── archived/               # 已回填的输出
├── schema.md                   # 模式配置
└── .brainforge/
    └── state.json              # 编译状态（文件 hash）
```

## 命令速查

| 命令 | 触发词 | 说明 |
|------|--------|------|
| **初始化** | `初始化知识库` / `init kb` | 创建目录结构和初始文件 |
| **摄入** | `摄入` / `ingest` / `处理这个文件` | 阅读原始资料 → 讨论 → 写入 wiki |
| **批量摄入** | `批量摄入` / `batch ingest` | 自动处理所有未编译文件 |
| **查询** | `查询` / `query` / 直接提问 | 检索 wiki → 深读 → 回答 |
| **回填** | `回填` / `归档` / `archive` | 将查询输出整合回 wiki |
| **检查** | `检查` / `lint` / `体检` | 9 维度健康检查 + 修复建议 |
| **状态** | `状态` / `status` | 知识库统计概览 |

每个命令的详细步骤见 [references/commands.md](references/commands.md)。

## 执行任何命令前

1. 确定知识库根目录（通常是当前工作目录，或用户指定的路径）
2. 检查 `schema.md` 是否存在（不存在说明未初始化）
3. 如果是初始化命令，读取 [references/templates.md](references/templates.md) 和 [references/schema-template.md](references/schema-template.md) 获取模板

## 关键设计原则

1. **更新而非追加**：已有页面获得新信息时，重新综合整个页面，让它始终是该主题的最佳单一文档
2. **摄入时保持参与**：默认交互式，先讨论再写入。批量模式是可选的快速通道
3. **查询输出是知识资产**：好的问答应回填到 wiki，探索和查询在知识库中复利增长
4. **原始资料不可变**：raw/ 是事实来源，LLM 只读不改
5. **日志可解析**：`## [{date}] {action} | {title}` 格式，支持 grep
6. **Schema 持续演进**：使用中发现更好的格式时，和用户一起更新 schema.md
7. **链接成网**：使用 `[[页面名]]` wikilink，每个页面都应有入链和出链
