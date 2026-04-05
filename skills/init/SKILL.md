---
name: init
description: "Use when user wants to create a new knowledge base. Triggers: '初始化知识库', 'init kb', 'create knowledge base', '新建知识库'."
argument-hint: "[path]"
---

# BrainForge Init

初始化一个新的 BrainForge 知识库。

**共享架构参考**：[../../references/architecture.md](../../references/architecture.md)

## 执行步骤

1. 确定知识库路径（用户指定或当前目录）
2. 创建完整目录结构：
   ```
   {kb-path}/
   ├── raw/
   ├── wiki/
   │   ├── entities/
   │   ├── concepts/
   │   ├── sources/
   │   ├── analyses/
   │   └── topics/
   ├── output/
   │   ├── queries/
   │   ├── reports/
   │   └── archived/
   └── .brainforge/
   ```
3. 生成 `wiki/index.md`（读取 [../../references/templates.md](../../references/templates.md) 中的模板）
4. 生成 `wiki/log.md`（写入初始化记录）
5. 生成 `schema.md`（读取 [../../references/schema-template.md](../../references/schema-template.md)，用 AskUserQuestion 询问用户填写领域）
6. 生成 `.brainforge/state.json`
7. 提示用户将原始资料放入 `raw/`

## 初始化后提示

```
知识库已初始化完成！

下一步：
1. 将原始资料放入 raw/ 目录
2. 使用 /brainforge:ingest 摄入资料
3. 使用 /brainforge:status 查看状态
```
