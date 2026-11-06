# Connect a memory service

Optional. Run it from step 5 of "Using memory well" in `SKILL.md`.

## Step 1: Pick one

Ask two questions: do they want the simplest setup, and do they mind a free plan using their data for training?

| Choose | When | Details |
|---|---|---|
| **Mem0** | Simplest. A free account and a hosted connector. The free plan trains on your data | [mem0.md](mem0.md) |
| **Hindsight** | More advanced. Reasons across memories. MIT licence. Self-host it or use the pay-as-you-go cloud | [hindsight.md](hindsight.md) |

Read only the reference for the one they pick. Tell them the privacy line in it before they sign up.

## Step 2: Connect

1. Add the connector address from the reference, using this harness's own settings and docs. The user signs in.
   Keys stay in the harness's connector settings, never in a file.
2. Test it: save one harmless fact ("The user connected <service> on YYYY-MM-DD"), then search for it and find it.
3. If it fails, say what failed, keep markdown memory, and stop. Nothing else depends on the service.

## Step 3: Record it

Write the two lines in "The records" in `SKILL.md`, filled in. Leave `0_System/memory/README.md` alone.

## Step 4: Backfill, if they want

Offer to send the current `people/`, `projects/` and `glossary.md` lines to the service, one file at a time, with
the user watching the first one. Skip `0_User/05_Voice.md`, `3_Library/` and anything else private unless they say yes.
