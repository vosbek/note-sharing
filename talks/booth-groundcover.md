---
title: "groundcover: eBPF observability in your own cloud, readable by coding agents over MCP"
---

# groundcover: eBPF observability in your own cloud, readable by coding agents over MCP

Booth visit: groundcover · QCon SF 2026 · Wed Nov 18

> groundcover collects logs, traces and metrics with an eBPF sensor and keeps them in your own cloud, and lets Claude Code or Cursor query them through an MCP server.

## Key points

- An eBPF sensor collects infrastructure, application and AI-workflow telemetry with no code changes, and OpenTelemetry is supported natively.
- In their bring-your-own-cloud model the backend runs in your VPC, managed by groundcover, and they host the UI; a separate on-premises tier runs both backend and UI on your side.
- Their AI observability tracks LLM calls and agent pipelines in production, including cost and latency.
- The MCP server gives Cursor and Claude Code tools to query logs, traces, metrics, events, monitors and Kubernetes objects.
- Pricing is per monitored host: free with 12-hour retention, Pro $30, Enterprise $35 and on premises $50 a host a month, by their pricing page.

Booth, Wednesday Nov 18. Sources: groundcover's homepage, pricing page and MCP server page, read Nov 18, 2026. Figures and claims are the vendor's own until we test them.

## What it is

groundcover is an observability platform for Kubernetes and Linux hosts. It collects telemetry with an eBPF sensor instead of code instrumentation, and stores it in the customer's own cloud rather than a vendor SaaS. It now adds monitoring for LLM calls and agents, and an MCP server so coding agents can query the data.

## How it works

- **Sensor.** An eBPF sensor on each node collects and processes logs, traces and metrics at the edge, with no code changes. OpenTelemetry data is accepted too.
- **Storage.** In the bring-your-own-cloud model a backend runs in your VPC and groundcover operates it. The on-premises tier also moves the UI and authentication to your side.
- **AI observability.** Traces LLM calls and agent pipelines, with cost and latency.
- **Agents.** An MCP server with tools such as query_logs, query_traces, query_metrics and get_k8s_object_yaml, and an in-product Agent Mode you can teach your team's conventions with skills.

## Where it connects to the talks

[OpenAI](building-a-100m-product-at-openai.md) talked about agents debugging production, including one that deleted slow pods when it was only asked to debug. Giving agents read access to telemetry is the useful half of that; groundcover sells a read-only query surface for it.

## Docs and getting started

- [groundcover docs](https://docs.groundcover.com/)
- [MCP setup](https://docs.groundcover.com/getting-started/groundcover-mcp)
- [Bring-your-own-cloud architecture](https://www.groundcover.com/byoc)
- [Pricing](https://www.groundcover.com/pricing)
- [Playground](https://play.groundcover.com/)
