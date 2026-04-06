# Learning Extraction Protocol

Experience is converted to reusable knowledge through a defined pipeline. Knowledge types are classified. New material is connected to existing knowledge — both forward (new → store) and backward (new → retroactively link to old).

## Minimum Implementation

- A capture pipeline: input → process → store.
- Signal tagging for routing: each piece of knowledge carries a classification tag that determines where it's stored.
- New entries are cross-referenced against existing sources and threads when connections are evident.

## Knowledge Types

Seven categories of extractable knowledge:

| Type | Description |
|---|---|
| **Working solution** | Something that worked — preserve the pattern |
| **Failed approach** | Something that didn't work — don't repeat it |
| **Architectural decision** | A structural choice and its rationale |
| **Error fix** | A specific bug/issue and its resolution |
| **Domain pattern** | A recurring pattern in the content domain |
| **User preference** | How the human wants things done |
| **Open thread** | Unresolved question or in-progress investigation |

## The Backward Linking Pass ("Reweave")

Forward linking is natural — when you create something new, you reference what it connects to. Backward linking is the gap: when new material arrives, systematically scan existing content for things that *should* reference it but don't.

**Implementation options:**
- Heartbeat cycle: after processing new captures, scan recent threads for missed connections.
- Steward audit: periodic pass comparing source dates against thread update dates — flag threads that haven't been updated despite relevant new sources.
- Automated: semantic search across existing content for each new source, proposing connections.

## Example Pipeline

```
Input (voice, text, file, API) → capture staging
  ↓
Processor (transcribe + tag) → staging/YYYY-MM-DD.md
  ↓                    ↓
  ↓              Router (route by signal tag)
  ↓                    ↓
  ↓              collections/{signal}.md
  ↓
Orchestrator → canonical ledger
  ↓
Cross-reference against threads, sources → new connections
```

Instances adapt this pipeline to their own capture sources and processing tools.

## Advanced Extensions

- **Dual extraction** — real-time (during session, triggered by observable events like test passes or user confirmations) + async (post-session, AI-powered extraction of implicit learnings from session transcripts).
- **Vector-similarity deduplication** — prevent storing near-duplicates (e.g., 85% similarity threshold).
- **Typed knowledge storage** — separate storage/indexing by knowledge type for targeted recall.
- **Memory-aware prompting** — on each user turn, fast-search stored learnings for relevant context and inject it.

## Anti-Patterns

- Forward-only pipelines that never revisit existing knowledge (misses connections).
- Untyped knowledge storage (everything goes in one pile — harder to recall).
- Session transcripts as the only learning record (too noisy, not structured enough).
- Extracting learnings only at session end (real-time signals are lost by then).
