# How These Skills Connect

Most OpenClaw skills extend what your agent **can** do.  
These skills define what your agent **should** do — before it acts.

---

## The Problem

Agents fail in predictable ways:

- Starting Ops-level work without realizing it (touching config, external paths)
- Diving into complex tasks without a safety plan
- Burning tokens re-reading files and pasting raw output
- Making "one small harness change" that breaks everything
- Enabling filesystem restrictions without knowing what will break first

Each of these is a **pre-flight failure** — something that goes wrong before the real work even starts.

---

## The Decision Chain

These 5 skills form a layered governance stack. They're designed to work together:

```
New task arrives
       │
       ▼
┌─────────────────┐
│  lane-router    │  ← Is this a workspace task or a system/runtime task?
│                 │     Project Lane (default) or Ops Lane (explicit only)
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  pm-safe-core   │  ← STOP. Confirm goal, search for context, plan before acting.
│                 │     Safety gates for destructive / external / irreversible actions.
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ token-efficiency│  ← Keep it lean. Conclusion first. Don't paste raw logs.
│                 │     Escalate model only when needed. Use output shape templates.
└────────┬────────┘
         │
    (if touching the harness)
         │
         ▼
┌──────────────────────┐
│ safe-harness-change  │  ← One tranche, one layer, one concern.
│                      │     No gateway changes, no restarts, no auth.
└──────────┬───────────┘
           │
    (if tightening filesystem boundaries)
           │
           ▼
┌───────────────────────────┐
│ workspaceonly-preflight   │  ← Read-only assessment only.
│                           │     Go / no-go before enabling workspaceOnly.
└───────────────────────────┘
```

---

## Use Them Independently or Together

Each skill works standalone — you don't need all five. But they're designed so that:

- `lane-router` narrows scope
- `pm-safe-core` structures execution within that scope
- `token-efficiency` keeps the execution lean
- `safe-harness-change` governs self-improvement safely
- `workspaceonly-preflight` gates boundary tightening

---

## What's Missing on Purpose

These skills don't:
- Connect to external services
- Store data
- Require configuration or API keys
- Run any code

They're pure behavioral protocols. They work by shaping how the agent *thinks*, not by adding new tools.

---

## Installation

Install individually or all at once:

```bash
# Install just lane-router
cp -r lane-router ~/.openclaw/workspace/skills/

# Install the full set
cp -r lane-router pm-safe-core token-efficiency safe-harness-change workspaceonly-preflight \
  ~/.openclaw/workspace/skills/
```

OpenClaw auto-detects and loads skills from the workspace `skills/` directory on next restart.
