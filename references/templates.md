# BrainForge 模板

> 初始化知识库时使用这些模板生成初始文件。

## index.md 模板

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

## log.md 模板

每条记录格式 `## [{date}] {action} | {title}`，支持 grep/tail。

```markdown
# 操作日志

## [{date}] init | 知识库初始化
领域：{domain}
```

## state.json 模板

```json
{
  "version": 1,
  "created": "{ISO timestamp}",
  "files": {}
}
```

`files` 对象记录每个已处理的原始文件：

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
