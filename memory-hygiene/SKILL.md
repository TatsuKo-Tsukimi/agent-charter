---
name: memory-hygiene
version: 1.0.0
author: TatsuKo-Tsukimi
description: Structured memory maintenance for OpenClaw agents. Use when daily memory files are accumulating, long-term memory (MEMORY.md) is getting stale or bloated, or you want to do a periodic review to distill daily notes into curated long-term knowledge. Also use when an agent reports "I don't remember X" despite it being in a daily log, or when context load from memory files is becoming expensive. Triggers on: "clean up memory", "review my notes", "update long-term memory", "memory maintenance", or any periodic housekeeping request.
---

# Memory Hygiene

Maintain a clean, useful memory layer across daily notes and long-term memory.

## The Problem This Solves

OpenClaw agents wake up fresh each session. Their continuity comes from files:
- **Daily notes** (`memory/YYYY-MM-DD.md`) — raw logs of what happened
- **Long-term memory** (`MEMORY.md`) — curated, distilled knowledge

Without maintenance, two things go wrong:
1. Daily notes accumulate indefinitely → reading "recent context" becomes expensive
2. Long-term memory fills with outdated decisions → the agent reasons from stale data

Memory hygiene is the periodic process of promoting what matters and pruning what doesn't.

---

## Memory Tiers

| Tier | File | Contents | Lifespan |
|---|---|---|---|
| Raw | `memory/YYYY-MM-DD.md` | What happened today — tasks, decisions, events | 2–4 weeks |
| Curated | `MEMORY.md` | Distilled insights worth keeping long-term | Indefinite, actively pruned |
| Archived | `memory/archive/` | Old daily files worth keeping but not loading | Indefinite, never loaded |

---

## When to Run

Run memory hygiene:
- Every **3–7 days** as a periodic maintenance pass
- When `MEMORY.md` exceeds ~200 lines
- When daily files older than 30 days still exist in `memory/`
- After a major project completes and its context is no longer needed
- When the agent says "I don't remember X" despite it being in daily logs

---

## Steps

### 1. Survey the current state
- List all files in `memory/`
- Check the line count and age of each daily file
- Check the line count and last-update date of `MEMORY.md`
- Identify: what's fresh, what's stale, what's missing

### 2. Review recent daily files (last 7–14 days)
For each daily file, extract entries that qualify for long-term memory:
- **Decisions** with lasting relevance (architectural choices, workflow preferences, standing rules)
- **Lessons learned** (mistakes worth not repeating)
- **Preferences** expressed by the user (tool choices, tone, naming conventions)
- **Project context** that is still active

Skip: completed one-off tasks, transient status updates, anything already in `MEMORY.md`.

### 3. Update MEMORY.md
- Add distilled entries from the review
- Group by topic or project, not by date
- Remove entries that are no longer true or relevant
- Keep it under ~200 lines

Format for new entries:
```markdown
## [Topic]
- [Insight or decision] — [brief context if needed]
```

### 4. Archive or delete old daily files
- Files older than **30 days**: move to `memory/archive/YYYY-MM/` or delete
- Files older than **7 days** with nothing worth keeping: delete
- Files with content that was already promoted to `MEMORY.md`: delete

Use `trash` instead of `rm` when deleting — recoverable beats gone forever.

### 5. Report the outcome
```
Memory hygiene complete:
  Daily files reviewed: N
  Entries promoted to MEMORY.md: N
  Daily files archived: N
  Daily files deleted: N
  MEMORY.md size: N lines (was N lines)
  Next recommended run: [date]
```

---

## What NOT to Do

- Do not delete daily files without reading them first
- Do not promote raw task logs verbatim — distill, don't copy
- Do not remove entries from `MEMORY.md` without understanding why they were added
- Do not run this in a shared/group context where `MEMORY.md` contains private user data
- Do not archive everything — if you're unsure, promote first, prune on the next pass

---

## Configuring for Your Setup

This skill uses the standard OpenClaw memory layout. To adapt:

| Default path | Replace with |
|---|---|
| `memory/YYYY-MM-DD.md` | Your daily log path |
| `MEMORY.md` | Your long-term memory file |
| `memory/archive/` | Your archive location |

If your setup uses a different file structure, update the paths in the Steps section above before running.

See `references/memory-layout.md` for the recommended directory structure.
