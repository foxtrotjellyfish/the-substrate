# Substrate

**v0.1.0-alpha** · The portable DNA of a Knowledge Workspace Framework.

---

Substrate is the platform-agnostic protocol layer for AI-augmented knowledge workspaces. It defines **how** persistent, accumulating, agent-augmented knowledge work operates — regardless of which AI tool or IDE sits on top.

## The Problem

AI agents are stateless. Every session starts from zero. The community has built solutions — knowledge graph plugins, persistent multi-agent environments, session continuity frameworks — but they're all tied to specific platforms. Switch tools and you start over.

Substrate extracts the **protocols** that make these systems work into a layer that any tool can implement through its own adapter.

## The Architecture

Substrate is one layer in the **Knowledge Workspace Framework (KWF)**:

| Layer | Name | What it is |
|---|---|---|
| 4 | **Plugins / Data Sources** | MCP servers, APIs, capture pipelines, web search |
| 3 | **Orchestration Engine** | The AI tool / IDE (any platform that can run agents) |
| 2 | **Substrate** | Protocols, scripts, file conventions, agent role patterns — **this repo** |
| 1 | **Instance** | A deployed workspace with its own content, identity, and purpose |

Each instance (a specific workspace on a specific machine) inherits the substrate and adapts it to its platform:

```
substrate/protocols/session-continuity.md     ← platform-agnostic protocol
  ↓ adapter for platform A
  platform-specific rules/config              ← implementation for platform A
  ↓ adapter for platform B
  platform-specific rules/config              ← implementation for platform B
```

The protocols are the shared DNA. The adapters are the translation layer. The content is yours.

## The Eight Protocols

| Protocol | What it governs |
|---|---|
| [**Accumulation**](protocols/accumulation.md) | Content is append-only and irreplaceable. Never consolidate without permission. |
| [**Session Continuity**](protocols/session-continuity.md) | Every session produces a handoff sufficient for a cold start. |
| [**Progressive Disclosure**](protocols/progressive-disclosure.md) | Navigate in layers of increasing detail. Don't load everything. |
| [**Agent Isolation**](protocols/agent-isolation.md) | Specialized work in isolated contexts with scope boundaries. |
| [**Learning Extraction**](protocols/learning-extraction.md) | Experience → classified, reusable knowledge. Forward and backward linking. |
| [**Context Pressure**](protocols/context-pressure.md) | Preserve state before the context window fills. |
| [**Temporal Anchoring**](protocols/temporal-anchoring.md) | Every entry has a when and where. Timestamps from source, not memory. |
| [**Feedback Loop**](protocols/feedback-loop.md) | The system teaches itself what matters. Friction → improvement. |

Each protocol defines a **minimum implementation** (what any instance must do) and **advanced extensions** (what mature instances can add).

## The Convergence

Three independent systems — built on different platforms by different people — converged on the same fundamental principles:

| Principle | System A | System B | System C |
|---|---|---|---|
| Don't lose signal | "The accumulation IS the value" | "Compound, Don't Compact" | "Notes grow, never edit" |
| State survives sessions | Session logs + warm handoffs | PreCompact YAML handoffs | SessionStart/Stop hooks |
| Navigate, don't load | Index → Status → Detail | 5-layer AST summaries | Skill graph traversal |

These aren't preferences. They're protocols. Substrate extracts them so they can be shared.

## Integration

Substrate is designed to live inside your workspace as a `substrate/` directory.

**Git subtree** (recommended — files live naturally in your repo):
```bash
# Add substrate as a remote
git remote add substrate <this-repo-url>

# Pull it into your workspace
git subtree add --prefix=substrate/ substrate main --squash

# Pull updates
git subtree pull --prefix=substrate/ substrate main --squash

# Push improvements back
git subtree push --prefix=substrate/ substrate main
```

**Direct clone** (for exploration):
```bash
git clone <this-repo-url>
```

## Status

This is **v0.1.0-alpha**. The protocols are extracted from real systems that have been running for months, but the substrate itself — as a standalone, shared artifact — is new. Expect evolution. The protocols will sharpen as more instances put pressure on them.

## Directory Structure

```
substrate/
  MANIFEST.md                    ← what's substrate vs not, versioned
  protocols/                     ← the eight protocol definitions
    accumulation.md
    session-continuity.md
    progressive-disclosure.md
    agent-isolation.md
    learning-extraction.md
    context-pressure.md
    temporal-anchoring.md
    feedback-loop.md
  roles/                         ← canonical agent definitions (tool-agnostic)
```

## License

MIT
