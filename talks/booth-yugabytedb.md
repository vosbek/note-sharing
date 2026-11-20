---
title: "YugabyteDB: distributed Postgres, with a database per agent and zero-copy branches"
kind: "booth"
company: "YugabyteDB"
day: "2026-11-18"
summary: "Yugabyte sells a distributed, PostgreSQL-compatible database and now pitches it for agents: isolated databases that scale to zero, branches to test against, and an MCP server."
---

# YugabyteDB: distributed Postgres, with a database per agent and zero-copy branches

Booth visit: YugabyteDB · QCon SF 2026 · Wed Nov 18

> Yugabyte sells a distributed, PostgreSQL-compatible database and now pitches it for agents: isolated databases that scale to zero, branches to test against, and an MCP server.

## Key points

- Their homepage describes a multi-master database that shards automatically and fails over across zones, regions and clouds, with Postgres compatibility including stored procedures, triggers and extensions.
- YugabyteDB AMP gives each agent its own Postgres database on shared infrastructure and scales idle databases to zero. It can branch a database onto separate compute, so an agent tests a change away from production.
- Four built-in agents set up, migrate, tune and integrate databases; Voyager, the migration agent, handles moves from Oracle, SQL Server and MongoDB.
- Their MCP server uses OIDC sign-in and keeps write tools disabled until an operator turns them on.
- The core database is open source under Apache 2.0; Aeon is the managed service (per-minute or vCPU subscription), and Anywhere is self-managed. No prices appear on the pages I read.

Booth, Wednesday Nov 18. Sources: Yugabyte's homepage, AMP page and deployment comparison, read Nov 18, 2026. Figures and claims are the vendor's own; I haven't tested them.

## What it is

YugabyteDB is a distributed SQL database that speaks PostgreSQL. It spreads data across nodes, zones and regions and keeps serving through failures. Yugabyte now markets it as "the distributed PostgreSQL database for agents and AI-native workloads", with a newer serverless product, AMP, built for running many small databases for agents.

## How it works

- **Core database.** Multi-master, auto-sharded, with rolling upgrades and failover across zones, regions and clouds.
- **AMP.** Serverless, multi-tenant Postgres. Each agent gets an isolated database, provisioned through an agent, MCP, the API or the UI. Idle databases scale to zero, and a workload that grows moves to the main database without migrating data.
- **Branching.** A zero-copy branch of a database runs on its own compute. Their example has an agent open three branches of production to diagnose a slow query.
- **Built-in agents.** Architect sets up, Voyager migrates, Perf Advisor tunes and Nexus manages connectors and streams, sharing context and keeping a trace of what they did.
- **AI features.** Vector search through SQL and pgvector, integrations with LangChain, LlamaIndex, Bedrock and Vertex AI, and MCP server version 2.0.

## Where it connects to the talks

OpenAI's top rung of verification was a sandbox running copies of live traffic ([their talk](building-a-100m-product-at-openai.md)). A cheap branch of a real database is the data half of that idea. On context, Yugabyte joins [Materialize](booth-materialize.md) and [Tacnode](booth-tacnode.md) as database vendors selling a layer agents read from.

## Docs and getting started

- [YugabyteDB docs](https://docs.yugabyte.com/)
- [AMP overview](https://www.yugabyte.com/amp/)
- [Deployment options compared](https://www.yugabyte.com/compare-products/)
- [Voyager migration](https://www.yugabyte.com/voyager/)
- [Download](https://download.yugabyte.com/#/)
