---
name: ingest
description: "Use when user wants to process raw materials into the knowledge wiki. Triggers: '摄入', 'ingest', '处理这个文件', '读一下这篇', '批量摄入', 'batch ingest', '处理 raw 目录'."
argument-hint: "[file path or 'batch']"
---

# BrainForge Ingest

将原始资料编译为结构化的 wiki 页面。

**共享架构参考**：[../../references/architecture.md](../../references/architecture.md)

## 前置检查

1. 确认知识库已初始化（`schema.md` 存在）
2. 读取 `schema.md` 了解领域和约定
3. 读取 `wiki/index.md` 了解已有知识结构

## 模式 A：交互式摄入（默认）

### Step 1：阅读与讨论

1. 读取指定的原始文件（按文件预处理规则）
2. **与用户讨论**关键要点：
   - 总结核心内容
   - 指出与已有知识的关联或矛盾
   - 询问用户希望重点关注哪些方面
   - 等待用户反馈后再继续

### Step 2：编译写入

一个资料来源可能涉及 10-15 个 wiki 页面：

1. **创建来源摘要**：`wiki/sources/{filename}-summary.md`
   - 来源信息、核心要点、关键论点（标注置信度）、涉及概念列表
2. **创建/更新概念页面**：`wiki/concepts/{name}.md`
   - 新概念 → 创建完整页面
   - 已有概念 → **重新综合整个页面**（不是简单追加）
3. **创建/更新实体页面**：`wiki/entities/{name}.md`
4. **创建/更新分析页面**：`wiki/analyses/{title}.md`（发现矛盾、互补或值得对比时）
5. **更新主题页面**：`wiki/topics/{topic}.md`（更新综合叙述）
6. **更新 index.md**
7. **追加 log.md**：
   ```
   ## [{date}] ingest | {文档标题}
   来源：raw/{path}
   新增页面：{list}
   更新页面：{list}
   ```
8. **更新 state.json**：记录文件 hash

## 模式 B：批量摄入

**触发**：参数包含 `batch` 或 `批量`

1. 扫描 `raw/` 中所有未编译文件（对比 state.json 中的 hash）
2. 列出待处理清单，询问确认
3. 逐个执行写入（跳过讨论环节）
4. 每 5 个文件执行一次跨文档关联分析
5. 完成后输出摄入报告

## 文件预处理规则

| 文件类型 | 处理方式 |
|----------|----------|
| `.md` / `.txt` | 直接读取 |
| `.pdf` | Read 工具读取（支持 PDF） |
| 代码文件 | 读取内容，标注语言 |
| 图片 | 记录路径，需要时单独查看 |
| >30000 字 | 分块处理（每块约 15000 字，保持段落完整） |

## 关键原则

- **更新而非追加**：已有页面获得新信息时，重新综合整个页面
- **链接成网**：使用 `[[页面名]]` wikilink，每个页面都应有入链和出链
- **日志可解析**：`## [{date}] {action} | {title}` 格式
