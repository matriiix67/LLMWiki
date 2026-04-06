---
description: "Use when user wants to see knowledge base statistics and recent activity. Triggers: '状态', 'status', '知识库状态', 'kb status'."
---

# BrainForge Status

显示知识库统计概览。

**共享架构参考**：[../../references/architecture.md](../../references/architecture.md)

## 执行步骤

1. 读取 wiki/ 目录，统计各类型页面数量
2. 用 Grep 统计 `[[wikilink]]` 总数
3. 对比 `raw/` 和 `.brainforge/state.json`，计算待摄入文件
4. 读取 `wiki/log.md` 最后 3 条记录

## 输出格式

```
知识库状态
━━━━━━━━━━━━━━━━━━━━
来源文档：{n} 篇
Wiki 页面：{n}（概念 {n} | 实体 {n} | 来源 {n} | 分析 {n} | 主题 {n}）
链接总数：{n}
待摄入：{n} 个新文件
最近操作：
  {last 3 log entries}
```
