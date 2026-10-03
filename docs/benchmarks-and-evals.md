# Benchmarks & evals for database agents

Why every vendor claims "state of the art", and how to read the numbers.

## The canonical benchmarks

- **Spider** (Yale, 2018) — 10K questions over 200 small databases. The benchmark that launched the field — and the one to trust least in 2026: top systems score in the high 80s/low 90s, schemas are clean and tiny by warehouse standards, and years of leaderboard tuning mean scores measure benchmark familiarity as much as capability.
- **Spider 2.0** (2024) — the reality check: enterprise workflows over BigQuery/Snowflake/DuckDB, DBs with thousands of columns, questions requiring multiple steps and external knowledge. Scores collapsed versus Spider 1.0 — that's the point. If a vendor quotes one number, ask whether it's Spider 1.0 or 2.0.
- **BIRD** (2023) — 12K+ question-SQL pairs over 95 real-world databases with dirty values, plus external-knowledge requirements and an efficiency dimension (queries are timed, not just checked). The most meaningful public comparison today; serious text-to-SQL systems report BIRD execution accuracy.
- **KaggleDBQA** — real Kaggle databases with unnormalized schemas and genuine documentation needs; small but humbling.
- **CoSQL / SParC** — conversational text-to-SQL (multi-turn, context-dependent questions). Relevant if your agent must handle follow-ups, which is most real usage.

## The influential methods (and what they teach)

- **DIN-SQL** — decomposes the problem into schema-linking → classification → generation → self-correction modules. Its lesson: a pipeline of small, debuggable steps beats one mega-prompt.
- **DAIL-SQL** — few-shot example selection and prompt organization; showed example choice matters as much as model choice.
- **MAC-SQL** — multi-agent decomposition (selector, decomposer, refiner) — the template most "agentic" text-to-SQL systems still follow.
- **CHESS** — schema selection at scale plus candidate-generation-and-selection; notable for tackling wide schemas rather than assuming the schema fits in context.
- **Defog sql-eval** — an open eval harness (Postgres-focused) for running your own comparisons, part of a broader shift from static leaderboards to reproducible eval tooling.

## How to read a vendor's number

1. **Which benchmark?** Spider 1.0 numbers in 2026 are marketing. BIRD or Spider 2.0 numbers are at least current.
2. **Execution accuracy or string match?** Only execution accuracy (did the query return the right data) reflects user value.
3. **Which model underneath?** A framework scoring 85% with a frontier model may score 60% with the cheap model you'll actually deploy.
4. **What's the schema?** Academic schemas fit in a prompt. Your 4,000-table warehouse does not — ask about schema-linking/retrieval behavior at scale.
5. **What's in your eval?** Build your own set (30–50 real questions with known-correct answers; see [choosing-a-db-agent](choosing-a-db-agent.md)) before believing anyone's leaderboard. Every serious team ends up here; skip the months of vendor-number comparison and start here.

## The efficiency dimension

BIRD's valid-efficiency score and Spider 2.0's workflow framing both point the same way: a correct query that scans 2 TB and takes 9 minutes is a wrong answer in production. When evaluating agents, measure cost and latency per answered question alongside accuracy — the cheapest correct system usually wins the deployment.
