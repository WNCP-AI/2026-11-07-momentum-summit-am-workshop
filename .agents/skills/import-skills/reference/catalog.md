# Skill catalog

Pointers only, except the skills marked bundled. Licenses were last checked on 2026-11-02, so re-check the upstream `LICENSE` at import time. Search with `npx skills find "<topic>"`. That command only searches.

Every skill here still goes through vetting. Several jobs below are already handled by a skill in this OS, and importing another one would duplicate it.

## 1. Live discovery

- **skills.sh** (`https://www.skills.sh`, by Vercel): a registry and leaderboard. Search with `npx skills find "<topic>"`. Do not use an installer from that site until the skill has been downloaded to a temporary folder and vetted. See [import-mechanics.md](import-mechanics.md).

## 2. Jobs this OS already covers

Recommend from here first. For each job, prefer the built-in route. Offer an outside skill only when the user needs something the built-in route can't do.

### Contacts, read only

Use `connect-tools`. The default is the harness's Google Sheets or Drive connector. Do not write to the sheet.

A CRM skill is a pointer, and it stays read-only. If it fails, the user exports a CSV.

- **`HubSpot/hubspot-mcp-plugins`** (Apache-2.0), skill `HubSpot-Sales/skills/contact-lookup`. *For:* reading HubSpot contacts when the user already uses HubSpot. Do not import `follow-up` from that repo: it can open a send window and update deals.

### News

Use `outreach-news`. It uses built-in web search by default. Its upgrade flow, `outreach-news/reference/upgrades.md` (advanced step A5), adds the Firecrawl hosted connector at `https://mcp.firecrawl.dev/v2/mcp`, then LinkedIn in the user's own browser. The key stays in the harness.

Do not import the Firecrawl skill folders (`firecrawl/skills`, ISC, or `firecrawl/firecrawl-claude-plugin`, MIT). Connecting the hosted MCP is enough, and those folders are large.

### Notify the user

Use `connect-tools` (Job 3). The user picks Slack, Asana, an email to themselves, or a CRM task. The fallback is the chat.

- **`anthropics/knowledge-work-plugins`** (Apache-2.0 at the repo; `partner-built/slack` is MIT, Copyright Slack Technologies, LLC), skills `slack-messaging` and `slack-search`. *For:* a Slack notification to the user when the harness has no Slack connector. Messages go only to the user.
- Asana: use the harness's Asana connector. The Asana entry in `anthropics/claude-plugins-official` (Apache-2.0) is a plugin of commands and a connector, not a skill to copy.

Do not import **`googleworkspace/cli`** skill `gws-gmail-send` (Apache-2.0). It can send mail, so it fails vetting for this OS.

### Memory

Use the built-in markdown memory, then `memory-upgrade` for Mem0 or Hindsight. Do not import another memory skill or hook installer: they write straight into skills or settings folders, and two memory systems disagree.

- **`memory-management`** (Apache-2.0, from `anthropics/knowledge-work-plugins`): bundled, adapted to `0_System/memory/`. It decodes the user's shorthand. Nothing to import.

### Writing

- **`stop-slop`** (MIT, from `hardikpandya/stop-slop`): bundled. Strips AI writing patterns from prose. Nothing to import.
- **`humanizer`** (MIT, from `blader/humanizer`): bundled. Rewrites AI-sounding text in the writer's voice. Nothing to import.

### Voice

Do not import a voice skill. `util-user-info` builds `0_User/05_Voice.md` from emails the user wrote.

## 3. Office documents: don't import

The `anthropics/skills` `pdf`, `docx`, `pptx` and `xlsx` folders are source-available reference only. Their `LICENSE` files begin "© 2025 Anthropic, PBC. All rights reserved" and limit use to Anthropic's services. The repo itself has no SPDX license. Don't import them. Check whether the user's agent can already create these files, because many can. If it can't, search live for a permissively licensed option.
