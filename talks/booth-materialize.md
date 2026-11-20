---
title: "Materialize: a live context layer kept current from operational data"
kind: "booth"
company: "Materialize"
day: "2026-11-16"
summary: "Materialize keeps SQL views over operational databases, ERPs and CRMs up to date as the data changes, and offers them to agents as live context."
---

# Materialize: a live context layer kept current from operational data

Booth visit: Materialize · QCon SF 2026 · Mon Nov 16

> Materialize keeps SQL views over operational databases, ERPs and CRMs up to date as the data changes, and offers them to agents as live context.

## Key points

- Their page says agents see the effect of a tool call in about a second, and can query it directly through MCP.
- It can keep vector embeddings current for retrieval, and take heavy queries off operational databases.
- It comes as a managed cloud, self-managed in your own cloud, or a local emulator, and the page mentions air-gapped deployment; pricing is not shown.
- The customer figures on the page, such as a 30x cut in context engineering cycle time at Zepz, are the vendor's own.

Booth, Monday Nov 16. Sources: Materialize's site and docs, read Nov 17, 2026. Figures and claims are the vendor's own; I haven't tested them.

## What it is

Materialize keeps SQL views over operational databases, ERPs and CRMs current as the data changes, using incremental computation. It positions itself as a live context layer that agents query directly, including over MCP.

## How it works

- **Incremental views.** Results update as source data changes, doing only the work needed, without loading the source databases.
- **SQL data products.** Any engineer who knows SQL can define live business objects to query or push downstream.
- **Agents.** Agents query the live views directly or through MCP; the vendor says they see the effect of a tool call in about a second.
- **Vectors.** Embeddings can be kept current as source rows change.

## Where it connects to the talks

Several talks argued agents act on stale context. Materialize and Tacnode are the two data-side answers at the conference: keep the facts an agent reads current, rather than giving it a bigger snapshot.

## Docs and getting started

- [Quick start](https://materialize.com/docs/get-started/)
- [Install the emulator](https://materialize.com/docs/get-started/install-materialize-emulator/)
- [Key concepts](https://materialize.com/docs/concepts/)
- [Guides](https://materialize.com/guides/)
