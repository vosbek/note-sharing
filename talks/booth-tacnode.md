---
title: "Tacnode: a Context Lake for real-time automated decisions"
kind: "booth"
company: "Tacnode"
day: "2026-11-16"
summary: "Tacnode sells a Context Lake: one store that holds what an automated decision reads and what it decided, kept current in one consistent snapshot."
---

# Tacnode: a Context Lake for real-time automated decisions

Booth visit: Tacnode · QCon SF 2026 · Mon Nov 16

> Tacnode sells a Context Lake: one store that holds what an automated decision reads and what it decided, kept current in one consistent snapshot.

## Key points

- Their page describes real-time ingestion with ACID transactions, continuously updated materialized views, and one query engine over rows, JSON and vector embeddings.
- Their page presents it as shared memory so several agents and decision systems act on the same current state.
- Their examples are fraud detection, dynamic pricing, personalization and ad bidding; the performance claims on the page come without benchmarks.
- It links an AWS Marketplace listing and shows SOC 2 Type II, HIPAA and GDPR badges; pricing is not shown.

Booth, Monday Nov 16. Sources: Tacnode's Context Lake page and its canonical specification, read Nov 17, 2026. Figures and claims are the vendor's own; I haven't tested them.

## What it is

Tacnode sells a Context Lake: one system that stores both the data an automated decision reads and the decisions it made, kept current in a single consistent state so several agents and decision systems act on the same facts. It presents this as an alternative to data lakes, warehouses and lakehouses for real-time AI.

## How it works

- **Ingestion as system of record**, with distributed ACID transactions.
- **Continuous transformation** through incrementally updated materialized views.
- **One query engine** over rows, JSON and vector embeddings in one plan.
- **Storage and scaling.** Columnar plus hybrid storage on disaggregated storage, with separate resource pools for ingestion, transformation, exploration and retrieval.

## Where it connects to the talks

Almost every booth was about context management. Tacnode is the data-side version, aimed at fraud, pricing and ad-bidding decisions rather than coding agents.

## Docs and getting started

- [Context Lake overview](https://tacnode.io/context-lake)
- [Docs](https://tacnode.io/docs)
- [Context Lake canonical specification](https://contextlake.org/canonical)
