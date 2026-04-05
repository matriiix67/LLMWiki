---
name: archive
description: "Use when user wants to feed query outputs or analysis results back into the wiki. Triggers: '回填', '归档', 'archive', '把这个查询写回 wiki'."
argument-hint: "[output file path]"
---

# BrainForge Archive

将查询输出或分析结果整合回 wiki，让知识复利增长。

**共享架构参考**：[../../references/architecture.md](../../references/architecture.md)

## 执行步骤

1. 读取指定的 output 文件（或最近一次查询输出）
2. 分析包含的新洞察和联系
3. 整合到 wiki：
   - 更新相关概念页面
   - 创建新分析页面（如果有新的对比或综合）
   - 更新主题叙述
4. 更新 `wiki/index.md`
5. 移动原文件到 `output/archived/`
6. 追加 log.md：`## [{date}] archive | {标题}`

## 关键原则

- **更新而非追加**：已有页面获得新信息时，重新综合整个页面
- 回填后原文件移入 `output/archived/`，不删除
