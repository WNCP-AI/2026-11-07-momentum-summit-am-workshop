# memory

How your agent remembers things between chats. It's plain markdown with no install and no dependencies, so it
works on any agent that can read and write files. You can open and edit it yourself.

This OS uses the `memory-management` skill (`.agents/skills/memory-management/SKILL.md`). It has the rules for
reading, saving and cleaning up. Everything here except this README is gitignored.

## Layout

| Path | Holds |
|---|---|
| `MEMORY.md` | Hot cache of about 100 lines: the facts you need most, and pointers to the files below |
| `glossary.md` | Short names, acronyms and jargon, with what they mean |
| `people/` | People with a history: investors, customers, team |
| `projects/` | Lasting facts about each project, and the active location of each process |
| `context/` | What's in progress right now. Rewritten freely |

## What not to save in memory

| What it is | Where it goes |
|---|---|
| Who the user is, their preferences, how they write | `0_User/`, with `util-user-info` |
| A company fact | `0_Company/`, with `util-company-info` |
| Research and news articles | `2_Research/`, with `util-files` |
| Saved emails | `3_Library/Emails/`, with `util-files` |

Also don't save secrets, or anything you can look up again.

## Memory service

Optional. `memory-upgrade` connects one and adds one pointer line to `MEMORY.md`. The files stay the source of truth.
