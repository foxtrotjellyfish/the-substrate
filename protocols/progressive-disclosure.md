# Progressive Disclosure Protocol

Agents navigate the workspace through progressive layers of detail, not by loading everything. Most routing decisions should happen before reading any full file. The workspace is a graph, not a pile.

## Minimum Implementation

Three levels of navigation depth:

1. **Index** — a file listing all sources, threads, ledgers, and sessions with one-line descriptions. Agents read this first to orient.
2. **Status overview** — current state, active threads, hot items, infrastructure health. Agents read this second to prioritize.
3. **Detailed files** — full sources, threads, ledgers. Agents read these on demand, scoped to the current task.

## The Traversal Pattern

```
Index (what exists) → Status (what matters now) → Detail (what I need for this task)
```

Most agent turns should only need levels 1-2. Level 3 is pulled in by reference, not pre-loaded.

## Advanced Extensions

- **YAML frontmatter descriptions** — each file carries a description in its frontmatter, enabling agents to scan without opening.
- **Wiki-links with semantic context** — links embedded in prose carry meaning ("this contradicts [source-042]" vs a bare reference).
- **Maps of Content (MOCs)** — hub files that organize clusters of related sources/threads at intermediate granularity.
- **AST-based code summaries** — background daemons providing structure/context/extract modes at different token costs (95%+ token savings).
- **Domain indexes** — per-domain status files that aggregate domain-specific state without polluting the root index.

## The Principle

Three independent systems converged on the same pattern:

- *"index → descriptions → links → sections → full content."*
- *"Structure mode → Context mode → Extract mode."*
- *"Index → Status → Detail."*

The common pattern: **progressive specificity**. Each level costs more tokens but provides more detail. The agent decides how deep to go based on the task.

## Anti-Patterns

- Loading all sources at session start (context bloat, attention dilution).
- Reading full files when only a section is needed (token waste).
- Maintaining no index at all (agents guess at structure, wasting turns on exploration).
- Index files that don't update when content changes (stale navigation → wrong decisions).
