# Contributing

Thanks for helping keep this the most current directory of AI agents for databases!

## Adding an entry

1. **Check it fits:** the entry must be an AI agent, copilot, framework, MCP server, analytics agent, or benchmark whose core job is querying, exploring, managing, or acting on **databases** via natural language or tool use. Generic LLM frameworks with a SQL tutorial don't count; generic BI tools with a chatbot bolted on don't count. A PR must point at a primary source: the vendor's official docs page or the project's official repo.
2. **Add to the right section** of `README.md`:
   - Text-to-SQL / NL2SQL agents & frameworks → dedicated NL→SQL systems
   - Database copilots & platform AI → AI features built into DB platforms and DB tools
   - MCP servers & agent tooling → Model Context Protocol servers and tool layers for databases
   - Agentic analytics & BI agents → agents that analyze and visualize database data
   - Frameworks for building DB agents → agent frameworks, semantic layers, and query layers used to build DB agents
   - Benchmarks & research → text-to-SQL benchmarks and influential open methods
3. **One entry = one bullet.** Format:
   `- [Name](https://example.com/official-docs) — ` one-line description + 2–4 key facts inline. Use the `OSS` tag for open-source entries.
   Tag verification honestly: every entry in this list is checked against its official source; if you couldn't verify a fact, say so rather than softening it.
4. **Add the matching record** to `data/agents.json` with these exact fields:

| field | type | values |
|---|---|---|
| `name` | string | product / project name |
| `org` | string | vendor / organization / author |
| `category` | string | `text2sql` / `db-copilots` / `mcp-servers` / `analytics-agents` / `frameworks` / `benchmarks` |
| `description` | string | one sentence |
| `url` | string | official https:// URL |
| `license` | string | exact OSS license, or SaaS pricing model in 2–4 words |
| `open_source` | bool | `true` / `false` |
| `verified` | bool | `true` only if you confirmed the entry on an official source |
| `last_verified` | string | ISO date, e.g. `2026-10-03` |

5. **Status changes:** if a product is retired, acquired, renamed, or archived, update its README entry *and* add a row (newest-first) to `docs/status-changes.md`.

## Style rules

- Link the **official site** (vendor docs page or project repo), never a blog post or aggregator.
- Facts that can change (pricing, versions, benchmark scores) get "as of" context in prose or are omitted — link the source instead of hard-coding numbers that rot.
- Vendor claims stay labeled as vendor claims ("vendor claims", "reported by the vendor").
- Never guess a price or a license. If the official source doesn't state it, write what it does state or leave the entry out.
- Keep README descriptions to one entry per bullet; put depth in `docs/`.

## CI

Every PR runs:
- **Link check** (lychee) over all markdown files — no dead links.
- **JSON validation** — `data/agents.json` must parse, every record must have the required fields, and `category` must be from the allowed set above. The same link check also runs monthly on a schedule to catch link rot.

Run locally before pushing:

```bash
python3 -c "import json; json.load(open('data/agents.json')); print('ok')"
```
