# Hindsight

Checked 2026-11-02. Trust Hindsight's docs if they disagree: https://hindsight.vectorize.io

- **What it is:** open-source agent memory (MIT) from Vectorize. Three verbs: `retain` saves, `recall` searches,
  `reflect` reasons across everything it knows. Facts are typed and dated, and it forms observations over time.
- **Cost:** Hindsight Cloud is pay as you go, with free starting credits: https://vectorize.io/pricing. Self-hosting
  is free but needs a server and an LLM key, so it's for technical users: https://github.com/vectorize-io/hindsight
- **Privacy:** self-hosting keeps everything on the user's server. For the cloud, read Vectorize's terms with the user.
- **Sign up:** Hindsight Cloud, from https://hindsight.vectorize.io

## Connect

The cloud connector is `https://api.hindsight.vectorize.io/mcp/<bank>/`. Use a single-bank address, because the
root address reaches every bank in the account. A bank is one memory store. Name it after the user or company.

## Use

- `recall` before a task that depends on the past. It's fast.
- `retain` after a file write, with a short `context` such as "outreach decision".
- `reflect` is slower and costs more. Use it for "what should I do" questions, not lookups.
