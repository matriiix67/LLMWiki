---
description: "Use when user wants to create a new knowledge base. Triggers: '初始化知识库', 'init kb', 'create knowledge base', '新建知识库'."
argument-hint: "[path]"
---

# BrainForge Init

Initialize a new BrainForge knowledge base.

**Shared architecture**: [../../references/architecture.md](../../references/architecture.md)

## Steps

1. Determine KB path (user-specified or current directory)
2. **Ask user two questions via AskUserQuestion** (in a single call):
   - **Domain**: What is this knowledge base about? (e.g. "AI research", "A股短线交易")
   - **Language**: Which language for wiki pages? Options: `简体中文 (Recommended)`, `English`, `日本語`, or user-specified
3. Create directory structure:
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
4. Generate `wiki/index.md` — use the matching language section from [../../references/templates.md](../../references/templates.md)
5. Generate `wiki/log.md` — write init record in the chosen language
6. Generate `schema.md` — use the matching language section from [../../references/schema-template.md](../../references/schema-template.md), fill in domain and language
7. Generate `.brainforge/state.json`
8. Show completion message in the user's language:

**zh:**
```
知识库已初始化完成！

下一步：
1. 将原始资料放入 raw/ 目录
2. 使用 /brainforge:ingest 摄入资料
3. 使用 /brainforge:status 查看状态
```

**en:**
```
Knowledge base initialized!

Next steps:
1. Add source materials to raw/
2. Use /brainforge:ingest to process them
3. Use /brainforge:status to check stats
```
