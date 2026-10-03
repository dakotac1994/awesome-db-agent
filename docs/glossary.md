# Glossary

Terms that recur across database-agent products, papers, and MCP tooling.

- **Text-to-SQL / NL2SQL** — translating a natural-language question into a SQL query. The original name for the whole field; "DB agent" is the broader 2024+ term covering planning, execution, self-correction, and follow-ups around that core translation.
- **Execution accuracy (EX)** — the benchmark metric that matters: does the generated query, when *run*, produce the correct result set? Superior to exact-string-match because many SQL strings compute the same answer.
- **Schema linking** — deciding which tables/columns a question refers to. The hardest sub-problem on real schemas with thousands of tables and cryptic names; retrieval-augmented systems exist largely to solve it.
- **Semantic layer** — a governed model of metrics, dimensions, and joins (Cube, MetricFlow/dbt Semantic Layer, Malloy, Wren MDL) that sits between raw tables and consumers, so "revenue" means the same thing in every dashboard and agent answer.
- **MDL (Modeling Definition Language)** — Wren AI's open semantic-modeling format: models, fields, relationships, and calculated fields defined once and compiled to SQL per-dialect.
- **MCP (Model Context Protocol)** — Anthropic-originated open protocol for exposing tools/data sources to LLM agents. A database MCP server typically offers `list_tables`, `describe_table`, and `execute_sql` tools; clients (Claude, Cursor, custom agents) drive the database through them.
- **Self-correction loop** — feeding execution errors (unknown column, type error, empty set) back to the model so it can revise the query. Responsible for a large share of real-world accuracy gains over single-shot generation.
- **Few-shot example retrieval** — storing prior question→SQL pairs and injecting the most similar ones into the prompt. Teaches dialect, naming conventions, and business definitions that the schema alone doesn't carry.
- **Read-only guardrails** — the safety stack around an agent: read-only DB role, statement allow-listing, row limits, timeouts, cost estimation, and human approval for mutations. The difference between a demo and a deployable system.
- **Agentic analytics** — analytics workflows where an agent plans multi-step queries, runs them, checks intermediate results, and composes an answer/dashboard — as opposed to single-shot NL→chart. Hex Magic and ThoughtSpot's agent features are the commercial reference points.
- **Spider / BIRD** — the two canonical text-to-SQL benchmarks. Spider (2018, Yale) is largely saturated; BIRD (2023) adds dirty values, external knowledge, and efficiency measurement, and is the more meaningful comparison today.
- **DAIL-SQL / CHESS / MAC-SQL / DIN-SQL** — influential open methods (prompting strategies and multi-agent decompositions) whose reported BIRD/Spider numbers reset the leaderboard in 2023–2024; useful as architecture references even if you never run them.
