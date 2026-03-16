# memory-hygiene

An OpenClaw skill for structured memory maintenance — promoting daily logs to long-term memory, pruning stale knowledge, and keeping context load manageable.

## The problem

OpenClaw agents wake up fresh each session. Their continuity depends on two files:
- `memory/YYYY-MM-DD.md` — raw daily logs
- `MEMORY.md` — curated long-term knowledge

Without maintenance, daily files accumulate indefinitely (expensive to load), and long-term memory fills with outdated decisions (causes wrong reasoning).

## What this skill does

1. **Surveys** the current state of both tiers
2. **Reviews** recent daily files for entries worth keeping long-term
3. **Promotes** distilled insights into `MEMORY.md`
4. **Archives or deletes** old daily files that have been processed
5. **Reports** the outcome with a recommended next-run date

## When to run

- Every 3–7 days as a periodic maintenance pass
- When `MEMORY.md` exceeds ~200 lines
- When daily files older than 30 days accumulate
- After a major project ends
- When the agent says "I don't remember X" despite it being in daily logs

## Quick start

```bash
cp -r memory-hygiene ~/.openclaw/workspace/skills/
```

OpenClaw will load it on next restart. Trigger with: *"run memory hygiene"*, *"clean up my memory files"*, or *"do a memory maintenance pass"*.

## Part of the agent-charter collection

This skill pairs well with:
- `pm-safe-core` — safe execution protocol (uses the same memory paths for task logging)
- `token-efficiency` — keeping context minimal (memory hygiene directly reduces context load)
- `session-discipline` — session start/end protocol (coming in a future release)
