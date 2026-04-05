# BrainForge Templates

> Used during init to generate initial files. Pick the section matching the user's chosen language.

---

## index.md — zh

```markdown
# 知识库索引

> 自动维护。最后更新：{timestamp}

## 统计

- 来源文档：0 | Wiki 页面：0 | 概念：0 | 实体：0 | 链接：0

## 主题

（暂无）

## 概念

| 名称 | 文件 | 简述 | 关联 |
|------|------|------|------|

## 实体

| 名称 | 类型 | 文件 | 简述 |
|------|------|------|------|

## 来源

| 原始文档 | 摘要页 | 涉及概念 | 摄入时间 |
|----------|--------|----------|----------|

## 分析

| 标题 | 文件 | 类型 | 涉及主题 |
|------|------|------|----------|
```

## index.md — en

```markdown
# Knowledge Base Index

> Auto-maintained. Last updated: {timestamp}

## Statistics

- Source documents: 0 | Wiki pages: 0 | Concepts: 0 | Entities: 0 | Links: 0

## Topics

(none yet)

## Concepts

| Name | File | Summary | Related |
|------|------|---------|---------|

## Entities

| Name | Type | File | Summary |
|------|------|------|---------|

## Sources

| Raw Document | Summary Page | Concepts | Ingested |
|--------------|--------------|----------|----------|

## Analyses

| Title | File | Type | Topics |
|-------|------|------|--------|
```

---

## log.md — zh

```markdown
# 操作日志

## [{date}] init | 知识库初始化
领域：{domain}
语言：{language}
```

## log.md — en

```markdown
# Operation Log

## [{date}] init | Knowledge base initialized
Domain: {domain}
Language: {language}
```

---

## state.json (language-independent)

```json
{
  "version": 1,
  "created": "{ISO timestamp}",
  "language": "{language code: zh/en/ja/...}",
  "files": {}
}
```

`files` records each processed raw file:

```json
{
  "files": {
    "raw/example.md": {
      "hash": "sha256:...",
      "ingestedAt": "{ISO timestamp}",
      "summaryPage": "wiki/sources/example-summary.md"
    }
  }
}
```
