# BrainForge 架构

> 所有子命令共享的架构背景。每个命令的 SKILL.md 引用此文件。

## 核心理念

LLM 渐进地构建和维护一个持久化 wiki——结构化、互相链接的 Markdown 文件集合。知识只编译一次，然后持续更新，而不是每次查询都重新推导。

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

## 设计原则

1. **更新而非追加**：已有页面获得新信息时，重新综合整个页面，让它始终是该主题的最佳单一文档
2. **原始资料不可变**：raw/ 是事实来源，LLM 只读不改
3. **链接成网**：使用 `[[页面名]]` wikilink，每个页面都应有入链和出链
4. **日志可解析**：`## [{date}] {action} | {title}` 格式，支持 grep
5. **Schema 持续演进**：使用中发现更好的格式时，和用户一起更新 schema.md
6. **查询输出是知识资产**：好的问答应回填到 wiki，探索和查询在知识库中复利增长

## 命令总览

| 命令 | 调用方式 | 说明 |
|------|----------|------|
| **初始化** | `/brainforge:init` | 创建目录结构和初始文件 |
| **摄入** | `/brainforge:ingest` | 阅读原始资料 → 讨论 → 写入 wiki |
| **查询** | `/brainforge:query` | 检索 wiki → 深读 → 回答 |
| **回填** | `/brainforge:archive` | 将查询输出整合回 wiki |
| **检查** | `/brainforge:lint` | 9 维度健康检查 + 修复建议 |
| **状态** | `/brainforge:status` | 知识库统计概览 |
