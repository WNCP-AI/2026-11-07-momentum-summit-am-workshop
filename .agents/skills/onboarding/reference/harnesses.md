# Harnesses

You know your own harness best. Set this OS up in whatever way works best on it. This file is guidance for when you
aren't sure or something goes wrong. It may be out of date, so trust the official docs if they disagree.

## The general case

Make the three setup outcomes from `AGENTS.md` true, and check each one:

1. **Instructions load:** `AGENTS.md` applies in every new chat and scheduled run. Check: in a new chat, quote the
   safety rules without opening the file.
2. **Skills are usable:** you can find and run every skill in `.agents/skills/`. Check: name the skills on disk and
   open one `SKILL.md`.
3. **Files last:** what you save in this folder is still there next chat and next scheduled run. Check: write a test
   file in `0_System/memory/`, then confirm it is there in a new chat.

If a check fails, use the fix under "If something goes wrong". If you're still stuck, ask the user.

Your harness will also ask for permissions. `connect-tools` Job 0 sets them, using the entries below.

## Starting points

| Harness | Instructions | Skills | Schedules | Official docs |
|---|---|---|---|---|
| Claude Code | Reads `CLAUDE.md`, which imports `AGENTS.md` | Found through the `AGENTS.md` lookup | Desktop scheduled task, while the computer is on | [Instructions](https://code.claude.com/docs/en/memory), [permissions](https://code.claude.com/docs/en/permission-modes), [schedules](https://code.claude.com/docs/en/desktop-scheduled-tasks) |
| Codex | Reads `AGENTS.md` | Reads `.agents/skills/` | App scheduled task, while the computer is on | [Instructions](https://learn.chatgpt.com/docs/agent-configuration/agents-md), [approvals](https://learn.chatgpt.com/docs/agent-approvals-security), [schedules](https://learn.chatgpt.com/docs/automations) |
| OpenCode | Reads `AGENTS.md` | Reads `.agents/skills/` | System cron, while the computer is on | [Instructions](https://opencode.ai/docs/rules/), [skills](https://opencode.ai/docs/skills/), [permissions](https://opencode.ai/docs/permissions/) |
| Grok Bot | Not documented. Use the kickoff prompt and ask it to remember | In-app private skills. Folder loading is untested | Routines, with the laptop closed | [Approvals](https://docs.x.ai/grok-bot/approvals-security-and-privacy), [computer and files](https://docs.x.ai/grok-bot/computer-and-apps), [skills and routines](https://docs.x.ai/grok-bot/skills-routines-and-automations), [troubleshooting](https://docs.x.ai/grok-bot/troubleshooting) |
| Muse | Not documented. Use the kickoff prompt and memory files | Built-in skills documented. Folder loading is untested | Recurring tasks | [Permissions](https://www.meta.com/help/superintelligence/1385290430137537/), [scheduled tasks](https://www.meta.com/help/superintelligence/1484325780075655/), [skills](https://www.meta.com/help/superintelligence/2797651547267109/) |
| Claude Duet | Not documented. Use the kickoff prompt or saved preferences | Built-in skills. Folder loading is untested | Morning brief and periodic checks. Your own recurring tasks are undocumented | [Get started](https://support.claude.com/en/articles/17631495-get-started-with-claude-duet), [skills](https://support.claude.com/en/articles/12512180-use-skills-in-claude) |

**Any other harness:** look up its docs for instructions, skills, permissions and schedules, then aim for the three
outcomes above. It needs to be able to read and write files.

The kickoff prompt is in the root `README.md`.

## Claude Code

- **Quirks:** It reads `CLAUDE.md`, which imports `AGENTS.md`, so the rules load with no extra step. Skills come
  through the `AGENTS.md` lookup: list `.agents/skills/` and read the `SKILL.md` that fits.
- **Optional:** only if the user wants slash commands, symlink each skill into the `skills` folder inside `.claude/`:
  `<name>` → `.agents/skills/<name>`. Offer this as a choice. Setup doesn't need it.
- **Permissions you'll see:** a prompt before each file edit and shell command, and before each connector tool.
- **Setting:** set the permission mode. *Edit automatically* lets the agent edit files and run common file commands
  in this folder. *Auto* approves everything, with a safety check. *Bypass permissions* approves everything with no
  check. Use Edit automatically or Auto. In the terminal, press Shift+Tab to cycle modes. In the desktop app, use the
  mode selector under the prompt box. To add a folder outside the working folder for one session, run `/add-dir`.
- **Turn it back down:** press Shift+Tab until the status bar shows manual mode, or start the next session with
  `claude --permission-mode default`.
- **Scheduler:** desktop app, Code tab, Scheduled, New task, Local, with this folder. The app must be open and the
  computer awake. A task in manual mode stalls on a permission prompt. Click **Run now** once and choose "always
  allow" for each tool.
- **Docs:** [permission modes](https://code.claude.com/docs/en/permission-modes),
  [scheduled tasks](https://code.claude.com/docs/en/desktop-scheduled-tasks).

## Codex

- **Quirks:** It reads `AGENTS.md` and `.agents/skills/` natively. The sandbox blocks network by default, which can
  stop a download from GitHub. If the download fails, ask the user to allow network for the session (below), or to
  put the folder in place themselves.
- **Permissions you'll see:** prompts for commands that leave the sandbox, for network access, and for connector
  tools that change things.
- **Setting:** the sandbox is `workspace-write` by default, which reads and writes this folder. Network is off. To
  turn network on for one CLI session, start with `-c 'sandbox_workspace_write.network_access=true'`. In the app,
  check the app's settings for the permission mode. `--dangerously-bypass-approvals-and-sandbox` (alias `--yolo`)
  turns the sandbox off. Don't suggest it.
- **Turn it back down:** start `codex` with no flags, or `--sandbox workspace-write --ask-for-approval on-request`.
  Remove any `network_access = true` line from the config.
- **Scheduler:** ChatGPT desktop app, Scheduled, with this folder as the project. The app must be running, the
  computer on and the folder on disk. The CLI has no Scheduled screen. Scheduled runs use your default sandbox, so
  a task that needs network or an app can fail.
- **Docs:** [approvals and security](https://learn.chatgpt.com/docs/agent-approvals-security),
  [automations](https://learn.chatgpt.com/docs/automations).

## OpenCode

- **Quirks:** It reads `AGENTS.md` and `.agents/skills/`. It also reads the `skills` folder inside `.claude/`, so don't
  link skills there, or each skill shows twice.
- **Permissions you'll see:** most tools are allowed by default. It asks before reading `.env` files and before
  touching a path outside the folder it started in.
- **Setting:** `opencode --auto` approves every request that isn't explicitly denied. You can also toggle it from the
  command palette in the terminal screen. To allow one outside path, add it under `external_directory` in
  `opencode.json`: `"external_directory": { "~/path/**": "allow" }`.
- **Turn it back down:** start without `--auto`, toggle it off in the command palette, or remove the
  `external_directory` rule.
- **Scheduler:** none built in. Use the system scheduler (cron, launchd or Task Scheduler) to run
  `opencode run "<prompt>"`. A prompt that needs approval hangs a run with nobody there.
- **Docs:** [permissions](https://opencode.ai/docs/permissions/), [rules](https://opencode.ai/docs/rules/),
  [skills](https://opencode.ai/docs/skills/).

## Grok Bot

- **Quirks:** It works on its own computer. Instructions aren't loaded from a file, so the kickoff prompt must say to
  remember `AGENTS.md`. Skills live in an in-app *Private skills* library. Loading a folder is untested, so read each
  `SKILL.md` from the folder by hand. Files may not last between routine runs: run the "Files last" check.
- **Permissions you'll see:** approval cards. Auto-review is on by default and checks each action first. A terminal
  command card shows Allow, Skip and Manage settings. Cards raised by a routine expire after 30 minutes.
- **Setting:** on an approval card, choose **Always allow** to save a rule. To manage rules, open Settings, General,
  Bot, then **Auto-review** and **Custom Rules**. Computer access is a separate setting: Settings, Computer, Your
  computer, **Execution on this computer**. It offers Ask every time, Always allow and Never allow.
- **Turn it back down:** delete the rule under Custom Rules, or set Execution on this computer back to Ask every time.
- **Scheduler:** routines. Ask the Bot in chat. They run in the cloud with the laptop closed. A new routine doesn't
  run when created, so use **Test** once.
- **Docs:** [approvals](https://docs.x.ai/grok-bot/approvals-security-and-privacy),
  [skills and routines](https://docs.x.ai/grok-bot/skills-routines-and-automations).

## Muse

- **Quirks:** It works on its own computer. Instructions and folder skills aren't documented, so use the kickoff
  prompt and ask it to save a memory. Run the "Files last" check.
- **Permissions you'll see:** an approval prompt with Allow once, Allow for this task, Allow for this site, Always
  allow and Deny.
- **Setting:** Settings, Permissions. Connectors and Web access each offer "Ask for some actions" or "Always ask".
  Choosing **Always allow** on a prompt covers that action for that connector.
- **Turn it back down:** in Settings, Permissions, review Manage permissions, revoke a site under Allowed websites,
  or disconnect the connector.
- **Scheduler:** recurring tasks. Tell Muse the task and how often. See them in the Upcoming tab. Results arrive as
  messages in the chat. Per-task approvals are under Settings, Permissions, Artifacts and scheduled tasks.
- **Docs:** [permissions](https://www.meta.com/help/superintelligence/1385290430137537/),
  [scheduled tasks](https://www.meta.com/help/superintelligence/1484325780075655/).

## Claude Duet

- **Quirks:** It works on its own computer and can't see the files on yours. Instructions and folder skills aren't
  documented, so use the kickoff prompt. Larger finished work appears in the Make tab. Run the "Files last" check.
- **Permissions you'll see:** it asks before it sends a message, pays, signs or deletes. If you aren't there, it
  finishes the rest and brings the approval back to you later.
- **Setting:** the docs name no auto-approve or folder setting, so check the app's settings. Connectors are managed in
  your Claude settings.
- **Turn it back down:** disconnect a connector in your Claude settings. Disconnecting stops access from then on.
- **Scheduler:** a morning brief and periodic checks of your accounts. Your own recurring tasks are undocumented, so
  check the app's settings before you promise a schedule.
- **Docs:** [get started](https://support.claude.com/en/articles/17631495-get-started-with-claude-duet).

## If something goes wrong

| Problem | How to tell | Try this |
|---|---|---|
| Instructions don't load | In a new chat, "what are your standing rules?" gets a vague answer | Have the user paste the kickoff prompt, then ask you to remember it |
| Skills aren't found | "What can you do?" doesn't list them | Read `AGENTS.md` and list `.agents/skills/` by hand. This works on any harness that can read files |
| Files disappear | A file you created is gone in a new chat | Look up where this harness keeps files long term and move the folder there. If there's nowhere, tell the user routines can't keep progress |
| Folder is nested | Everything is inside a `<repo>-main/` folder | Work from inside that folder |
| Download fails | The folder can't be fetched from the repo address | The sandbox may block network. See the Codex entry. Otherwise ask the user to put the folder in place |
| Install or permission error | A command fails | Read the error, check the official docs above, and try another route. Don't ask the user to do anything you can do yourself |

If you're still stuck, tell the user plainly what failed, what you tried and which docs page to look at, then move on
to the next step.
