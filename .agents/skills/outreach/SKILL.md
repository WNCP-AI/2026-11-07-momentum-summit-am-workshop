---
name: outreach
description: >
  Runs the reconnect loop: read contacts, skip sleeping ones, recall the last conversation with outreach-history,
  find news with outreach-news, and draft an email in the user's voice for each real reason to write. Shows the
  drafts in the chat, saves them, and logs who sleeps. Never sends. Use when the user says "run outreach", "run
  outreach on 3 contacts", "check my contacts", "draft follow-ups", "who should I write this week", or when the
  scheduled run fires.
---

# Outreach

Finds reasons to reconnect with investors or prospects, drafts the email, and shows it to the user. The user sends.
Every customization lives in the settings file, written by `outreach-setup`.

## Resolve the location

1. If `3_Library/Outreach/settings.md` exists, use the Library: drafts in `3_Library/Outreach/Drafts/YYYY/MM/`,
   meetings in `3_Library/Meetings/YYYY/MM/`.
2. Otherwise, use the active work project named in `0_System/memory/MEMORY.md`: `outreach-settings.md`, `drafts/`
   and `meetings/` in the project.
3. Otherwise, run `outreach-setup`.

`sleep-log.md`, `draft.md` and `contacts.csv` sit next to the settings file. On a scheduled run, where you can't ask
questions, skip step 3: draft nothing and say in the report that outreach needs setup.

## Before the run

1. Read the settings file and `sleep-log.md`. If the sleep log is missing, copy
   `.agents/skills/outreach-setup/assets/sleep-log.md` next to the settings file.
2. Read `0_User/05_Voice.md` and `0_Company/01_Overview.md`. In a chat, if the voice file is missing, offer the
   light voice exercise with `util-user-info` (Voice) before drafting. On a scheduled run, still draft, and say
   the voice is missing.
3. Read `## Mode`: investor, sales, or both. With both, each contact row has a Type column.
4. Use the limit in `## Run`, 10 contacts by default. If the user names a number for this run, use theirs.

## The loop

1. **Read contacts** from the source in `## Contacts`. If that read fails, read `contacts.csv`. Apply the skip and
   priority lines in `## Contacts`. Skip anyone whose Notes say not to contact them, whatever the skip line says.
   Never write to the contact source.
2. **Skip sleeping contacts:** anyone whose sleep-until date in `sleep-log.md` is still ahead. Keep the rest, up to
   the run limit, priorities first.
3. **Recall the history** with `outreach-history` for those contacts. It returns the last contact date, what was
   discussed, what was promised, and open questions.
4. **Find news** with `outreach-news` for the same contacts. It labels each item `yes`, `maybe` or `no`. If it
   already saved articles for these contacts today, use those articles instead of searching again.
5. **Draft** each `yes` item: one file per contact, shaped like `draft.md`. If there's no `draft.md` next to the
   settings file, use `.agents/skills/outreach-setup/assets/draft.md`.
   - Every draft has, in this order: a warm opening line from the relationship, in the user's voice; the news, and
     one sentence on why the news matters to them; the link to what you last discussed; one ask. Keep the length
     limits in `## Drafts`.
   - Use the contact's type: `### Investor` or `### Sales` under `## Drafts` and under `## What counts as a reason`.
     With mode investor or sales, every contact has that type.
   - Serve the goal in `## Goal`. Write in the user's voice from `05_Voice.md`.
   - Build on the last conversation: pick up a promise, an open question or the topic. If history says "no
     history", write a first-touch email.
   - If the user has an open or overdue promise to this contact, own it in one plain line, such as "I owe you the
     model-terms page. It comes Friday." Never say it was sent. If you don't know the new date, write `<date>`.
   - Mention the news specifically. Cite the source with its date in the draft header.
   - Don't repeat anything else from the last email in the history.
6. **Edit the draft.** Apply `stop-slop`, then `humanizer` in embedded mode. Then check it against `05_Voice.md`:
   phrases, punctuation, sign-off. Use `## Drafts` in the settings file for length; do not treat length as a voice
   file rule. Where the voice file and an editing rule disagree, the voice file wins.
   Keep every fact; add none. Keep the warm opener.
7. **List maybes.** Write no draft for `maybe` items. List each with one line on why, so the user can decide. An
   open promise with no `yes` news goes in the report, not in a draft.
8. **Report.** Always in the chat. Also through the notify tool if `## Run` names one; if that fails, say so in the
   chat. Notify only the user. Never message a contact.
9. **Log.** For each draft, add a row to `sleep-log.md`: contact, draft date, source link, sleep-until one month
   after today. No draft, no sleep.

## Where drafts go

| Location | Draft path |
|---|---|
| Library | `3_Library/Outreach/Drafts/YYYY/MM/YYYY-MM-DD <Contact>.md` |
| Work project | `drafts/YYYY-MM-DD <Contact>.md` in the project |

Never send a draft, schedule it, or put it in an email account's drafts folder or outbox.

## The report

Start with one line: contacts read, skipped as asleep, checked, drafts written, maybes, open promises. Then for each
draft:

1. The contact, and one line on why now.
2. The last conversation it builds on, with its date.
3. The news source, with its date and link.
4. The full draft text, so the user can copy it.
5. The saved path.

Then the maybes. Then every open or overdue promise the user made to a checked contact, with or without a draft:
contact, what, due date, and the draft or why there's none. For example: "Avery: data room and term outline, due
2026-11-06, no draft (no news)".

If a source or connector fell back, say which and what that means for the results.

Add one line to today's memory log: date, contacts checked, drafts, maybes, any source that failed.

## When the user corrects a draft

Put the change in the right place, then redo that one draft so they can compare:

| What they correct | Where it goes |
|---|---|
| Tone, phrases | `0_User/05_Voice.md`, with `util-user-info` |
| Length | `## Drafts` in the settings file |
| What counts as news, sources, history, run limit, the ask | The settings file, with `outreach-setup` |
| A wrong or missing step | This `SKILL.md`, with `make-skill` |

If they say the draft is good as is, note in the memory log what made it work.
