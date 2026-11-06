---
name: util-schedule
description: >
  Puts a settled job on a recurring schedule so it runs with nobody there: checks Notify, runs one promote to the
  Library when needed, asks for a day and time, creates the routine this harness supports, adds monthly-cleanup, and
  watches the first unattended run. Use when the user says "schedule outreach", "schedule <the job>", "run it every
  week", "run it on its own", "change the schedule" or "stop the schedule".
---

# Schedule

Any settled job can run on a schedule. Outreach is only the example. A scheduled run can't ask questions, so the job
must already work end to end. Tell the user that laptop agents run only while the machine is on.

## The records

Routines live in the harness's scheduler, named `Agentic OS: <job>`, such as `Agentic OS: outreach`. If the
scheduler has no names, put the name in a comment on the entry. `0_System/memory/MEMORY.md` has one line under
`## Preferences`: `- Schedules: <scheduler>. Routines are named "Agentic OS: <job>".` Outreach also keeps a
`- schedule:` line in `## Run` of its settings.

## Outreach: start here

1. Find **outreach** in the active project's `outreach-settings.md` or in `3_Library/Outreach/settings.md`.
2. If **`3_Library/Outreach/settings.md` is missing** (nothing in the Library yet):
   - Say scheduled jobs run from the **Library**, not the working folder. Show what **Promote to the Library** in
     `util-files` will move (the settled files for that step).
   - Ask for **one** yes. If **no**, stop, set `- schedule: by hand` in `## Run` of the work project's
     `outreach-settings.md`, and leave the job in the working folder. If **yes**, follow **Promote to the Library** in
     `util-files` with **caller already said yes** — do the move, don't ask again.
3. **Notify** must be set before a schedule: a `- notify:` line other than `chat` in `## Run`. If it's missing or
   still `chat`, offer Phase 3, Notify, in `connect-tools` (Job 3). Stop.
4. List or tidy scheduler records as in "Tidy the records" below.
5. If they asked to change or stop a routine, go to "Change or remove". It needs no readiness check.
6. Find `Agentic OS: outreach`.
   - **It exists:** show it and ask: keep it, change the time, or remove it. Follow "Change or remove", then stop.
   - **It doesn't:** if an old line or settings show it had one, say it's gone. Unless they just asked to schedule it,
     ask whether to create one. If not, stop, and set `- schedule: by hand` in `## Run` of
     `3_Library/Outreach/settings.md`. If so, create the routine (they already passed Notify and Library).

7. Ask for a day and time. The demo answer is **Monday 7:00**.
8. Follow this harness's `**Scheduler:**` line in `.agents/skills/onboarding/reference/harnesses.md`. If there's none,
   say so and offer to keep running by hand.
9. Name the routine `Agentic OS: outreach`. Write its prompt: name the job, and say to run it from its files and
   report. Never send anything to a contact.
10. Add the `Schedules:` line if it's missing. Set `- schedule: <day and time>` in `## Run` of
    `3_Library/Outreach/settings.md`.
11. If there's no `Agentic OS: monthly-cleanup` routine, offer it on the 1st of each month, created the same way.
12. Say when the first run will happen, and that you'll check it next chat.

## Other jobs

1. **Tidy the records.** List the scheduler the `Schedules:` line names, or this harness's if there's no line.
   - For each old `- Schedule:` line in `MEMORY.md`, find the routine it names. If it's there, rename it to
     `Agentic OS: <job>`, or add that name in a comment, and check the scheduler finds it. If it's gone, note it.
   - If any `Agentic OS: ...` routine exists, make sure the `Schedules:` line does. Remove the old lines once the
     user confirms.
2. If they asked to change or stop a routine, go to "Change or remove".
3. Find `Agentic OS: <job>`.
   - **It exists:** show it and ask: keep it, change the time, or remove it.
   - **It doesn't:** if an old line or the job's settings show it had one, say it's gone. Unless they just asked to
     schedule it, ask whether to create one. If not, stop, and for outreach set `- schedule: by hand` in `## Run`.
     If so, check the job is ready (see below), then create the routine.

## Check the job is ready

Each job needs these before it runs unattended:

| Job | Needs |
|---|---|
| `outreach` | Library settings (`3_Library/Outreach/settings.md` exists), and Notify done (a `- notify:` line other than `chat` in its `## Run`) |
| `monthly-cleanup` | Nothing. It reports through the notify tool under `## Connected tools` in `0_User/03_Preferences.md`, or in the run's chat |
| Any other skill | It runs without asking anything, and it reports through the notify tool in `0_User/03_Preferences.md`. Or the user agrees the results stay in files |

If something's missing, say what, and offer the fix. Stop until the user says it's done.

## Create the routine

1. Ask for a day and time. Offer a default, such as Monday 09:00.
2. Follow this harness's `**Scheduler:**` line in `.agents/skills/onboarding/reference/harnesses.md`. It names the
   scheduler, its limits and any fallback. If there's none, say so and offer to keep running by hand.
3. Name the routine `Agentic OS: <job>`. Write its prompt: name the job, and say to run it from its files and
   report. Never send anything to a contact.
4. Add the `Schedules:` line if it's missing. For outreach, also set `- schedule: <day and time>` in `## Run` of
   `3_Library/Outreach/settings.md`.
5. If there's no `Agentic OS: monthly-cleanup` routine, offer it on the 1st of each month, created the same way.
6. Say when the first run will happen, and that you'll check it next chat.

## Watch the first run

1. After the first run time passes, check what it produced and that its report arrived. If so, it's done.
2. If it stalled on a permission prompt, or didn't run, say why, using the harness entry. Help fix it once, then
   check again next chat. If it keeps failing, suggest running by hand, and say why.

## Change or remove

1. Find `Agentic OS: <job>` in the scheduler the `Schedules:` line names. Change or delete it there. If it's gone,
   say so, and offer to create it again or leave it.
2. For outreach, set `- schedule:` in `## Run` to match: the new time, or `by hand` once it's stopped.
