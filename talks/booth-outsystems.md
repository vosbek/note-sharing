---
title: "OutSystems: a low-code platform that outside coding agents drive through MCP"
---

# OutSystems: a low-code platform that outside coding agents drive through MCP

Booth visit: OutSystems · QCon SF 2026 · Wed Nov 18

> OutSystems now calls itself an agentic systems platform: its own agent builds apps, and Claude Code, Codex, Cursor or Kiro can build, deploy and roll back through its Coding MCP.

## Key points

- Mentor, their built-in coding agent, generates an app from a prompt, which you then inspect and refine visually in the IDE.
- Their Coding MCP is generally available on every OutSystems Developer Cloud (ODC) tenant. It lets Claude Code, Codex, Cursor or Kiro build apps, publish, promote between stages, roll back and read logs and traces.
- Their pages say agent actions run as the signed-in user, under existing ODC roles, approvals and audit trail. An Enterprise Context Graph maps apps, data and dependencies for the agent.
- Agent Workbench builds business-process agents with guardrails, evaluations, monitoring and a choice of LLM.
- Pricing is by quote, counted in Application Objects (screens, tables and API methods) and end users; a free Personal Edition covers up to 100 internal users.

Booth, Wednesday Nov 18. Sources: OutSystems's homepage, Agent Experience page, Coding MCP product update and pricing page, read Nov 18, 2026. Figures and claims are the vendor's own until we test them.

## What it is

OutSystems is a low-code platform that now positions itself as an "agentic systems platform" for building and running apps and agents, aimed at large regulated companies modernizing old systems. OutSystems Developer Cloud (ODC) is the cloud-native version the agent features are built on.

## How it works

- **Mentor.** Their own coding agent turns a prompt into an app model you then edit visually.
- **Coding MCP.** An MCP server, installed from their GitHub repository, that lets Claude Code, Codex, Cursor or Kiro hand build requests to Mentor, publish, check impact, promote, roll back and read health, logs and traces.
- **Enterprise Context Graph.** A live map of the apps, data and connections on the platform, so an agent can reuse components and trace dependencies before it changes anything.
- **Governance.** Agent actions inherit the user's RBAC, approval policies apply to high-impact changes, and changes are audited.
- **Agent Workbench.** Builds business-process agents with guardrails, evaluations, monitoring and a swappable LLM.

## Where it connects to the talks

A recurring point in [what we learned](../themes.md) was that limits on agents belong outside the prompt: scoped credentials, a separate identity, merge policy as code. OutSystems has built that into a platform: the agent can only do what the signed-in user's roles allow, and every change is audited.

## Docs and getting started

- [Coding MCP announcement](https://www.outsystems.com/product-updates/outsystems-coding-mcp)
- [Coding MCP repository](https://github.com/OutSystems/outsystems-mcp)
- [Agent Experience overview](https://www.outsystems.com/platform/agent-experience)
- [Documentation](https://success.outsystems.com/documentation)
- [Pricing and editions](https://www.outsystems.com/pricing-and-editions)
