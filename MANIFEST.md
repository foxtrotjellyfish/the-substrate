# Substrate Manifest

**Version:** 0.1.0
**Created:** 2026-04-06

The substrate is the portable DNA of a Knowledge Workspace Framework (KWF) instance. Everything in this directory is context-independent — it works on any machine, any IDE, any content domain.

## What's Substrate

| Category | Contents | Location |
|---|---|---|
| **Protocols** | The eight rules any KWF instance follows | `protocols/` |
| **Canonical roles** | Tool-agnostic agent definitions (adapted per-platform by adapter layer) | `roles/` |
| **Scripts** | Portable tooling (timestamp generators, source allocators, linters, index generators, etc.) | Instance `scripts/` (symlinked or copied) |
| **Directory conventions** | `sources/`, `ledgers/`, `threads/`, `sessions/`, `research/`, `domains/` | Implicit in protocols |

## What's NOT Substrate

- **Content** — sources, ledger entries, thread analyses, session logs (instance-specific)
- **Machine identity** — git config, location state, SSH keys, shortcodes (instance-specific)
- **Clearance / org boundaries** — compliance constraints, openness levels (instance-specific)
- **Tool configuration** — platform-specific rule files, hook configs, adapter settings (adapter-specific)
- **Domain-specific agent roles** — roles tied to a particular instance's content domains (instance-specific)

## The Eight Protocols

1. **Accumulation** — content is append-only and irreplaceable
2. **Session Continuity** — every session produces a resumable handoff
3. **Progressive Disclosure** — navigate, don't load; layers of increasing detail
4. **Agent Isolation** — specialized work in isolated contexts with scope boundaries
5. **Learning Extraction** — experience → classified, reusable knowledge
6. **Context Pressure** — preserve state before the context window fills
7. **Temporal Anchoring** — every entry has a when and where
8. **Feedback Loop** — the system teaches itself what matters

Each protocol has a definition file in `protocols/` with minimum and advanced implementation levels.

## Propagation Model

**v0.1:** Substrate is integrated into instances via `git subtree`. Changes made in any instance can be pushed upstream; all instances can pull updates.

**Future:** As more instances adopt the substrate, a scaffold script reads this manifest and generates new instances. Each instance gets the protocols + scripts + adapted roles for its target platform.

## Changelog

| Version | Date | What Changed |
|---|---|---|
| 0.1.0 | 2026-04-06 | Initial manifest. Eight protocols defined. Bootstrapped from convergence analysis of three independent knowledge workspace systems. |
