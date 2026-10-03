# Choosing a database agent

A decision guide. The right answer depends less on the model than on where your data lives, how governed your metrics are, and how much damage a wrong answer can do.

## Step 1: Where must the agent run?

- **Inside a platform you already pay for** → start with the native copilot: Databricks Genie, Snowflake Cortex Analyst, Gemini in BigQuery, Supabase AI. Zero integration work, and they see your real schema and query history. Evaluate them before buying anything else.
- **Across several databases / self-hosted** → an OSS text-to-SQL framework (Vanna, WrenAI, DB-GPT) or MCP servers wired into your own agent. Budget engineering time; you own the safety layer.
- **In analysts' existing BI tool** → the analytics agents (Hex Magic, ThoughtSpot Sage, Metabase Metabot): the value is workflow (notebooks, dashboards, sharing), not raw NL→SQL accuracy.

## Step 2: How governed are your metrics?

- **Finance-grade numbers** (revenue, churn, board metrics) → demand a semantic layer (Cube, dbt Semantic Layer, Malloy, Wren MDL) or a platform agent that consumes one. Bare text-to-SQL will eventually produce a confident, wrong join.
- **Exploration and debugging** (why did this pipeline break, what's in this table) → bare text-to-SQL is fine and faster to adopt; show-the-SQL UIs matter more than benchmark scores.

## Step 3: Pick your integration surface

- **Chat UI for non-technical users** → hosted agents/copilots.
- **Embedded in your product** ("ask your data" inside your SaaS) → Cube's agent APIs, WrenAI, Vanna, or a semantic layer + your own LLM calls.
- **Agent tooling for coding assistants / internal agents** → MCP servers (start with the vendor-official ones: MongoDB, ClickHouse, Neon, Supabase, Google's MCP Toolbox).

## Step 4: Evaluate like an adult

1. Build a 30–50 question eval set from *real* past analyst requests, with known-correct SQL/results.
2. Score: exact result match, not "SQL looks right". Include questions the agent *should* refuse or clarify.
3. Measure the self-correction loop: first-try accuracy vs after-retry accuracy.
4. Test the failure modes: huge tables, cryptic column names, ambiguous terms ("active users" — whose definition?).
5. Only then look at vendor benchmark claims (Spider/BIRD numbers are on clean academic schemas — see [benchmarks-and-evals](benchmarks-and-evals.md)).

## Red flags

- No way to inspect the generated SQL.
- Requires write credentials for a read-only use case.
- "95% accurate" claims with no named benchmark or eval set.
- No row limits / query timeouts — an agent loop *will* eventually scan your biggest table repeatedly.
- Accuracy numbers quoted only on Spider (a 2018 academic benchmark, largely saturated and unrepresentative of warehouse schemas).
