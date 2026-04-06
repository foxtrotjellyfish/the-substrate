# Temporal Anchoring Protocol

Every entry carries a timestamp and spatial anchor. All date math, day-of-week references, and deadline proximity are derived from a fresh timestamp — never from memory, training data, or drift.

## Minimum Implementation

- Session start fetches a fresh UTC timestamp (`date -u`). This is the session's temporal anchor.
- Every log entry carries a timestamp header: `### YYYY-MM-DD ~HH:MM TZ · City, ST [surface]`
- Location state is maintained in a local file (never committed to git — privacy).
- Timezone is derived from location, not from system defaults or IP geolocation.

## The Anchoring Sequence (Session Start)

1. Fetch UTC timestamp: `date -u +"%Y-%m-%dT%H:%M:%SZ"`
2. Fetch spatial anchor: location detection script
3. Derive local time from UTC + location timezone
4. Display both time and location so the human can verify
5. All subsequent date references in the session derive from this anchor

## Advanced Extensions

- **Domain-specific correlation** — cross-reference timestamps against domain-relevant temporal data (e.g., market hours, astronomical events, seasonal patterns).
- **Location confidence checking** — if location detection is IP-based (`low` confidence) or stale (`degraded`), warn the user.
- **TZ offset validation** — after commits, compare git's timezone offset against the location file to catch geolocation errors.
- **Machine identity stamps** — each entry carries a machine shortcode identifying which device produced it.
- **Capture surface enum** — distinguish between different input surfaces (desktop IDE, mobile app, CLI, web interface, etc.).

## Anti-Patterns

- Assuming the date from context headers or training data.
- Using system timezone without verifying against location.
- Committing exact coordinates to git (privacy — city-level is sufficient for committed files; coordinates stay in local-only files).
- Omitting timestamps because the entry "isn't important" (temporal signal compounds — you don't know what will matter later).
