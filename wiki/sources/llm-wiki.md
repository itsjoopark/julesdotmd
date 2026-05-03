---
title: "LLM Wiki"
source_url: "https://gist.github.com/tobi/llm-wiki"
ingested: 2026-05-03
type: article
tags: [llm, knowledge-management, methodology, obsidian]
---

# LLM Wiki

## TL;DR

A pattern for building personal knowledge bases where an LLM incrementally writes and maintains a persistent wiki of interlinked markdown files, rather than re-deriving answers from raw documents on every query (as RAG does). The human curates sources and asks questions; the LLM does all the summarizing, cross-referencing, and maintenance.

## Key Claims

- Most LLM-document workflows (RAG, ChatGPT uploads, NotebookLM) rediscover knowledge from scratch on every query — nothing accumulates
- The alternative: the LLM builds a **persistent, compounding wiki** — structured markdown files that get richer with every source ingested and every question asked
- Three-layer architecture: **raw sources** (immutable), **wiki** (LLM-owned markdown), **schema** (AGENTS.md/CLAUDE.md that codifies conventions and workflows)
- Three core operations: **ingest** (process a source into wiki pages), **query** (answer questions from the wiki, optionally filing answers back), **lint** (health-check for contradictions, orphans, stale claims)
- Two special files: **index.md** (content catalog for navigation) and **log.md** (chronological activity record)
- The wiki is just a git repo of markdown files — version history, branching, and collaboration come free
- The key insight: humans abandon wikis because maintenance burden grows faster than value; LLMs eliminate that burden because maintenance cost is near zero
- Good query answers should be filed back into the wiki as new pages — explorations compound just like ingested sources

## Quotes

> "The wiki is a persistent, compounding artifact. The cross-references are already there. The contradictions have already been flagged. The synthesis already reflects everything you've read."

> "Obsidian is the IDE; the LLM is the programmer; the wiki is the codebase."

> "Humans abandon wikis because the maintenance burden grows faster than the value. LLMs don't get bored, don't forget to update a cross-reference, and can touch 15 files in one pass."

## Connections

- [[Second Brain]] — the LLM Wiki pattern is a modern implementation of the second brain concept, with LLMs handling the maintenance that makes personal knowledge bases unsustainable for humans
- [[Memex]] — the article explicitly connects this pattern to Vannevar Bush's 1945 Memex vision, noting that LLMs solve the maintenance problem Bush couldn't
- [[RAG]] — positioned as the contrasting approach: RAG re-derives knowledge per query, while LLM Wiki compiles it persistently
