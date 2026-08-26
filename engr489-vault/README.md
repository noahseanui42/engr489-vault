# ENGR489 Vault

How this vault works — read once, then never think about it again.

## The one rule that keeps it clean

There are **two kinds of notes** and they never mix:

1. **Reference** (`reference/`) — the *current* state of the world. Parameters,
   decisions, how things are wired right now. You **overwrite** these as things
   change. If you want to know "what is true today," look here.
2. **Worklog** (`worklog.md`) — dated, **append-only** history. What you did and
   what happened, in order. You **never edit old entries**, you only add.

Mixing these two is what caused the mess all year. Keep them apart and it holds.

## Conventions

- **ISO dates everywhere:** `2026-08-26`, never "aug26" or "last tues". Sorts
  correctly, never ambiguous, always searchable.
- **One home.** If it's a note, it lives here. If it's a binary (CAD, STL, photo,
  datasheet), it lives in `assets/` and gets referenced by name.
- **Commit often.** This vault is under git, so every commit is a dated record of
  what changed — that history doubles as your logbook. Check whether ENGR489 wants
  a formal logbook and, if so, make this feed it rather than maintaining two.

## Map

- `reference/` — one file per subsystem (current state)
- `worklog.md` — append-only dated log
- `open-issues.md` — live checklist of what's outstanding
- `assets/` — CAD, photos, datasheets (referenced from notes by name, not committed to git)
