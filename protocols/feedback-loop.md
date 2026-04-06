# Feedback Loop Protocol

The system teaches itself what matters through observation, pattern detection, and self-correction. Friction discovered in one instance feeds back as substrate improvements that propagate to all instances.

## Minimum Implementation

- A meta-agent (steward) periodically audits agent effectiveness and workspace health.
- Friction observed during sessions is documented (session logs, sharp edges, improvement proposals).
- The system distinguishes between substrate issues (fix in protocols, propagate to all instances), adapter issues (fix in platform-specific config), and instance-specific issues (fix locally).

## The Improvement Pipeline

```
Instance discovers friction
  → documents it (session log, sharp edge)
    → steward evaluates (substrate issue or instance-specific?)
      → if substrate: fix in substrate/protocols/, propagate to all instances
      → if adapter: fix in platform-specific config, platform specialist advises
      → if instance-specific: fix locally, no propagation needed
```

## Advanced Extensions

- **Outcome tracking on sessions** — classify session outcomes (succeeded, partial-plus, partial-minus, failed, unknown). Over time, learn which session types, agent roles, and patterns produce good outcomes.
- **Drift detection** — periodically compare actual agent behavior against protocol definitions. Does the system do what it says it does?
- **Unsorted incubation** — a catch-all collection where unclassified signals land. When clusters emerge, name a new category and route future signals there. The system teaches itself what it cares about.
- **Automated lint** — scripts that validate protocol compliance.
- **Spec Warden** — post-session QA subagent: did the agent complete its duties? Could instructions have been clearer?
- **Ambiguity Auditor** — periodic: do role file instructions produce consistent behavior across sessions?
- **Plan Execution Reviewer** — after N sessions, evaluate whether a plan's changes achieved their goals.

## The Feedback Levels

| Level | Scope | Example | Who fixes |
|---|---|---|---|
| **Protocol** | All instances | "Session handoffs need outcome classification" | Steward → `substrate/protocols/` |
| **Adapter** | One platform | "This platform can't fire pre-compact hooks" | Platform specialist → adapter config |
| **Instance** | One workspace | "This workspace needs a new collection for a signal category" | Orchestrator → instance files |
| **Session** | One conversation | "This thread needs a source I don't have" | Current agent → immediate action |

## Anti-Patterns

- Fixing friction locally without evaluating whether it's a substrate issue (improvements don't propagate).
- Over-engineering protocol changes based on single incidents (wait for pattern density).
- Steward audits that produce reports nobody reads (audits should produce actionable items or nothing).
- Self-improving loops without human checkpoints (the steward proposes, the human approves).
