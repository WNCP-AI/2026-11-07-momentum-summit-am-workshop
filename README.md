# Agentic OS

A folder of plain files and skills that turns the AI agent you already use into a chief of staff. It learns who
you are and what your company does, connects to your tools, and prepares recurring work. You decide what goes out.

You don't need a GitHub account or any terminal knowledge. The agent does the installing.

Phases 0 and 1 take about 15 minutes.

## Pick your agent

Use the agent you already have. Each one reads this folder a little differently.

| Agent | Why pick it | Official docs |
|---|---|---|
| Claude Code | Loads rules from `CLAUDE.md` and finds skills through `AGENTS.md` | [Instructions](https://code.claude.com/docs/en/memory) |
| Codex | Reads `AGENTS.md` and the skills folder natively | [Instructions](https://learn.chatgpt.com/docs/agent-configuration/agents-md) |
| Grok Bot | In-app skills; paste the kickoff prompt below | [Skills and routines](https://docs.x.ai/grok-bot/skills-routines-and-automations) |
| OpenCode | Reads `AGENTS.md` and skills; good if you already use OpenCode | [Instructions](https://opencode.ai/docs/rules/) |
| Muse | Pick it if you already use Muse | [Skills](https://www.meta.com/help/superintelligence/2797651547267109/) |

## Get started

Paste this into your agent:

```
You are my AI chief of staff. Get the agentic OS from
https://github.com/WNCP-AI/2026-11-07-momentum-summit-am-workshop into your workspace.
Read AGENTS.md in that folder first, and treat it as authoritative.
Then run the onboarding skill.
```

That repository is the OS. The workshop example, with paste prompts and a finished run, is
https://github.com/WNCP-AI/2026-11-07-momentum-summit-am-workshop-example.

The folder can live anywhere the agent can read and write: your computer, the agent's computer, Google Drive, or any
file store. Nothing syncs.

Developers: clone the repo, open the folder in your agent, and say "get me started".

## The four phases

The agent names the phase and the step, such as "Phase 2, Your contacts".

| Phase | Steps, in order |
|---|---|
| Phase 0: Check the setup | Check the setup |
| Phase 1: Set up your OS | Memory · About you · Your company |
| Phase 2: Your first job | Your project · Who you write to · Your contacts · Past conversations · What's new · Your voice, before drafts · First drafts · Make it yours · Send it · What's next |
| Phase 3: Upgrades | Notify · Schedule · Memory. If there's time: Deep voice · Better research |

Lines you can type today:

| Step | You type |
|---|---|
| Check the setup | The kickoff prompt above |
| Your project | `set up outreach` |
| Who you write to | `investor outreach`, `sales outreach`, or `both` |
| First drafts | `run outreach on 3 contacts` |
| What's new | `what's new with my contacts` |
| Make it yours | `good enough` |
| Send it | `sent` |
| What's next | `promote outreach to the Library` |
| Notify | `set up notifications` |
| Schedule | `schedule outreach` |
| Phase 3, Memory | `upgrade my memory` |
| Deep voice | `learn my voice from my emails` |
| Better research | `add better news sources` |

Phase 1 asks the questions in the chat. The agent writes the line for Your contacts and Past conversations once it
knows the source. What's new and Send it are Phase 2 steps; type their lines when you reach them. Your voice runs on
its own, before drafts.

## What's inside

| Folder | Holds | Private |
|---|---|---|
| `0_System/` | Setup machinery and your agent's memory, as plain markdown | Memory only |
| `0_User/` | You: profile, preferences and voice | Yes |
| `0_Company/` | Your company's key facts | |
| `1_Work_Projects/` | One folder per work project | Some projects |
| `2_Research/` | Research and news your agent gathers, in dated folders | News only |
| `3_Library/` | Permanent documents, saved emails and meeting notes | Yes |
| `Z_Personal/` | Personal work | Yes |
| `.agents/skills/` | What your agent knows how to do | |

Private folders are gitignored, so they can't reach a repo by accident. That doesn't cover other ways of sharing,
so take care if you put this folder on a shared drive.

## Skills

**Core**, in every version of this OS:

| Skill | What it does |
|---|---|
| `onboarding` | Sets up the OS and learns about you and your company |
| `util-user-info` | Keeps your profile and voice up to date |
| `util-company-info` | Keeps company facts up to date |
| `util-files` | Files research, documents, emails and notes in the right place |
| `connect-tools` | Sets permissions, then connects a contact list and meeting notes. Notify is set up later |
| `memory-management` | Keeps your agent's memory in plain markdown: what to save, recall and clean up |
| `memory-upgrade` | Optional: adds Mem0 or Hindsight on top of the built-in memory |
| `make-skill` | Creates a skill or improves one from your feedback |
| `import-skills` | Finds outside skills, and checks them before they're installed |
| `util-schedule` | Puts a settled job on a recurring schedule and watches the first unattended run |
| `monthly-cleanup` | Tidies memory, news and drafts once a month |

**Writing**, to make drafts sound like you:

| Skill | What it does |
|---|---|
| `stop-slop` | Removes AI writing patterns from prose as you draft |
| `humanizer` | Rewrites AI-sounding text so it reads like you, without changing what it says |

**Outreach**, the AI chief of staff's first job:

| Skill | What it does |
|---|---|
| `outreach-setup` | Coaches the job: who you write to, contacts, past conversations, and first drafts |
| `outreach-news` | Finds news on your contacts, using built-in search, Firecrawl, or LinkedIn |
| `outreach-history` | Finds what you last discussed with each contact, from your call notes, so drafts build on it |
| `outreach` | Drafts emails to reach back out from that news and reminds you to send them |

Ask your agent "what can you do?" at any time for the current list.

## Memory

Built in, with nothing to install: plain markdown in `0_System/memory/`. The rules are in
[0_System/memory/README.md](0_System/memory/README.md). When that's working, `memory-upgrade` can add Mem0 or
Hindsight for search across a long history.
