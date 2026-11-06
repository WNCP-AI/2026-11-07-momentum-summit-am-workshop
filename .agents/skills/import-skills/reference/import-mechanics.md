# Import mechanics

The goal: land one skill at `.agents/skills/<name>/`, keep its license and record where it came from. Download to a temporary folder, vet it, and only then copy it into place.

## License rules

| License | Action |
|---|---|
| MIT, Apache-2.0, ISC, or another clearly permissive license | Allowed. Apache-2.0 requires keeping `NOTICE`. MIT and ISC require keeping the copyright line |
| None stated, or unclear | Stop. Show the user, and import only if they explicitly choose to, and record that in `PROVENANCE.md` |
| Source-available or restricted | Don't import. See catalog section 3 for the `anthropics/skills` office-document skills |

Licenses change, so re-check the upstream `LICENSE` at import time. A skill that can message a contact fails vetting even when the license is fine.

## Search

`npx skills find "<topic>"` only searches. Do not run `npx skills add` or any other installer that writes into `.agents/skills/` or another folder this agent loads as skills. Those make the skill live before it is vetted.

## Download

Put the files in a temporary folder outside every skills folder. Pick the first route that works on this agent.

**With git:**

```
git clone --no-checkout --depth 1 <repo-url> <temp-folder>
cd <temp-folder>
git sparse-checkout init --cone
git sparse-checkout set <path-to-skill>
git checkout
git rev-parse HEAD
```

**Without git:** take the commit id from the repo's latest commit page, not a branch name, then download each file:

```
https://raw.githubusercontent.com/<owner>/<repo>/<commit>/<path>
```

## Record where it came from

After vetting passes, or the user accepts a Warn, copy the skill to `.agents/skills/<name>/` and add `PROVENANCE.md` in that folder. It's deleted along with the skill, so there's no central list to maintain.

```
# Provenance

- Source: https://github.com/<owner>/<repo>
- Path: <path-to-skill>
- Commit: <full commit id>
- License: <SPDX id>
- Copyright: <copyright line>
- Imported: YYYY-MM-DD
- Vetting verdict: Pass or Warn, with any accepted warnings
```

## Why a plain copy

A plain copy works offline and survives a download. A git submodule stores only a pointer, so it breaks both.

**Updating:** download the new version to a temporary folder, vet it again, then replace the folder and update `PROVENANCE.md`.
