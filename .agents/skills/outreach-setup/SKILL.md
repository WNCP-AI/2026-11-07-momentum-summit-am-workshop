---
name: outreach-setup
description: >
  Builds the outreach job in a dated work project and coaches the user through it: who you write to, your contacts,
  past conversations, what's new, your voice, first drafts, and fixes until the drafts are good. The user sends one
  email, then What's next covers promote outreach, schedule outreach, what's new with my contacts, and sent. Use when
  the user says "set up outreach",
  "build my outreach job", "change my contacts", "change the mode", "change where my call notes are",
  "outreach isn't finding the right people", "what's new with my contacts", "sent", "promote outreach" or
  "schedule outreach".
---

# Outreach setup

Builds the outreach job once, with the user, one step at a time. The `outreach` skill then runs it from the files
this skill writes.

## How to coach

Follow `reference/coaching.md` on every step.

Never write to a contact source. Never message a contact.

## Find the job

The settings file is `3_Library/Outreach/settings.md` if it exists, or else `outreach-settings.md` in the active
outreach project in `MEMORY.md`. If neither exists, start at Your project. Every step below edits that file.

When the job exists, go to the named step. "change the mode" is Who you write to. "change my contacts" is Your
contacts. "change where my call notes are" is Past conversations. "what's new with my contacts" is What's new.
"sent" follows `reference/send-it.md` only when Send it is active (after Make it yours finished) or you are already
guiding Send it. Otherwise say which step you're on. "promote outreach" follows **Promote to the Library** in
`util-files`. "schedule outreach" follows `util-schedule`. Otherwise, show the settings and ask which section to change.

## J1. Your project

**What's happening:** "Phase 2, Your project: I'm making a work project for your outreach job."

**The user types:** "set up outreach"

A working folder where we build and test the job. Once it works, it moves to your Library.

1. Create `1_Work_Projects/YYYY.MM.DD Outreach/` for today with `util-files`. Pick the name. Don't ask.
2. Add the folder's path to `.gitignore` before saving anything in it. Tell the user it will hold contacts.
3. Copy the three files in `assets/`. Rename `settings.md` to `outreach-settings.md`. Never overwrite a file.
4. Write `README.md`: the goal, status "Your project done", and the next step.
5. Add one line to `0_System/memory/MEMORY.md`: `Active outreach project: 1_Work_Projects/YYYY.MM.DD Outreach/`.

**Writes:** `README.md`, `outreach-settings.md`, `draft.md`, `sleep-log.md`, `.gitignore`, `MEMORY.md`.

## J2. Who you write to

**What's happening:** "Phase 2, Who you write to: now we pick who you're writing to."

**The user types:** "investor outreach", "sales outreach" or "both". Then: "Goal: <one sentence on what these emails
are for this quarter>". Follow `reference/who-you-write-to.md`.

**Writes:** `## Mode`, `## Goal`, `## What counts as a reason` and `## Drafts` in the settings file.

## J3. Your contacts

**What's happening:** "Phase 2, Your contacts: I connect to your contact list, read-only."

**The user types:** "My contacts are in HubSpot." Example: "My contacts are in <source>." Sources in order: a CRM (HubSpot, Salesforce, Attio), a Google Sheet, Gmail or Google Contacts, Outlook, a CSV in this workspace, or a pasted list. Read only. It reads your list where it lives and never writes to it. If it is not connected, paste three names or export a CSV.

1. Connect with `connect-tools` job 1. Read-only. Read a workspace CSV where it is. Don't copy its rows.
2. If it can't connect, ask the user to paste the list. Save it as `contacts.csv` in the project.
3. Show the first five rows and the column names. Say how you'll use each column.
4. Show the default `Skip:` line. Ask who to skip and who goes first. The user types: "Skip <rule>. Put <rule> first."
5. With mode "both", find the column that says investor or sales. If there isn't one, ask which column does.
6. Fill `## Contacts`: source, how to read it, columns, skip and priority rules. Write the location, never the rows
   or keys. A workspace CSV uses the source lines in `assets/settings.md`. On a re-run, replace the section. If the
   new source isn't a paste, offer to delete an old `contacts.csv`, because `outreach` falls back to it.

**Writes:** `## Contacts` in the settings file, and `contacts.csv` if it's a pasted list.

## J4. Past conversations

**What's happening:** "Phase 2, Past conversations: I find what you've already discussed, read-only."

**The user types:** "My call notes are in Fireflies." Example: "My call notes are in <source>." Sources: MeetGeek, Fireflies, Otter, Teams transcripts, Drive or OneDrive or SharePoint, Gmail or Outlook, files in this workspace, or pasted notes. Same paste fallback. Then: "My sent emails are in <my email | files in this workspace, <folder>>" or "skip"

1. Connect with `connect-tools` job 2, for the notes and the emails. Read-only.
2. Fill `## History` now: the source, how to read it, and `Emails:`. If the user skips emails, delete that line. A
   workspace folder uses the lines in `assets/settings.md`. On a re-run, replace the whole section.
3. Run `outreach-history` for the first three contacts in priority order. It saves notes to `meetings/`.
4. If nothing connects, set the `## History` source to "pasted notes". Save each paste as `outreach-history` does.
5. Show one saved note and its summary: last contact, discussed, open questions, promised.

**Writes:** `meetings/` in the project, and `## History` in the settings file.

## What's new

**What's happening:** "Phase 2, What's new: I look up recent news on your first three contacts, before any draft."

**The user types:** "what's new with my contacts". Run `outreach-news` on its own. Follow `reference/whats-new.md`.

**Writes:** articles in `2_Research/News/`, and `## What counts as a reason` when they change it.

## Your voice

**What's happening:** "Phase 2, Your voice: I check that a draft can sound like you." If `0_User/05_Voice.md`
exists, say so in one line and move on. If not, follow `reference/your-voice.md`.

**Writes:** `0_User/05_Voice.md`, only when it was missing.

## J5. First drafts

**What's happening:** "Phase 2, First drafts: we run outreach for real, on three contacts."

**The user types:** "run outreach on 3 contacts". Run `outreach`. It reuses news saved for these contacts today.
Show each draft, or why there is none.

**Writes:** `drafts/`, `sleep-log.md`, and articles in `2_Research/News/` for anyone still missing one.

## J6. Make it yours

**What's happening:** "Phase 2, Make it yours: we fix what's off, then run the same contacts again."

**The user types:** "not yet: <what's wrong>" or "good enough". Follow `reference/make-it-yours.md`.

**Writes:** the file named there, `sleep-log.md`, and new drafts in `drafts/`.

## Send it

**What's happening:** "Phase 2, Send it: you send one email from your own mailbox. I never send."

**The user types:** "sent". Follow `reference/send-it.md`.

## J7. What's next

**What's happening:** "Phase 2, What's next: outreach works. Let's keep it and choose what's next."

1. Add a line to today's memory log: `YYYY-MM-DD outreach working, <mode>, project <path>`. Set the README status
   to "Working".
2. Show the What's next list. Follow `reference/j7-whats-next.md`.

**Writes:** today's memory log and `README.md`.
