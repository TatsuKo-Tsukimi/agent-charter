# Recommended Memory Layout

```
workspace/
├── MEMORY.md                    # Long-term curated memory (main session only)
├── memory/
│   ├── 2026-03-01.md            # Daily log
│   ├── 2026-03-02.md
│   ├── ...
│   ├── archive/
│   │   ├── 2026-01/             # Archived month
│   │   │   ├── 2026-01-15.md
│   │   │   └── ...
│   │   └── 2026-02/
│   └── heartbeat-state.json     # (optional) last-check timestamps
```

## MEMORY.md structure (recommended)

```markdown
# MEMORY.md

## [Topic or Project]
- Key decision or insight — context if needed
- Preference or rule — why it exists

## [Another Topic]
- ...
```

Keep sections short. If a section exceeds 10 bullets, it probably needs pruning or splitting.

## Daily log structure (recommended)

```markdown
# YYYY-MM-DD

## [Session or Task name]
- What happened
- Decisions made
- Next steps

## [Another session]
...
```

Raw is fine. The goal is capture, not polish — hygiene promotes the good parts later.

## Signs MEMORY.md needs pruning

- A section refers to a project that ended months ago
- There are contradictory entries (old decision overridden by new one)
- Line count > 200
- You keep reading past entries that no longer apply

## Signs daily files need archiving

- The file is older than 30 days
- The important parts have already been promoted to MEMORY.md
- Nothing in the file is still active context
