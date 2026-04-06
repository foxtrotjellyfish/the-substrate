# Context Pressure Protocol

When the context window fills, the system must preserve state before the context is lost. The protocol defines what to extract, when to extract it, and where to store it.

## Minimum Implementation

- Manual session chunking: when the agent or user recognizes context pressure (slowing responses, losing earlier context), write a handoff artifact and start a new session.
- Target session length: 5-7 processing cycles, or ~3-4 hours, whichever comes first.
- The handoff captures enough state for a cold start (see Session Continuity Protocol).

## Advanced Extensions

- **Automated thresholds** — hooks that fire at configurable context usage levels:
  - 85%: warning — agent flags that context is heavy, suggests chunking
  - 90%: forced — auto-creates handoff, blocks further execution until acknowledged
- **Pre-compact extraction** — before the platform's internal compaction kicks in, extract and persist:
  - Current goal and progress
  - Key decisions made this session
  - Files modified with reasons
  - Open questions and blockers
- **Session affinity** — after a context clear, the new session resumes the same logical work using the handoff artifact, maintaining continuity of intent.

## Platform-Specific Triggers

Different orchestration engines provide different mechanisms for detecting context pressure. The adapter layer must implement whatever mechanism the platform provides:

- **Hook-based:** Some platforms fire events when context approaches a threshold (e.g., pre-compaction hooks). Use these to auto-generate handoffs.
- **Manual/heuristic:** When the platform provides no context pressure events, fall back to time-based heuristics and agent self-monitoring.
- **Token counting:** Headless/CLI agents can monitor API responses for context usage metrics directly.

The protocol is the same regardless of trigger mechanism: extract state, write handoff, prepare for cold start.

## Anti-Patterns

- Ignoring context pressure until responses degrade (by then, important context is already lost).
- Writing handoffs that are too detailed (defeats the purpose — the handoff should be compact enough to fit in the new session's context alongside new work).
- Waiting for the user to explicitly request a handoff when the agent can see the context is saturated (the agent should proactively flag it).
- Compacting without extraction (the failure mode that persistent-agent frameworks were built to prevent).
