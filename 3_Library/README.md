# 3_Library

Your permanent record: documents you want to keep, settled processes, emails your agent uses, and meeting notes.

Everything here except this README is gitignored, because these files often name contacts or hold sensitive
information.

| Type | Where | Name |
|---|---|---|
| Documents | `3_Library/` | Keep the original name |
| Outreach | `Outreach/` | Settings, sleep log and contacts. Drafts in `Outreach/Drafts/YYYY/MM/` |
| Emails | `Emails/YYYY/MM/` | `YYYY-MM-DD <Sender or contact> - <subject>.md` |
| Meeting notes | `Meetings/YYYY/MM/` | `YYYY-MM-DD <topic>.md` |

**Promotion:** a settled process moves here from a work project. The `util-files` skill copies the settled files
to `3_Library/<Process>/` after you say yes. The project stays as the record of how it was built.

**Emails** are saved as markdown when a skill uses them: the samples that teach the agent your voice, and past
emails with a contact that a draft builds on. Each one starts with who, when and the subject, then the body.
Signatures, long quoted threads and anything you mark private are left out.

Files stay here in full. When one holds a lasting fact, the agent saves a short, tagged line in
`0_System/memory/` or `0_Company/` that points back here. Daily logs live in `0_System/memory/`, not here.

The `util-files` skill files things here. `monthly-cleanup` asks before touching anything older than a year.
