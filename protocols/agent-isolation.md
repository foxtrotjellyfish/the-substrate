# Agent Isolation Protocol

Specialized work happens in isolated contexts with defined scope boundaries. The orchestrator dispatches; specialists execute. Identity (who you are, what you decide) is separate from procedure (how you do things).

## Minimum Implementation

- Agent role definitions declare: scope (what they do), boundaries (what they don't do), files they read, files they write.
- Subagent spawning for parallel or isolated work — each subagent gets only the context it needs.
- A meta-agent (steward) observes the agent ecosystem and audits for scope violations.

## The Three-Layer Architecture

| Layer | Unit | Context | Good for |
|---|---|---|---|
| **Skills** | Markdown procedures | Parent's context (in-band) | Deterministic procedures, checklists, protocols |
| **Subagents** | Spawned isolated agents | Own context (isolated) | Parallel work, QA, cheap-model execution |
| **Agent Roles** | Session-level identities | Own session | Identity, routing, judgment |

**The principle:** Agent roles say *who you are* and *what you decide*. Skills say *how to do things*. Subagents do *isolated work in parallel*.

## Role Anatomy (Canonical Fields)

- **Identity** — name, description, one-line purpose
- **Scope** — what this agent does, what domain it covers
- **Boundaries** — what this agent does NOT do, what it defers to other agents
- **Files You Read** — explicit list of files/directories this agent consumes
- **Files You Write** — explicit list of files/directories this agent produces
- **Session Protocol** — what to do at session start and end
- **Cross-references** — related agents, sources, threads

## Advanced Extensions

- **Multi-session coordination** — advisory locking, heartbeat pings, file claims for concurrent agents working on the same workspace.
- **Fresh subagents per processing phase** — prevents context contamination by giving each pipeline stage a clean context.
- **Agent categories** — pipeline (stateless processors), domain (need persistent state), dialogue (conversational), support (serve other agents).
- **Model routing** — different agents use different models based on task complexity (high-capability for judgment, fast/cheap for QA/audit).
- **Coordination database** — structured tracking of which agents are active, what files they claim, cross-process communication.

## Anti-Patterns

- Agent roles that are simultaneously identity documents AND instruction manuals (conflation of identity and procedure — extract procedures into skills).
- Loading all agent context into every session (context bloat — each agent gets only its scope).
- No boundaries declaration (agents drift into each other's territory).
- Sequential execution of independent audit tasks (parallelize with subagents).
