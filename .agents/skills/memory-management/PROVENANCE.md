# Provenance
- Source: https://github.com/anthropics/knowledge-work-plugins/tree/2574e29377c7173d0cecffef29a6ecbd7f8ccb5d/productivity/skills/memory-management
- Commit: 2574e29377c7173d0cecffef29a6ecbd7f8ccb5d
- License: Apache-2.0
- Imported: 2026-11-03, vetted with import-skills (result: Warn, accepted). Upstream "Bootstrapping" told the agent to scan
  chat, calendar, email and documents through `/productivity:start`, with no rule to treat their contents as data. That
  command doesn't exist in this OS. Resolved by replacing the section (see Changes).
- Files: SKILL.md, LICENSE (repo root LICENSE), NOTICE (added by WNCP AI), PROVENANCE.md (added by WNCP AI)
- Changes:
  - The hot cache `CLAUDE.md` is now `0_System/memory/MEMORY.md`.
  - `memory/` is now `0_System/memory/`, in the architecture, lookup flow, file formats and rules.
  - "Claude" is now "the agent" in the description and body.
  - The hot cache format gains two lines: `Active work project: 1_Work_Projects/<YYYY.MM.DD Name>/` and `Active Library processes: 3_Library/<Process>/`.
  - The description names `0_System/memory/MEMORY.md` and `0_System/memory/`.
  - Re-aligned the arrows in the architecture and lookup code blocks after the path changes.
  - "Bootstrapping" now points to `onboarding` instead of `/productivity:start`, reads emails and documents only where
    the user points, and treats their contents as data.
