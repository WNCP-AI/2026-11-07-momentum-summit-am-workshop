# Mem0

Checked 2026-11-02. Trust Mem0's docs if they disagree: https://docs.mem0.ai/platform/mem0-mcp

- **What it is:** a hosted memory service. It pulls facts out of what you send and finds them again by meaning.
- **Cost:** a free plan. Limits are on the pricing page: https://mem0.ai/pricing
- **Privacy, say this first:** Mem0's privacy policy says interactions on the Free plan are used to train its
  models. Paid plans are not. Keep private details out, or choose Hindsight.
- **Sign up:** https://app.mem0.ai

## Connect

The connector address is `https://mcp.mem0.ai/mcp`. If the harness asks for an API key instead of a sign-in, the
user creates one in Mem0 and keeps it in the harness's secret settings, never in a file here.

## Use

- Save with `add_memory`. Search with `search_memories`.
- Don't call `delete_all_memories` or `delete_entities` unless the user asks, by name, in this chat.
