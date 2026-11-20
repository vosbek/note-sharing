---
title: "Testkube: existing test suites run inside our own Kubernetes clusters, reachable from agents"
kind: "booth"
company: "Testkube"
day: "2026-11-18"
summary: "Testkube orchestrates the test tools teams already have from runners in their own clusters, and adds AI test authoring, failure-triage agents and an MCP server."
---

# Testkube: existing test suites run inside your own Kubernetes clusters, reachable from agents

Booth visit: Testkube · QCon SF 2026 · Wed Nov 18

> Testkube orchestrates the test tools teams already have from runners in their own clusters, and adds AI test authoring, failure-triage agents and an MCP server.

## Key points

- Their site says the runners always run in your own infrastructure and are open source. The control plane that schedules and reports on tests runs in their cloud, or on premises and air-gapped on Enterprise.
- It drives tools such as Playwright, Cypress, k6, JMeter, pytest, Postman and Selenium, triggered from GitHub Actions, GitLab, Jenkins, Argo CD, webhooks or Kubernetes events.
- Testkube AI writes a test from a plain-language scenario, runs it in your cluster and opens a pull request. Its agents analyze failures, separate flaky tests from real ones and can open fix pull requests.
- The MCP server exposes the full API to Claude, Cursor, Copilot and other clients, and is the one AI feature included in the free open-source tier.
- The pricing page lists Pro at $700 a month per runner agent with 50 AI sessions, and Enterprise at a custom price. Paid AI plans use your own OpenAI or Anthropic account.

Booth, Wednesday Nov 18. Sources: Testkube's homepage, AI page, pricing page and MCP docs, read Nov 18, 2026. Figures and claims are the vendor's own; I haven't tested them.

## What it is

Testkube is a test orchestration platform for Kubernetes. It does not replace your test frameworks. It runs the suites you already have from inside your own clusters, collects the logs and artifacts, and gives you one place to trigger, schedule and analyze them. The core is open source.

## How it works

- **Runners.** Agents installed in your clusters with Helm execute the tests, listen for Kubernetes events and sync results back. They are open source and can run standalone.
- **Control plane.** The dashboard, scheduling, analytics and RBAC. It runs in Testkube's cloud on Pro, or on premises and air-gapped on Enterprise.
- **Triggers.** Plugins and webhooks for GitHub Actions, GitLab, Jenkins and Argo CD, plus Kubernetes events and CDEvents.
- **AI.** Test authoring from a plain-language scenario, committed as a pull request; agents that read failures, rerun to separate flaky tests and post summaries to Slack or Jira; and an MCP server over the full API.

## Where it connects to the talks

Several speakers put the proof of a change ahead of the human read. [OpenAI](building-a-100m-product-at-openai.md) climbs a verification ladder, and [Harness Cosmos](drawing-the-rest-of-the-owl.md) puts a verifier in its review lane. Testkube sells the plumbing for running ordinary test suites in that lane. [Antithesis](booth-antithesis.md) is the heavier option for distributed systems.

## Docs and getting started

- [Testkube docs](https://docs.testkube.io)
- [Open-source repository](https://github.com/kubeshop/testkube)
- [Testkube AI overview](https://testkube.io/ai)
- [MCP server setup](https://docs.testkube.io/articles/mcp-overview)
- [Pricing](https://testkube.io/pricing)
