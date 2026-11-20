---
title: "Unblocked: a context layer for coding agents"
---

# Unblocked: a context layer for coding agents

Booth visit: Unblocked · QCon SF 2026 · Mon Nov 16

> Unblocked gives coding agents context from conversations, issues, docs and production systems as well as code.

## Key points

- Their site calls it a context layer for agentic software development that resolves conflicts between sources and weighs how recent each one is.
- Unblocked comes as an MCP server for Cursor, Claude Code and Copilot, a CLI, a Slack bot, a web search page and an API.
- Their site lists SOC 2 Type II, SSO and SCIM. It says customer data is never used to train models, and it describes no self-hosted option.
- Their site shows customer-reported savings, such as faster onboarding, that are not independently verified.

Booth, Monday Nov 16. Sources: Unblocked's site and docs, read Nov 17, 2026. Figures and claims are the vendor's own until we test them.

## What it is

Unblocked is a context layer for software teams and their agents. It connects code, conversations, issues, docs and production systems into one knowledge graph that agents and people can query, and adds AI code review and a task-to-draft-PR agent on top.

## How it works

- **Sources.** Code plus systems such as GitHub, Jira, Confluence and Slack.
- **Conflict resolution.** Weighs recency and authority when sources disagree, and scopes answers to the user's permissions.
- **Conventions.** Mines team conventions from pull request feedback, the same raw material Roblox used for exemplars.
- **Delivery.** MCP server for Cursor, Claude Code and Copilot; a CLI; a Slack bot; web search; an API.

## Where it connects to the talks

[Roblox](generation-got-cheap-trust-didnt.md) spent months building exemplars from its review history. Unblocked offers a packaged version of the same idea, mining conventions from PR feedback, plus cross-tool context.

## Docs and getting started

- [Docs](https://docs.getunblocked.com)
- [Product overview](https://getunblocked.com)
