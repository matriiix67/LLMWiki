---
description: "Use when user wants to check knowledge base health and find issues. Triggers: '检查', 'lint', '体检', 'health check', '知识库检查'."
---

# BrainForge Lint

对知识库执行 9 维度健康检查。

**共享架构参考**：[../../references/architecture.md](../../references/architecture.md)

## 检查维度（9 项）

1. **矛盾检测**：同一概念在不同页面的矛盾描述
2. **过时结论**：被更新资料取代的旧结论
3. **断链**：`[[wikilink]]` 指向不存在的页面
4. **孤岛页面**：没有入链的页面
5. **缺失页面**：被多次提及但没有专属页面的重要概念
6. **深度不足**：页面内容过于简略
7. **交叉引用缺失**：明显相关但未链接的页面
8. **索引偏差**：index.md 与实际文件不一致
9. **研究建议**：基于知识库空白，主动建议新的研究问题和资料来源

## 输出

- 生成 `wiki/_HEALTH_REPORT.md`（评分 + 问题清单 + 增强建议）
- 追加 log.md：`## [{date}] lint | 评分 {score}/100, {n} 个问题`

## 自动修复项

以下问题可直接修复（执行前询问用户确认）：

| 问题 | 修复方式 |
|------|----------|
| 断链 | 创建 stub 页面 |
| 索引偏差 | 重建 index.md |
| 缺失页面 | 生成初始内容 |
