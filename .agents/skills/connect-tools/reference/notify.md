# Notify (advanced step A1)

Job 3 of `connect-tools`. Called by `outreach-setup`. This is the one job that sends, and only to the user.

1. If a notify tool is already recorded under `## Connected tools`, show it and offer to change it.
2. Offer one channel: Slack, Asana, email to themselves, or a task in their CRM. They pick one.
3. Connect it with the Notify table in `connectors.md`. This job sends: to the user only, never a contact.
4. Send a test ping to the user. If it doesn't arrive, say so and use the fallback.
5. Record the channel in `0_User/03_Preferences.md` under `## Connected tools`, with `util-user-info`. In `## Run`
   of the active outreach settings, set the `- notify:` line to `- notify: <tool>`. Keep one `notify` line.

Fallback: the chat. Set the line to `- notify: chat` and say that scheduled runs report there.
