# Awesome DB Agent [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated, verified directory of **AI agents for databases** — systems that query, explore, manage, and act on databases through natural language or tool use: text-to-SQL agents, database copilots, MCP servers, analytics agents, the frameworks and semantic layers behind them, and the benchmarks that measure them.

Every entry was checked against its official site, docs, or repo on **2026-10-03**. Entries that could not be verified on an official source carry an honest `verified: false` flag in the machine-readable catalog ([`data/agents.json`](data/agents.json)) instead of a guessed description; license terms are quoted from official repos/pages, never inferred. Notable exclusions after checking official sources: **MindsDB** (current official positioning has pivoted to a general agent workspace, not a text-to-SQL DB agent) and a **Semantic Kernel SQL plugin** (no official DB-agent plugin verified).

## Contents

- [Text-to-SQL & NL2SQL Agents](#text-to-sql--nl2sql-agents)
- [Frameworks for Building DB Agents](#frameworks-for-building-db-agents)
- [Database Copilots & Platform AI Features](#database-copilots--platform-ai-features)
- [MCP Servers & Agent Tooling](#mcp-servers--agent-tooling)
- [Agentic Analytics & BI Agents](#agentic-analytics--bi-agents)
- [Benchmarks & Research](#benchmarks--research)
- [Guides](#guides)
- [Contributing](#contributing)
- [License](#license)

---

## Text-to-SQL & NL2SQL Agents

Dedicated systems whose core loop is turning natural language into executed SQL.

| Name | Org | What it does | License / Model | OSS |
|---|---|---|---|---|
| [Vanna AI](https://github.com/vanna-ai/vanna) | Vanna AI | Turns natural-language questions into SQL and answers by chatting with a SQL database using agentic retrieval over schema and example queries. | MIT | Yes |
| [WrenAI](https://github.com/Canner/WrenAI) | Canner | Open-source generative BI engine that gives AI agents a governed semantic layer (MDL) and context layer to turn business questions into SQL and dashboards across 22+ data sources. | Apache-2.0 (core) | Yes |
| [DB-GPT](https://github.com/eosphoros-ai/DB-GPT) | eosphoros-ai | Open-source agentic AI data assistant that connects to databases and other data sources, writes SQL autonomously from natural language, and generates reports and analysis. | MIT | Yes |
| [Dataherald](https://github.com/dataherald/dataherald) | Dataherald | Natural language-to-SQL engine built for enterprise-level question answering over relational data, exposed through an API. | Apache-2.0 | Yes |
| [Defog SQLCoder](https://github.com/defog-ai/sqlcoder) | Defog | Family of open large language models fine-tuned for converting natural-language questions into SQL queries. | Apache-2.0 (code); CC BY-SA 4.0 (weights) | Yes |
| [Chat2DB](https://github.com/CodePhiliaX/Chat2DB) | OtterMind | Cross-platform, local-first database client and SQL workspace that uses a bring-your-own AI model to generate, explain, and optimize queries across 40+ databases. | Apache-2.0 with additional conditions (source-available) | No |
| [DataLine](https://github.com/RamiAwar/dataline) | Rami Awar | AI-driven data analysis and visualization tool that connects to Postgres, Snowflake, MySQL, SQLite, and CSV files and generates and executes SQL from natural language. | GPL-3.0 | Yes |
| [AI2sql](https://ai2sql.io/ai-to-sql-converter) | AI2sql (Cross Regions Technology) | Transforms plain-English requests into SQL queries, optionally mapped to a database schema to construct statements. | SaaS subscription | No |
| [SQL Chat](https://github.com/sqlchat/sqlchat) | SQL Chat | Chat-based SQL client that uses natural language to query and operate databases including MySQL, PostgreSQL, MSSQL, TiDB Cloud, and OceanBase. | MIT | Yes |

## Frameworks for Building DB Agents

Agent frameworks, semantic layers, and query layers used to build governed database agents.

| Name | Org | What it does | License / Model | OSS |
|---|---|---|---|---|
| [LangChain SQL Agent](https://docs.langchain.com/oss/python/langgraph/sql-agent) | LangChain | Documented LangGraph pattern for building a custom agent that answers questions about a SQL database using database tools and query-checking steps. | MIT | Yes |
| [LlamaIndex NLSQL](https://github.com/run-llama/llama_index) | LlamaIndex | NLSQLTableQueryEngine constructs natural-language queries synthesized into SQL over a SQLDatabase wrapper, with response synthesis. | MIT | Yes |
| [Haystack](https://github.com/deepset-ai/haystack) | deepset | Open-source AI orchestration framework whose official cookbook shows building a pipeline that generates SQL and queries a SQL database with a custom component. | Apache-2.0 | Yes |
| [Cube](https://github.com/cube-js/cube) | Cube | Open-source semantic layer where metrics, dimensions, joins, and access rules are defined once and exposed through SQL, REST, and GraphQL APIs to BI tools, applications, and AI agents. | Apache-2.0 | Yes |
| [dbt Semantic Layer](https://docs.getdbt.com/docs/use-dbt-semantic-layer/sl-architecture) | dbt Labs | Powered by MetricFlow, the dbt Semantic Layer lets data teams define metrics in the modeling layer and query them consistently in downstream tools; AI tools can connect through the dbt MCP server. | Apache-2.0 (MetricFlow); proprietary (hosted layer) | No |
| [Malloy](https://github.com/malloydata/malloy) | Malloy | Open-source semantic modeling and query language built on top of SQL that describes data relationships and transformations and executes through an existing SQL engine; models can be served via REST and MCP APIs. | MIT | Yes |
| [Wren MDL](https://docs.getwren.ai/oss/concepts/what_is_context) | Canner | Wren AI's Modeling Definition Language: a versionable semantic contract describing models, relationships, calculated fields, and views, forming the governed context layer for WrenAI's text-to-SQL. | Apache-2.0 | Yes |

## Database Copilots & Platform AI Features

AI assistants built into database platforms, consoles, and database tools.

| Name | Org | What it does | License / Model | OSS |
|---|---|---|---|---|
| [Supabase AI Assistant](https://supabase.com/docs/guides/ai-tools) | Supabase | Supabase's dashboard AI Assistant helps with schema design, SQL, RLS policies, functions, and error debugging, complemented by Supabase's MCP server for AI agents. | SaaS subscription | No |
| [DBeaver AI Assistant](https://dbeaver.com/docs/dbeaver/AI-Tools-and-MCP/) | DBeaver Corp | Generates and explains SQL from natural language and can act on databases through built-in AI tools and connected MCP servers; fuller AI Chat and tooling ship in PRO editions. | Apache-2.0 (Community) | Yes |
| [Snowflake Cortex Analyst](https://docs.snowflake.com/en/user-guide/snowflake-cortex/cortex-agents) | Snowflake | Generates SQL over structured data from natural language using a semantic view, and is available as a tool inside Cortex Agents. | SaaS subscription | No |
| [Databricks Genie](https://docs.databricks.com/gcp/en/genie) | Databricks | AI experience for asking data questions in natural language, with answers grounded in organization data governed through Unity Catalog (Genie Agents, formerly Genie Spaces). | SaaS subscription | No |
| [Gemini in BigQuery](https://docs.cloud.google.com/bigquery/docs/gemini-overview) | Google Cloud | AI assistance in BigQuery Studio to explore data, chat with data via conversational analytics and data agents, and generate SQL and Python. | SaaS subscription | No |
| [Microsoft Copilot in Azure SQL Database](https://learn.microsoft.com/en-us/azure/azure-sql/copilot/copilot-azure-sql-overview?view=azuresql) | Microsoft | Conversational interface in the Azure portal to ask database questions and generate T-SQL using database context, DMVs, Query Store, and documentation. | SaaS subscription | No |
| [Amazon Q generative SQL](https://aws.amazon.com/q/developer/features/) | AWS | Amazon Q generative SQL in the Amazon Redshift Query Editor recommends SQL from natural-language intent, analyzing query patterns and schema metadata. | SaaS subscription | No |
| [MongoDB Compass Intelligent Assistant](https://www.mongodb.com/docs/compass/query-with-natural-language/compass-ai-assistant/) | MongoDB | Compass's intelligent assistant answers natural-language questions, helps debug errors, and uses read-only, user-approved tools to query the connected MongoDB deployment. | SaaS subscription | No |
| [Oracle Select AI](https://docs.oracle.com/en/database/oracle/oracle-database/26/nfcoa/select_ai.html) | Oracle | Lets users interact with Oracle AI Database using natural language to generate, run, and explain SQL via DBMS_CLOUD_AI, with an agent framework via DBMS_CLOUD_AI_AGENT. | SaaS subscription | No |
| [ClickHouse AI-powered SQL generation](https://clickhouse.com/docs/guides/use-cases/ai-ml/ai-powered-sql-generation) | ClickHouse | From ClickHouse 25.7, ClickHouse Client and clickhouse-local convert natural-language descriptions into SQL using built-in schema-discovery tools. | Apache-2.0 | Yes |
| [pgAdmin AI Assistant](https://www.pgadmin.org/docs/pgadmin4/latest/query_tool.html) | pgAdmin project | pgAdmin 4's Query Tool includes an AI Assistant tab that generates SQL from natural language by analyzing the database schema, after an AI provider is configured. | PostgreSQL/Artistic license | Yes |

## MCP Servers & Agent Tooling

Model Context Protocol servers that expose databases as tools to general-purpose agents.

| Name | Org | What it does | License / Model | OSS |
|---|---|---|---|---|
| [MCP Reference Servers (archived)](https://github.com/modelcontextprotocol/servers-archived) | modelcontextprotocol | The original MCP reference servers, including the Postgres and SQLite reference implementations, are archived and no longer maintained; current servers live in modelcontextprotocol/servers. | MIT | Yes |
| [Postgres MCP Pro](https://github.com/crystaldba/postgres-mcp) | crystaldba | Community MCP server giving agents configurable read/write access to Postgres plus performance-analysis tooling. | MIT | Yes |
| [mcp-server-mysql (benborla)](https://github.com/benborla/mcp-server-mysql) | benborla | Community Model Context Protocol server providing read-only access to MySQL databases: schema inspection and read-only queries for LLMs. | MIT | Yes |
| [MongoDB MCP Server](https://github.com/mongodb-js/mongodb-mcp-server) | MongoDB (mongodb-js) | MongoDB's official Model Context Protocol server to connect AI agents to MongoDB databases and MongoDB Atlas clusters. | Apache-2.0 | Yes |
| [ClickHouse MCP Server](https://github.com/ClickHouse/mcp-clickhouse) | ClickHouse | ClickHouse's official MCP server for querying ClickHouse from MCP-compatible agents. | Apache-2.0 | Yes |
| [MotherDuck MCP Server](https://github.com/motherduckdb/mcp-server-motherduck) | MotherDuck | MotherDuck's official local MCP server for DuckDB and MotherDuck. | MIT | Yes |
| [Redis MCP Server](https://github.com/redis/mcp-redis) | Redis | Redis's official MCP Server: a natural-language interface designed for agentic applications to manage and search data in Redis efficiently. | MIT | Yes |
| [MSSQL MCP servers (community)](https://github.com/RichardHan/mssql_mcp_server) | Community | No official Microsoft SQL Server MCP server was verified on official Microsoft sources as of October 2026; community servers (for example RichardHan/mssql_mcp_server) exist and are unaudited. | Unknown | No |
| [MCP Toolbox for Databases](https://github.com/googleapis/genai-toolbox) | Google (googleapis) | Google's open-source MCP server for databases, providing prebuilt and custom tools across many database engines; the repo now points to googleapis/mcp-toolbox. | Apache-2.0 | Yes |
| [Supabase MCP Server](https://github.com/supabase-community/supabase-mcp) | Supabase (supabase-community) | Supabase's official MCP server connecting AI assistants to Supabase projects and Postgres databases. | Apache-2.0 | Yes |
| [Neon MCP Server](https://github.com/neondatabase/mcp-server-neon) | Neon (neondatabase) | Neon's official MCP server for interacting with the Neon Management API and databases using natural language. | MIT | Yes |
| [AWS Labs MCP Servers for Databases](https://github.com/awslabs/mcp) | AWS Labs (awslabs) | AWS Labs' official open-source MCP monorepo, including database servers for DynamoDB, Aurora PostgreSQL/MySQL/DSQL, DocumentDB, Neptune, and Redshift. | Apache-2.0 | Yes |
| [Snowflake MCP Server (Snowflake-Labs)](https://github.com/Snowflake-Labs/mcp) | Snowflake-Labs | Snowflake-Labs' MCP server for Cortex AI, object management, and SQL orchestration — deprecated upstream in favor of Snowflake's official managed MCP server. | Apache-2.0 | Yes |
| [Qdrant MCP Server](https://github.com/qdrant/mcp-server-qdrant) | Qdrant | Qdrant's official Model Context Protocol server implementation for the Qdrant vector database. | Apache-2.0 | Yes |
| [PlanetScale MCP Server](https://planetscale.com/blog/introducing-planetscale-mcp-server) | PlanetScale | PlanetScale's hosted MCP server exposing organizations, databases, branches, schema, and Insights data to MCP-compatible AI tools, with optional read/write query execution. | SaaS subscription | No |
| [Turso MCP Server](https://github.com/tursodatabase/turso-mcp) | Turso | Turso's hosted MCP server connecting AI coding agents to Turso Cloud to manage organizations, databases, and groups and run SQL, with OAuth login. | MIT | Yes |

## Agentic Analytics & BI Agents

Analytics products whose agents query databases and warehouses to answer business questions.

| Name | Org | What it does | License / Model | OSS |
|---|---|---|---|---|
| [Hex Magic (Hex AI agents)](https://hex.tech/blog/why-hex-doesnt-require-an-ai-add-on/) | Hex Technologies | Hex's Magic AI features generate SQL, edit Python, and build charts and analyses from prompts using warehouse schemas and project context. | SaaS subscription | No |
| [ThoughtSpot Sage](https://www.thoughtspot.com/press-releases/thoughtspot-experiences-historic-year-of-growth-as-customers-around-the-world) | ThoughtSpot | AI-powered search experience that lets users get insights from data through natural-language search using foundation models within ThoughtSpot's search technology; ThoughtSpot now also promotes the Spotter conversational experience. | SaaS subscription | No |
| [Mode AI Assist](https://mode.com/help/articles/ai-assist) | Mode (ThoughtSpot) | Generates SQL in Mode's SQL editor from natural-language comments embedded in queries, for any warehouse the user can query; enabled per account on request. | SaaS subscription | No |
| [Metabase Metabot](https://github.com/metabase/metabase) | Metabase | Metabase's AI that gives answers, helps write queries, and can be extended via an AI agent API to query data. | AGPL-3.0 (OSS edition) | Yes |
| [Seek AI](https://www.seek.ai/blog/seek-ai-supports-microsoft-sql-server-for-natural-language-querying-of-data-2) | Seek AI | Natural-language interface that queries structured data sources (including SQL Server, Snowflake, and other warehouses) and returns answers in plain English. | SaaS subscription | No |
| [Julius AI](https://julius.ai/) | Julius AI | AI data-analysis tool that turns analysis into conversations: users upload files or connect databases and get visualizations without coding. | SaaS subscription | No |
| [Dust](https://docs.dust.tt/docs/user-documentation/agents/discover-knowledge) | Dust | Agent platform whose Discover Knowledge capability explores data-warehouse tables and runs SQL analysis on Snowflake and BigQuery to answer quantitative questions. | SaaS subscription | No |

## Benchmarks & Research

Text-to-SQL benchmarks, evaluation harnesses, and the influential open methods behind modern DB agents.

| Name | Org | What it does | License / Model | OSS |
|---|---|---|---|---|
| [Spider](https://github.com/taoyds/spider) | Yale (taoyds) | Large human-labeled dataset for complex and cross-domain semantic parsing and the text-to-SQL task over relational databases. | Apache-2.0 | Yes |
| [Spider 2.0](https://github.com/xlang-ai/Spider2) | XLANG Lab (xlang-ai) | Evaluates language models on real-world enterprise text-to-SQL workflows, with Snowflake, Lite, and DBT settings. | MIT | Yes |
| [BIRD](https://bird-bench.github.io/) | BIRD-bench / Alibaba DAMO-ConvAI | Large-scale cross-domain text-to-SQL benchmark emphasizing database values, external knowledge, and query efficiency. | Research dataset/paper | Yes |
| [DAIL-SQL](https://github.com/BeachWang/DAIL-SQL) | BeachWang | Approach for optimizing LLM utilization on text-to-SQL through few-shot example selection and prompt organization; a method, not a dataset. | Apache-2.0 | Yes |
| [CHESS](https://github.com/ShayanTalaei/CHESS) | ShayanTalaei | Contextual Harnessing for Efficient SQL Synthesis: a multi-agent framework (information retriever, schema selector, candidate generator, unit tester) for text-to-SQL. | Apache-2.0 | Yes |
| [MAC-SQL](https://github.com/wbbeyourself/MAC-SQL) | wbbeyourself | Multi-agent collaborative framework for text-to-SQL with selector, decomposer, and refiner agents. | Unknown (no license file verified) | No |
| [DIN-SQL](https://github.com/MohammadrezaPourreza/Few-shot-NL2SQL-with-prompting) | Mohammadreza Pourreza | Decomposed in-context learning of text-to-SQL with self-correction: schema linking, classification, generation, and self-correction modules. | MIT | Yes |
| [Defog sql-eval](https://github.com/defog-ai/sql-eval) | Defog (defog-ai) | The open evaluation harness Defog uses for evaluating generated SQL, built for reproducible comparisons. | Apache-2.0 | Yes |
| [KaggleDBQA](https://github.com/chia-hsuan-lee/kaggledbqa) | Microsoft Research authors | Challenging cross-domain evaluation dataset of real web (Kaggle) databases, with domain-specific data types, original formatting, and unrestricted questions. | Other (NOASSERTION) | No |
| [CoSQL](https://yale-lily.github.io/cosql) | Yale LILY | Corpus for building cross-domain conversational text-to-SQL systems. | CC BY-SA 4.0 | Yes |
| [SParC](https://yale-lily.github.io/sparc) | Yale & Salesforce | Semantic parsing and text-to-SQL in context: context-dependent, multi-turn questions built upon the Spider dataset. | CC BY-SA 4.0 | Yes |

## Guides

- [Choosing a DB agent](docs/choosing-a-db-agent.md) — platform copilot vs OSS text-to-SQL vs MCP tooling, and how to evaluate with your own questions.
- [Architecture patterns](docs/architecture-patterns.md) — the core agent loop, schema linking, semantic layers, MCP tool exposure, and the production safety checklist.
- [Benchmarks & evals](docs/benchmarks-and-evals.md) — Spider vs BIRD vs Spider 2.0, the influential methods, and how to read vendor accuracy claims.
- [Glossary](docs/glossary.md) — text-to-SQL, semantic layer, MDL, execution accuracy, self-correction, and friends.
- [Status changes](docs/status-changes.md) — rebrands, deprecations, and shutdowns, newest first.
- [Machine-readable catalog](data/agents.json) — every entry with license, open-source, and verification flags.

## Contributing

Entries and corrections are welcome — see [CONTRIBUTING.md](CONTRIBUTING.md). Every PR is checked by CI: lychee link check over all markdown files (also re-run monthly to catch link rot) and JSON validation of `data/agents.json`, including the exact field set and category values documented in CONTRIBUTING.md.

## License

[MIT](LICENSE) © 2026 dakotac1994
