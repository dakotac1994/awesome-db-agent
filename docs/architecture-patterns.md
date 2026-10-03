# Architecture patterns for database agents

How the systems in this list actually work, at the pattern level. Every DB agent is some combination of the pieces below — knowing which pieces a tool has (and which it fakes) is most of vendor evaluation.

## The core loop

1. **Schema intake** — the agent learns what it's querying: table/column names, types, relationships, and (in better systems) descriptions, sample values, and business definitions.
2. **Question → plan** — the model decomposes a natural-language question into steps ("find churned accounts, then their last payment") instead of jumping straight to one SQL statement.
3. **SQL/code generation** — one or more SQL statements (or pandas/API calls) are generated against the schema context.
4. **Execution sandbox** — queries run somewhere safe: read-only credentials, row limits, timeouts, and cost guards. *This is the layer that decides whether an agent is a demo or a production tool.*
5. **Self-correction** — errors (missing column, type mismatch, empty result) are fed back to the model for a retry. This loop is where most real-world accuracy comes from.
6. **Answer synthesis** — results are turned back into prose, a table, or a chart, ideally with the SQL shown for verification.

## Pattern 1: Bare text-to-SQL

The model gets the schema (or the top-K relevant tables) and writes SQL directly. Vanna AI, Defog SQLCoder, and most "chat with your database" tools start here.

- **Strengths:** simple, works with any LLM, easy to self-host.
- **Weaknesses:** schema doesn't fit in context on real warehouses; column names like `amt_2` carry no semantics, so the model guesses; accuracy collapses on multi-join questions without help.

## Pattern 2: Retrieval-augmented schema & example linking

Instead of dumping the whole schema, the system embeds tables/columns/DDL and retrieves only what's relevant, plus similar past question→SQL pairs. Vanna's training data (DDL + documentation + SQL pairs in a vector store) is the canonical open-source version.

- **Strengths:** scales to thousands of tables; past examples teach house style (naming, filters, fiscal calendars).
- **Weaknesses:** retrieval misses are silent — the agent answers confidently against the wrong tables.

## Pattern 3: Semantic-layer-mediated querying

The agent never writes raw SQL against warehouse tables. It queries a **semantic layer** — Cube, dbt Semantic Layer (MetricFlow), Malloy, or Wren's MDL — where metrics, dimensions, and joins are pre-defined and governed.

- **Strengths:** the model composes *metrics* ("monthly recurring revenue by plan") instead of inventing joins; numbers match the company's dashboards by construction; this is the architecture behind Databricks Genie, Snowflake Cortex Analyst, and ThoughtSpot's agent features.
- **Weaknesses:** someone has to build and maintain the semantic model; ad-hoc questions outside the modeled surface fall back to raw SQL or fail.

## Pattern 4: Platform-native copilots

The database vendor embeds the agent in its own console: Supabase's AI assistant, Snowflake Copilot, Gemini in BigQuery. They have privileged context (query history, storage layout, your actual data profile) that third-party tools must approximate.

- **Strengths:** zero setup, best schema context, inherits platform auth.
- **Weaknesses:** locked to one platform; quality varies wildly by vendor; hard to eval against alternatives.

## Pattern 5: MCP tool exposure

Instead of building an agent, expose the database as **tools** — `execute_sql`, `list_tables`, `describe_table` — over the Model Context Protocol, and let a general agent (Claude, Cursor, your own LangGraph app) drive. Google's MCP Toolbox for Databases and the vendor MCP servers (MongoDB, ClickHouse, Neon, Supabase) are the reference points.

- **Strengths:** one integration, every MCP client can use it; auth and guardrails live server-side.
- **Weaknesses:** the agent is only as good as the client model; tool surface design (granularity, pagination, result-size limits) becomes your problem.

## Safety checklist (applies to every pattern)

- **Read-only role** for the agent's DB credentials unless writes are the explicit point.
- **Row/cost limits and timeouts** on every generated query — an agent loop can run a full-table scan 40 times in a minute.
- **Human-in-the-loop** for mutations and for answers that feed decisions; show the SQL, not just the prose.
- **Audit log** of generated queries + prompts; you will need it the first time a number is wrong.
- **Eval harness** on your own questions before trusting any vendor benchmark number (see [benchmarks-and-evals](benchmarks-and-evals.md)).
