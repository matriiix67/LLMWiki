<p align="center">
  <strong>English</strong> | <a href="README.zh-CN.md">简体中文</a>
</p>

# BrainForge

A Claude Code plugin that lets an LLM incrementally build and maintain a persistent knowledge wiki from your collected materials.

## What It Does

Unlike RAG (retrieve-and-generate-every-time), BrainForge **compiles knowledge once** and keeps it updated. You drop raw materials — articles, papers, code, PDFs — into a folder, and the LLM reads them, extracts concepts, entities, and relationships, then writes structured, interlinked Markdown wiki pages. Over time, the wiki becomes a living knowledge base you can query, cross-reference, and grow.

## Three-Layer Architecture

```
raw/          Immutable source materials (user-managed, LLM read-only)
wiki/         Knowledge wiki (LLM-owned, structured Markdown pages)
schema.md     Schema config (co-evolved by user and LLM)
```

## Commands

Each command is a sub-command invoked via `/brainforge:<command>`:

| Command | Invocation | What It Does |
|---------|------------|--------------|
| **Init** | `/brainforge:init` | Scaffold the directory structure and config files |
| **Ingest** | `/brainforge:ingest` | Read a source file, discuss with user, write wiki pages |
| **Query** | `/brainforge:query` | Search the wiki, synthesize an answer with citations |
| **Archive** | `/brainforge:archive` | Feed valuable query outputs back into the wiki |
| **Lint** | `/brainforge:lint` | 9-dimension health check with auto-fix suggestions |
| **Status** | `/brainforge:status` | Dashboard showing KB statistics |

## Quick Start

1. **Initialize** a knowledge base:
   ```
   /brainforge:init
   ```
   This creates the directory structure and asks you to define the domain.

2. **Add materials** to the `raw/` folder — Markdown, PDF, code, plain text.

3. **Ingest** a file:
   ```
   /brainforge:ingest raw/my-paper.pdf
   ```
   The LLM reads the material, discusses key points with you, then creates/updates wiki pages (concepts, entities, source summaries, analyses). Use `/brainforge:ingest batch` to auto-process all uncompiled files.

4. **Query** the knowledge base:
   ```
   /brainforge:query What are the main differences between LoRA and QLoRA?
   ```
   Answers cite specific wiki pages via `[[wikilinks]]`.

5. **Archive** a good answer back into the wiki:
   ```
   /brainforge:archive
   ```

6. **Check** wiki health:
   ```
   /brainforge:lint
   ```
   Reports contradictions, broken links, orphan pages, missing concepts, and suggests new research directions.

## Wiki Page Types

| Type | Directory | Purpose |
|------|-----------|---------|
| **Entities** | `wiki/entities/` | People, projects, products, companies, tools |
| **Concepts** | `wiki/concepts/` | Technical concepts, theories, methodologies |
| **Sources** | `wiki/sources/` | Structured summary of each raw document |
| **Analyses** | `wiki/analyses/` | Comparative, trend, and contradiction analyses |
| **Topics** | `wiki/topics/` | High-level overviews serving as entry points |

## Design Principles

- **Resynthesize, don't append** — When a page gets new information, the entire page is rewritten as the best single document on that topic.
- **Interactive by default** — Ingest mode discusses findings with you before writing. Batch mode is the opt-in fast path.
- **Queries compound** — Good Q&A outputs can be archived back into the wiki, so exploration grows the knowledge base.
- **Raw is immutable** — Source files are never modified by the LLM.
- **Linked graph** — Every page uses `[[wikilinks]]` for bidirectional navigation. Obsidian-compatible.

## Installation

### As a Claude Code Plugin

The plugin is registered as a marketplace in Claude Code:

```
~/.claude/plugins/marketplaces/brainforge -> ~/.agents/skills/brainforge
```

Enable in `~/.claude/settings.json`:
```json
{
  "enabledPlugins": {
    "brainforge@brainforge": true
  }
}
```

## File Structure

```
brainforge/
├── .claude-plugin/
│   └── plugin.json               # Plugin manifest
├── skills/
│   ├── init/SKILL.md             # /brainforge:init
│   ├── ingest/SKILL.md           # /brainforge:ingest
│   ├── query/SKILL.md            # /brainforge:query
│   ├── archive/SKILL.md          # /brainforge:archive
│   ├── lint/SKILL.md             # /brainforge:lint
│   └── status/SKILL.md           # /brainforge:status
├── references/
│   ├── architecture.md           # Shared architecture & design principles
│   ├── templates.md              # Templates for index.md, log.md, state.json
│   └── schema-template.md        # Template for schema.md
├── README.md                     # This file
└── README.zh-CN.md               # Chinese README
```

## Requirements

- Claude Code (Claude CLI)
- No external dependencies — pure LLM text processing using built-in tools (Read, Write, Edit, Grep, Glob)

## Compatibility

- Works with Obsidian (wikilinks, folder structure)
- All wiki content is plain Markdown
- `schema.md` is human-readable and editable
