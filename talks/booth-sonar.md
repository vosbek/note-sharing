---
title: "Sonar: Vortex guides coding agents and checks their changes with SonarQube"
---

# Sonar: Vortex guides coding agents and checks their changes with SonarQube

Booth visit: Sonar · QCon SF 2026 · Mon Nov 16

> Sonar Vortex gives coding agents a project's rules and context before they write, then checks each change against SonarQube analysis as they work.

## Key points

- Their page splits it in two: Guide supplies repository context, architecture rules, security standards, conventions and approved libraries to the agent.
- Verify checks agent-written changes as they happen for security, reliability, code smells, coverage and duplication, and the page says it does not replace CI.
- It runs through a SonarQube instance, set up by an agent plugin for Claude Code, Copilot, Codex CLI, Cursor and Antigravity, by the SonarQube CLI, or by its MCP server.
- The headline figures on the page all read zero and look like placeholders; pricing is through sales.

Booth, Monday Nov 16. Sources: Sonar's Vortex page and SonarQube docs, read Nov 17, 2026. Figures and claims are the vendor's own until we test them.

## What it is

Sonar Vortex gives coding agents a project's rules and context before they write code, then checks each change against SonarQube analysis while the agent works. It runs on the SonarQube engine many teams already use in CI.

## How it works

- **Guide.** Supplies repository context, architecture rules, security standards, conventions and approved libraries to the agent before it starts.
- **Verify.** Checks changes as they are made for security, reliability, maintainability, coverage and duplication, with cross-file analysis. Sonar says it complements CI rather than replacing it.
- **Integration.** A SonarQube agent plugin for Claude Code, Codex CLI, Copilot, Cursor and Antigravity; the SonarQube CLI (`sonar integrate`); or the SonarQube MCP Server.

## Where it connects to the talks

Sonar's own session, *Building a Safe Software Factory*, ran Monday at 1:35. The idea matches [Roblox](generation-got-cheap-trust-didnt.md): give the agent your rules before it writes, and check before review, so humans see fewer problems.

## Docs and getting started

- [Agent-centric development cycle](https://docs.sonarsource.com/agent-centric-development-cycle)
- [SonarQube MCP Server](https://www.sonarsource.com/products/sonarqube/mcp-server/)
- [SonarQube CLI](https://www.sonarsource.com/sonarqube/cli/)
- [SonarQube Server docs](https://docs.sonarsource.com/sonarqube-server/latest/)
