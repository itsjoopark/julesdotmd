---
title: "RAG"
aliases: [Retrieval-Augmented Generation, retrieval augmented generation]
tags: [llm, knowledge-management, architecture]
source_count: 1
---

# RAG

## Definition

Retrieval-Augmented Generation (RAG) is a pattern where an LLM retrieves relevant chunks from a collection of documents at query time and uses them to generate an answer. The documents themselves are not transformed or synthesized ahead of time — the LLM rediscovers relevant knowledge from scratch on every question.

## Key Points

- RAG is the dominant approach in most LLM-document workflows: NotebookLM, ChatGPT file uploads, enterprise knowledge bases
- Strength: no upfront processing needed — upload documents and start querying immediately
- Weakness: knowledge is re-derived per query, not accumulated — subtle questions requiring synthesis across many documents are answered inconsistently
- The [[LLM Wiki]] pattern is positioned as the alternative: compile knowledge persistently into a wiki, so cross-references and synthesis are built up over time rather than reconstructed per query
- RAG is still useful at scale as a search mechanism over a large wiki (e.g. using [[qmd]] or embedding-based retrieval), but the LLM Wiki argues the wiki layer should exist between RAG and the user

## Connections

- [[Second Brain]] — RAG is one approach to building a queryable knowledge base; the second brain / LLM Wiki is the other
- [[Memex]] — RAG lacks the persistent "associative trails" that Bush envisioned

## Sources

- [[LLM Wiki]] — contrasts RAG with the persistent wiki approach
