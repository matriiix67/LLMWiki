# Schema Template

> Generated as `schema.md` during init. Pick the section matching the user's chosen language.
> User and LLM co-evolve this file over time.

---

## schema.md — zh

```markdown
# Wiki Schema

> 本文件定义知识库的结构约定和工作流规则。
> 由用户和 LLM 共同维护，随使用不断优化。

## 领域

{domain}

## 语言约定

- 所有 wiki 页面使用中文撰写
- 关键术语保留英文原文（如 Transformer、RAG、LoRA）
- 术语首次出现时格式：中文名（English Term）

## 页面类型与约定

### 实体页面（entities/）
用于：人物、项目、产品、公司、工具等具体事物
包含：一行简介、关键属性、详细描述、关系链接

### 概念页面（concepts/）
用于：技术概念、理论、方法论、术语
包含：清晰定义、原理/机制、应用场景、与相关概念的关系和区别

### 来源摘要（sources/）
用于：每个原始文档的结构化摘要
包含：来源信息、核心要点（200-500 字）、关键论点（标注置信度）、涉及的概念和实体

### 分析页面（analyses/）
用于：对比分析、综合分析、趋势分析、矛盾分析
包含：分析目标、涉及来源、分析内容、结论和开放问题

### 主题页面（topics/）
用于：某个研究方向的全局概述，是该领域的"入口页"
包含：主题概述、核心概念列表、关键实体、综合叙述、待研究问题

## 链接约定

- 使用 [[页面名]] 格式的 wikilink
- 每个页面都应有入链和出链
- 新概念首次提及时如果尚无页面，先创建 stub

## 摄入工作流偏好

- 默认：交互式，LLM 与用户讨论后再写入
- 可选：批量模式，减少交互

## 领域特化规则

{随使用积累，例如：}
{- 对于论文类资料，重点提取方法论和实验结果}
{- 对于新闻类资料，标注时效性}
{- 对于代码类资料，重点提取架构设计和关键 API}
```

---

## schema.md — en

```markdown
# Wiki Schema

> This file defines the structure conventions and workflow rules for the knowledge base.
> Co-maintained by user and LLM, refined over time.

## Domain

{domain}

## Language Conventions

- All wiki pages are written in English
- Keep well-known abbreviations and proper nouns as-is (e.g. Transformer, RAG, LoRA)
- Define acronyms on first use: Full Name (ABBR)

## Page Types & Conventions

### Entity Pages (entities/)
For: people, projects, products, companies, tools
Contains: one-line summary, key attributes, detailed description, relationship links

### Concept Pages (concepts/)
For: technical concepts, theories, methodologies, terms
Contains: clear definition, mechanism/principles, use cases, relationships and distinctions with related concepts

### Source Summaries (sources/)
For: structured summary of each raw document
Contains: source info, key points (200-500 words), main arguments (with confidence), related concepts and entities

### Analysis Pages (analyses/)
For: comparative, synthesis, trend, and contradiction analyses
Contains: analysis goal, involved sources, analysis content, conclusions and open questions

### Topic Pages (topics/)
For: high-level overview of a research area, serving as an "entry page"
Contains: topic overview, core concept list, key entities, synthesized narrative, open research questions

## Link Conventions

- Use [[Page Name]] wikilink format
- Every page should have inbound and outbound links
- Create stubs for new concepts mentioned but not yet documented

## Ingest Workflow Preference

- Default: interactive — LLM discusses with user before writing
- Optional: batch mode — less interaction

## Domain-Specific Rules

{Accumulated over time, e.g.:}
{- For academic papers, focus on methodology and experimental results}
{- For news articles, mark timeliness}
{- For code repositories, focus on architecture and key APIs}
```

---

## Other Languages

For languages not listed above (e.g. 日本語, Deutsch, Español), use the English template as a base and translate all headings, labels, and placeholder text into the target language. Keep the same structure.
