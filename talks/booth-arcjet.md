---
title: "Arcjet: runtime security policy for AI agents and coding agents"
---

# Arcjet: runtime security policy for AI agents and coding agents

Booth visit: Arcjet · QCon SF 2026 · Mon Nov 16

> Arcjet enforces security policy at the moment an agent acts: in application code through an SDK, and in coding agents such as Claude Code and Copilot through their hooks.

## Key points

- Their docs describe three jobs: observe which agents run and what they do, enforce policy before an action's side effect happens, and keep decisions as audit evidence.
- Applications call protect() on requests or guard() on tool calls, MCP servers and queue consumers; the SDKs cover JavaScript and TypeScript, Python and Go.
- For coding agents there is no SDK: Arcjet enforces policy through the hooks Claude Code, GitHub Copilot, Cursor and OpenAI Codex already fire, installed through managed settings.
- Rules include prompt injection and sensitive data detection, token budgets, bot protection and a WAF. Some run locally in WebAssembly and others call Arcjet's cloud API, which the docs say adds 20 to 30 ms.
- Published pricing runs from a free tier to Individual at $25 and Startup at $299 a month plus usage; Enterprise is custom and adds a log drain to a SIEM.

Booth, Monday Nov 16. Sources: Arcjet's docs and its build-versus-buy page, read Nov 17, 2026. Figures and claims are the vendor's own until we test them.

## What it is

Arcjet is a runtime security platform for AI applications and agents. It started as a developer SDK for bot protection, rate limiting and a web application firewall, and in September 2026 added an agent runtime product. Its docs describe three jobs: observe which agents are running and what they do, enforce policy before an action has a side effect, and record each decision with the policy behind it as evidence.

## How it works

- **In your code.** Call `protect()` on an HTTP request, or `guard()` where there is no request: tool handlers, MCP servers, queue consumers. Guards are chosen by a label naming the action, so security can change what a label allows through remote policy without a code change.
- **In coding agents, with no SDK.** Policy runs through the hooks Claude Code, GitHub Copilot, Cursor, OpenAI Codex and Muse Code already fire, installed through managed settings. Decisions happen at the tool call, the prompt, or a model switch.
- **Rules.** Prompt injection detection, sensitive information detection, token-bucket budgets, destination threat checks, bot protection, a WAF, email validation and custom rules.
- **Where rules run.** Some run in-process in WebAssembly, including local sensitive-data detection where the body is not sent. Others call Arcjet's cloud API, which the docs say adds 20 to 30 ms per request; prompt injection detection sends the prompt text and takes about 100 ms.
- **Failure mode.** A direct `guard()` call fails open; framework wrappers fail closed unless you opt in. A `DRY_RUN` mode records without blocking.

## Where it connects to the talks

The [Harness keynote](the-harness-is-the-new-operating-system.md) argued that instructions cannot enforce a boundary and that the gate belongs in the harness, at the action. Arcjet sells that gate as a product, applied through the same Claude Code hooks the keynote recommended. [Roblox](generation-got-cheap-trust-didnt.md) built its own version of the audit half: every agent action recorded and traced back to a conversation.

## Docs and getting started

- [Coding agents: enforcing policy through hooks](https://docs.arcjet.com/coding-agents)
- [Agent quickstart](https://docs.arcjet.com/agent-get-started)
- [Guards with the Claude Agent SDK](https://docs.arcjet.com/guards/claude-agent-sdk)
- [Prompt injection detection quickstart](https://docs.arcjet.com/prompt-injection/quick-start)
- [Build versus buy: what runs locally, what calls the cloud, and pricing](https://arcjet.com/compare/arcjet-build-vs-buy)
