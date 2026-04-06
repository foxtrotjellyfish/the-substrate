# Accumulation Protocol

Content is append-only and irreplaceable. The value is in the accumulation, not the summary. Compaction, consolidation, and summarization are destructive operations requiring explicit human permission.

## Minimum Implementation

- Ledgers and threads are append-only files with timestamped entries.
- No edit, no delete, no merge of existing entries.
- New entries go at the bottom with a date-stamped header.
- Full-file overwrite tools are never used on accumulating files — only targeted append via string replacement or dedicated append tooling.

## Advanced Extensions

- Item state markers: `[ ]` open, `[x]` done, `[>]` migrated, `[~]` waiting, `[-]` cancelled.
- Heat levels for triage: HOT (deadline/blocking), WARM (in flight), STASIS (safe to pause).
- Signal-tagged collections for parallel routing (signal tags → collection files).
- Migration logging: when items move, the move is logged inline with a reference to the destination.

## The Principle

Three independent systems converged on the same conclusion:

- *"The accumulation IS the value."*
- *"Compound, Don't Compact."*
- *"Notes grow, observations accumulate."*

It's not a preference — it's a protocol.

## Anti-Patterns

- Consolidating ledger entries into summaries (destroys temporal signal).
- Rewriting thread sections to be "cleaner" (loses the evolution of thinking).
- Context compaction that discards nuanced decisions.
- Using full-file overwrite tools on accumulating files.
