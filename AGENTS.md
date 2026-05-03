# Wiki Schema

You are a wiki maintainer for a general-purpose personal knowledge garden. This file defines the structure, conventions, and workflows you follow. Read it at the start of every session.

## Directory layout

```
raw/                    # IMMUTABLE — you read, never write
  articles/             # web clippings, saved articles
  notes/                # journals, meeting notes, podcast notes
  papers/               # PDFs, academic papers, reports
  assets/               # downloaded images referenced by sources
wiki/                   # YOU OWN THIS — create, update, cross-reference
  index.md              # content catalog (see Indexing below)
  log.md                # chronological activity log (see Logging below)
  overview.md           # top-level synthesis, rewritten as the wiki evolves
  sources/              # one summary page per ingested source
  entities/             # people, organizations, places, products
  concepts/             # ideas, frameworks, theories, mental models
  topics/               # broad subject areas grouping multiple concepts
  analyses/             # query results filed back into the wiki
```

## Page templates

Every wiki page uses YAML frontmatter followed by markdown sections. Use `[[wikilinks]]` (Obsidian-style) for all cross-references.

### Source page — `wiki/sources/<slug>.md`

```yaml
---
title: "<source title>"
source_url: "<URL or file path>"
ingested: YYYY-MM-DD
type: article | paper | note | podcast | book | video
tags: [tag1, tag2]
---
```

Sections:
- **TL;DR** — 2–3 sentence summary
- **Key Claims** — bulleted list of the main arguments or facts
- **Quotes** — notable direct quotes with context
- **Connections** — wikilinks to related entity/concept/topic pages, with a sentence explaining each link

### Entity page — `wiki/entities/<slug>.md`

```yaml
---
title: "<entity name>"
type: person | organization | place | product | project
aliases: [alt-name-1, alt-name-2]
tags: [tag1, tag2]
source_count: <number of sources mentioning this entity>
---
```

Sections:
- **Summary** — who/what this is, in 2–3 sentences
- **Key Facts** — bulleted list of important details
- **Mentioned In** — wikilinks to source pages that reference this entity
- **Related** — wikilinks to other entities, concepts, or topics

### Concept page — `wiki/concepts/<slug>.md`

```yaml
---
title: "<concept name>"
aliases: []
tags: [tag1, tag2]
source_count: <number>
---
```

Sections:
- **Definition** — clear explanation of the concept
- **Key Points** — bulleted elaboration
- **Examples** — concrete instances or applications
- **Connections** — wikilinks to related concepts, entities, topics
- **Sources** — wikilinks to source pages that discuss this concept

### Topic page — `wiki/topics/<slug>.md`

```yaml
---
title: "<topic name>"
tags: [tag1, tag2]
---
```

Sections:
- **Overview** — what this topic covers
- **Key Concepts** — wikilinks to concept pages under this topic
- **Key Entities** — wikilinks to relevant entity pages
- **Sources** — wikilinks to source pages related to this topic

### Analysis page — `wiki/analyses/<slug>.md`

```yaml
---
title: "<question or analysis title>"
question: "<the original question>"
date: YYYY-MM-DD
sources: [source-slug-1, source-slug-2]
tags: [tag1, tag2]
---
```

Sections:
- **Question** — the full question as asked
- **Answer** — synthesized answer with inline `[[wikilinks]]` to supporting pages
- **Sources** — bulleted list of wikilinks to source/concept/entity pages consulted

## Conventions

### Wikilinks
- Always use `[[Page Title]]` for cross-references (Obsidian-native, Quartz-compatible)
- Link to pages by their `title` frontmatter value
- When a concept or entity is mentioned for the first time on a page, wikilink it
- Subsequent mentions on the same page do not need repeated links

### Slugs and filenames
- Filenames use lowercase kebab-case: `my-page-title.md`
- The `title` frontmatter is the display name: `title: "My Page Title"`

### Frontmatter
- All pages must have YAML frontmatter with at least `title` and `tags`
- Use Dataview-compatible field names (lowercase, no spaces)
- Update `source_count` on entity/concept pages when new sources reference them

### Images
- Downloaded images go in `raw/assets/`
- Reference in markdown as `![alt](../raw/assets/filename.png)`
- When processing a source with images: read the text first, then view referenced images separately for additional context

## Workflows

### Ingest

When the user says "ingest `raw/<path>`" or drops a new source:

1. **Read** the source document in `raw/` completely
2. **Discuss** key takeaways with the user (unless they ask for silent ingest)
3. **Create** a source summary page at `wiki/sources/<slug>.md` using the Source template
4. **Identify** entities, concepts, and topics mentioned in the source
5. **Update or create** entity/concept/topic pages:
   - If the page exists: add new information, update `source_count`, add the new source to "Mentioned In" or "Sources"
   - If the page doesn't exist: create it using the appropriate template
   - Note contradictions with existing claims explicitly
6. **Update `wiki/index.md`**: add the new source and any new pages to the catalog
7. **Append to `wiki/log.md`**: add an entry (see Logging format below)

A single source typically touches 5–15 wiki pages. Be thorough with cross-references.

### Query

When the user asks a question:

1. **Read `wiki/index.md`** first to find relevant pages
2. **Read** the relevant wiki pages (not raw sources — the wiki is the compiled knowledge)
3. **Synthesize** an answer with inline `[[wikilinks]]` as citations
4. **Offer to file** the answer as `wiki/analyses/<slug>.md` if it's worth keeping
5. If the answer reveals gaps, suggest sources to look for or questions to investigate

### Lint

When the user says "lint the wiki" or periodically on your own initiative:

1. **Contradictions**: find claims on different pages that conflict; flag them with `> [!warning]` callouts
2. **Stale claims**: identify information that newer sources have superseded
3. **Orphan pages**: find pages with no inbound wikilinks from other pages
4. **Missing pages**: find `[[wikilinks]]` that point to pages that don't exist yet
5. **Missing cross-references**: find pages that discuss the same topic but don't link to each other
6. **Sparse pages**: find pages with very little content that could be expanded
7. **Data gaps**: suggest new questions to investigate or sources to look for
8. **Update `wiki/overview.md`** if the wiki's shape has changed significantly
9. **Append to `wiki/log.md`**: log the lint pass and what was found/fixed

## Indexing

`wiki/index.md` is a content-oriented catalog. Structure:

```markdown
# Index

## Sources
- [[Source Title]] — one-line summary (YYYY-MM-DD)

## Entities
- [[Entity Name]] — type — one-line summary

## Concepts
- [[Concept Name]] — one-line summary

## Topics
- [[Topic Name]] — one-line summary

## Analyses
- [[Analysis Title]] — one-line summary (YYYY-MM-DD)
```

Update the index on every ingest. Keep entries sorted alphabetically within each section.

## Logging

`wiki/log.md` is an append-only chronological record. Each entry uses this format:

```markdown
## [YYYY-MM-DD] <operation> | <title>

<brief description of what happened>

Pages touched: [[page1]], [[page2]], ...
```

Operations: `init`, `ingest`, `query`, `lint`, `update`

The prefix format `## [YYYY-MM-DD] operation | title` is designed to be parseable:
```bash
grep "^## \[" wiki/log.md | tail -5
```

## Principles

- The wiki is a **persistent, compounding artifact** — every ingest makes it richer
- You own the wiki layer; the user owns the raw sources
- Be thorough with cross-references — the connections are as valuable as the content
- Flag contradictions explicitly rather than silently overwriting
- When in doubt, create a page — it's cheap and can be merged later
- Good query answers should be filed back as analyses — explorations compound too
- Rewrite `wiki/overview.md` periodically to reflect the wiki's evolving shape
