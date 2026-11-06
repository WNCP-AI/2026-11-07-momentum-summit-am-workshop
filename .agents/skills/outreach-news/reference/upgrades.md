# Better news sources

Advanced step A5. Run this on its own when the user says "add better news sources". The news check in `SKILL.md`
doesn't change: each run uses whatever `## News` turns on.

## Where to start

Read the `Sources on:` line in `## News` of the outreach settings:

- `firecrawl` isn't there: start at Firecrawl. If the user declines it, stop. Don't offer LinkedIn.
- `firecrawl` is there but `linkedin` isn't: skip to LinkedIn.
- Both are there: say so, and offer to turn one off.

A setup that stopped partway leaves the line unchanged, so it starts again from the same place.

## Firecrawl

1. The user signs up for a free Firecrawl account.
2. They connect the hosted MCP, `https://mcp.firecrawl.dev/v2/mcp`, through the harness's connector settings. The
   key stays in the harness, never in a file.
3. Run one contact with built-in search, then the same contact with Firecrawl, by [firecrawl.md](firecrawl.md).
   Show both results side by side and let the user pick.
4. If the user keeps Firecrawl, add `firecrawl` to the `Sources on:` line in `## News` and show them the line. If
   the connect fails, say so, stay on built-in search, and leave `Sources on:` unchanged.

## LinkedIn, optional

Offer it once Firecrawl is on. It's off by default and stays off unless the user says yes.

1. First, tell the user LinkedIn's terms prohibit scraping. Then show the rules in [linkedin.md](linkedin.md):
   read-only, in their own browser, at most 10 profiles per run, and a stop at any login check or captcha.
2. If they say yes, add `linkedin` to the `Sources on:` line. If they say no, leave it off.

## After either upgrade

Ask the user for rules about weak results: what to do with a `maybe`, and what never counts. Write their rules in
the `- Weak results:` and `- Skip:` lines in `## News`.

## Turning a source off

When the user asks to turn a source off, remove it from `Sources on:`.
