---
name: query
description: "Use when user wants to search and ask questions against the knowledge wiki. Triggers: '查询', 'query', '问', or any direct question about knowledge base content."
argument-hint: "[question]"
---

# BrainForge Query

检索知识库并综合回答问题。

**共享架构参考**：[../../references/architecture.md](../../references/architecture.md)

## 执行步骤

### Step 1：检索

1. 读取 `wiki/index.md`，关键词匹配相关页面
2. `Grep` 工具搜索 wiki/ 目录辅助查找
3. 确定 Top 5-10 个相关页面

### Step 2：深读

1. 读取筛选出的页面全文
2. 内容过多时进一步精筛

### Step 3：回答

- 严格基于 wiki 内容，标注引用来源 → `[[页面名]]`
- 多文档涉及时综合分析异同
- 信息不足时说明并**建议可补充的资料方向**

### Step 4：保存与回填建议

- 保存到 `output/queries/{date}-{slug}.md`
- 追加 log.md：`## [{date}] query | {question}`
- **主动判断**：如果回答包含有价值的综合分析，建议用户使用 `/brainforge:archive` 回填
