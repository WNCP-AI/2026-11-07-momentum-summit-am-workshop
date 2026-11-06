# Firecrawl

Connected through the harness's connector settings, by [upgrades.md](upgrades.md). The hosted MCP is
`https://mcp.firecrawl.dev/v2/mcp`, with the free account's key. The key stays in the harness, never in a file.
Docs: https://docs.firecrawl.dev

## Use

1. **Search:** call the search tool with `"<person>" "<company>"`, then `"<company>"`. Ask for news results and a
   recent time range that covers the news window. Ask for 5 results per query.
2. **Read:** scrape only the one or two results you're going to label `yes` or `maybe`, as markdown. Search
   snippets are enough to drop the rest.
3. **Budget:** about 3 to 5 credits per contact. The free plan covers a weekly run of 5 contacts many times over.
   If the tool says credits are out, switch to built-in search for the rest of the run and tell the user.

## Don'ts

- Don't crawl whole sites or run agent or browser tools from Firecrawl. Search and one scrape are enough.
- Don't use Firecrawl on LinkedIn. That source has its own rules.
