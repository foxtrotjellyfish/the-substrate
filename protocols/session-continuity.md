# Session Continuity Protocol

Every session produces a handoff artifact sufficient for a cold-started agent to resume the work. Continuity lives in the files, not the agent's memory. Sessions are ephemeral; the workspace is permanent.

## Minimum Implementation

- A structured handoff file (markdown or YAML) is written at session end.
- The handoff includes: what happened, what's unfinished, what files were touched, and outcome classification.
- Session start reads the most recent handoff(s) to restore context.
- A status overview file provides cross-session state at a glance.

## Handoff Structure (Minimum Fields)

- **Session identifier** — unique, platform-agnostic (UUID, timestamp-based, or composite)
- **Mode** — session type (intake, thread work, research, life management, etc.)
- **What happened** — brief, high-signal summary
- **Files created/modified** — list with short descriptions
- **Open threads for next session** — what's unfinished, what needs follow-up
- **Outcome** — succeeded, partial-plus, partial-minus, failed, or unknown

## Advanced Extensions

- **Automated context-pressure triggers** — hooks that fire at configurable context thresholds (e.g., 85% warning, 90% forced handoff) to create handoffs before context is lost.
- **Session affinity** — tracking terminal/process ID so context clears resume the same logical session.
- **Warm handoff vs cold start** — explicit distinction between "same day, same intent" handoffs and "next day, fresh context" handoffs.
- **Platform-agnostic session identity** — IDs that work across any orchestration engine, not tied to any single tool's session model.
- **Session log archive** — `sessions/` directory with per-session files, sorted chronologically.

## The Naming Convention

UTC-based: `YYYY-MM-DD-HHMMz-{shortcode}.md`
- `z` suffix signals UTC (ISO 8601)
- `{shortcode}` is machine provenance (2-3 char code from machine registry)
- Human-friendly local time goes inside the file, not in the filename

## Session Ephemerality

Sessions are meant to be **short-lived and closed fast**. A session that lingers open is losing signal — context drifts, other agents sync around it, and the handoff becomes stale before it's written. Instances should treat sessions older than ~24 hours as likely abandoned. Cleanup of session-runtime artifacts (manifests, temp files) should be aggressive — measured in hours, not days.

This matters more as workspaces scale beyond a single operator. If every team member's sessions are short and closed promptly, the workspace stays coherent. Long-running sessions become invisible state that blocks accurate status reads.

## Anti-Patterns

- Relying on agent memory across sessions (stateless by design).
- Writing session logs that narrate instead of structure (future agents parse these).
- Skipping the handoff because the session "wasn't important" (every session produces artifacts or it didn't happen).
- Using platform-specific session IDs as the canonical identifier (breaks cross-platform continuity).
- Leaving sessions open indefinitely — if a session outlives ~24 hours, it should be force-closed or treated as abandoned. The goal is micro sessions that integrate fast, not long-running ambient contexts.
