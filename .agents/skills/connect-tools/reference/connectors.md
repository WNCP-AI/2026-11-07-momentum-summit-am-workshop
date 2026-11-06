# Connectors

Job 0 sets permissions. Jobs 1 and 2 connect sources. Job 3 (Notify) is set up in Phase 3, Notify. If the connect
button isn't obvious, use the harness guide at `.agents/skills/onboarding/reference/harnesses.md`. Trust that
harness's official docs if they disagree with this file.

## Permissions

One row per harness. The full entry, with docs links, is in the harness guide.

| Harness | What to ask the user to set | Turn it back down |
|---|---|---|
| Claude Code | Permission mode *Edit automatically* or *Auto* | Shift+Tab to manual mode, or `--permission-mode default` |
| Codex | Keep the `workspace-write` sandbox. Allow network for the session if a download is blocked | Start `codex` with no flags |
| OpenCode | `opencode --auto`, or allow the folder under `external_directory` | Start without `--auto` |
| Grok Bot | **Always allow** on the approval cards for this folder | Delete the rule under Settings, General, Bot, Custom Rules |
| Muse | Settings, Permissions: choose **Always allow** on the prompts for this folder's connectors | Settings, Permissions, Manage permissions |
| Claude Duet | Check the app's settings. No auto-approve setting is documented | Disconnect a connector in your Claude settings |

## Contacts (read only)

| Source | How to connect | Read-only rule | Fallback |
|---|---|---|---|
| HubSpot, Salesforce, Attio | The harness's connect button for that CRM | Read contacts only. Create and update nothing | The user exports a CSV |
| Google Sheet | The harness's Google or Sheets connector | Read the sheet. Never write to it | The user exports a CSV |
| Gmail or Google Contacts | The harness's Gmail connector | Read sender names and addresses. Never send, draft or label. No separate Google Contacts connector: use Gmail | The user pastes a list |
| Outlook contacts and mail | The harness connector if it has one. Claude has Microsoft 365. Grok has Outlook mail and calendar. Codex has an Outlook mail plugin. Muse does not | Read only. Never send | Export or paste |
| Files in this workspace | None. The agent reads files in this workspace with its own file access | Read the named CSV where it is. Never edit, move or copy its rows | The user pastes a list |
| A list | The user pastes it in chat | Not applicable | Save it as a CSV in the active work project |

Columns outreach expects, and can adapt if they differ: name, company, role, type (investor or prospect),
email, last contact, notes, and LinkedIn profile URL if they use LinkedIn.

## Meeting notes (read only)

| Source | How to connect | Read-only rule | Fallback |
|---|---|---|---|
| MeetGeek | The harness's connector, or MeetGeek's own integration settings | Read titles, dates, summaries and transcripts. Change nothing | The user pastes notes |
| Fireflies | The harness's connector | Read titles, dates, summaries and transcripts. Change nothing | The user pastes notes |
| Otter | The harness's connector, if it has one for Otter; otherwise say this harness has no Otter connector | Read titles, dates, summaries and transcripts. Change nothing | The user pastes notes |
| Teams transcripts | Claude's Microsoft 365 connector includes Teams if your harness offers it. Grok's Teams connector is chat, not transcripts. If this harness cannot read transcripts, say so | Read only | Paste |
| A Drive folder | The harness's Google Drive connector | Read files in that folder only. Never edit or move them | The user pastes notes |
| OneDrive or SharePoint | If your harness has a connector (Claude and Grok do), read the named folder only. If this harness has no connector, say so | Read only. Never edit or move | Paste or a file in this workspace |
| Gmail | The harness's Gmail connector | Read messages that hold notes. Never send, draft or label | The user pastes notes |
| Outlook | The harness connector if it has one for Outlook mail (see Contacts). Read only. Never send | Read messages that hold notes | Paste |
| Files in this workspace | None. The agent reads files in this workspace with its own file access | Read files in the named folder and its subfolders only. Never edit or move them | The user pastes notes |

If a meeting tool has no connector in this harness, say so and use the paste fallback.

## Notify the user

Job 3 connects one of these, in Phase 3, Notify. It's the one job that sends, and it sends to the user only.
Never message a contact.

| Channel | How to connect | Send rule | Fallback |
|---|---|---|---|
| Slack | The harness's Slack connector | A direct message to the user | Say it in the chat |
| Asana | The harness's Asana connector | A task assigned to the user | Say it in the chat |
| Email to self | The harness's email connector | Only the user's own address | Say it in the chat |
| A CRM task | The harness's connector for that CRM | One task assigned to the user, nothing else | Say it in the chat |

If a channel has no connector in this harness, check that tool's docs for an MCP address. If there isn't one, use
the fallback.
