---
name: monthly-cleanup
description: >
  Tidies the OS once a month: consolidates memory, archives old news and emails, trims the outreach sleep log and
  drafts, and reports what changed. Use when the monthly routine fires, or when the user says "clean up", "tidy my
  files", "clean up your memory", or "my agent is getting slow or confused".
---

# Monthly cleanup

Agents get worse as files fill with noise. This keeps what matters and moves the rest out of the way. It never
deletes the user's documents. It moves them to an archive and lists what moved.

On a scheduled run, do steps 1 to 4 and report. Anything that needs a decision goes in the report as a question,
not done.

## 1. Memory

Follow `memory-management`:

1. Keep `MEMORY.md` to about 100 lines. Move cold entries to `glossary.md` and the detail folders (`people/`,
   `projects/`, `context/`). Move finished items in `context/` into the right detail file, or remove them.
2. Archive finished projects: drop them from the active list in `MEMORY.md` and keep their facts in
   `projects/<name>.md`, with the finish date.
3. Check every path in `MEMORY.md` exists. Fix or remove broken ones. Keep the `Schedules:` and `Memory service:` lines.

## 2. News

In `2_Research/News/`, month folders older than three months move to `2_Research/News/Archive/YYYY/MM/`. Keep any
article a draft or memory file points to, because it's evidence for a sent email.

## 3. Emails and library

In `3_Library/Emails/`, list month folders older than twelve months and ask whether to keep them. Never move or
delete them on a scheduled run.

## 4. Outreach

Work where outreach lives now: `3_Library/Outreach/` if it exists, otherwise the active work project named in
`MEMORY.md`. The sleep log and drafts sit by the settings file there.

1. Move sleep-log rows whose sleep-until date is more than three months past to `sleep-log-archive.md`.
2. Move drafts older than two months into `archive/` beside them.

## 5. Report

Send the report through the notify tool recorded under `## Connected tools` in `0_User/03_Preferences.md`. If
there is none, or it fails, give the report in the chat, not in `MEMORY.md`.

- what moved, with counts per folder
- broken pointers fixed
- questions that need them, such as old emails to keep or delete
- one suggestion, if you noticed a pattern, such as a source that keeps failing

Under `## Log` in `MEMORY.md`, keep one line, `- Monthly cleanup: last run YYYY-MM-DD`, replacing any older ones.
