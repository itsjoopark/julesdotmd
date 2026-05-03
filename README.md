# julesdotmd

A personal knowledge garden maintained by an LLM agent, built on the [LLM Wiki](https://gist.github.com/tobi/llm-wiki) pattern. You curate sources and ask questions; the LLM does the summarizing, cross-referencing, and maintenance.

## How it works

```
raw/    → you drop source documents here (articles, notes, papers)
wiki/   → the LLM builds and maintains interlinked markdown pages
AGENTS.md → the schema that tells the LLM how to operate
```

Browse `wiki/` in Obsidian. The LLM edits it; you read the results in real time.

## Quickstart

### 1. Open in Obsidian

Open `wiki/` as a vault: **File → Open Vault → Open folder as vault** → select the `wiki/` directory.

### 2. Ingest a source

Drop a markdown file into `raw/articles/` (or `raw/notes/`, `raw/papers/`), then tell your LLM agent:

```
ingest raw/articles/my-article.md
```

The agent will read the source, create a summary page in `wiki/sources/`, update or create entity/concept/topic pages, update `wiki/index.md`, and append to `wiki/log.md`. A single source typically touches 5–15 wiki pages.

### 3. Ask a question

```
What do my notes say about <topic>?
```

The agent reads `wiki/index.md` to find relevant pages, synthesizes an answer with wikilink citations, and offers to file the answer as a permanent `wiki/analyses/` page.

### 4. Lint the wiki

```
lint the wiki
```

The agent scans for contradictions, orphan pages, missing cross-references, and stale claims. Keeps the wiki healthy as it grows.

## Tips

- **Obsidian Web Clipper** converts web articles to markdown — great for quickly adding sources to `raw/articles/`
- **Graph view** (Cmd-G in Obsidian) shows the shape of the wiki — hubs, clusters, and orphans
- Download images to `raw/assets/` for local persistence (Obsidian Settings → Files & Links → Attachment folder path → `../raw/assets/`)
- The wiki is a git repo — you get version history for free

## Structure

See [AGENTS.md](AGENTS.md) for the full schema: directory layout, page templates, frontmatter conventions, and detailed workflow specifications.
