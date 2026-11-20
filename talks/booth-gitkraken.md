---
title: "GitKraken: Insights compares AI coding tools by adoption, cost and cycle time"
kind: "booth"
company: "GitKraken"
day: "2026-11-16"
summary: "GitKraken Insights is a performance platform that tracks AI coding agents' output, cost and changes reaching production."
---

# GitKraken: Insights compares AI coding tools by adoption, cost and cycle time

Booth visit: GitKraken · QCon SF 2026 · Mon Nov 16

> GitKraken Insights is a performance platform that tracks AI coding agents' output, cost and changes reaching production.

## Key points

- The trial page lists a leaderboard that ranks AI agents on output shipped, cost, and changes that reached production.
- Its tool comparison covers adoption, cost and cycle time across Claude Code, Copilot, Codex and Windsurf.
- An AI ROI view converts hours returned and capacity created into dollar figures, and an adoption view shows which developers get the most from AI tools.
- The linked page is a three-day trial on sample data for a made-up company, behind a work-email form; no pricing is shown.

Booth, Monday Nov 16. Sources: GitKraken Insights help docs, its 2026 survey report and the trial page, read Nov 17, 2026. Figures and claims are the vendor's own; I haven't tested them.

## What it is

GitKraken Insights is a software engineering intelligence product. It combines delivery (DORA) metrics, pull request flow, code quality and AI impact, and adds a leaderboard comparing AI coding agents on output, cost and changes that reach production. It came from GitKraken's combination with GitClear.

## How it works

- **Metrics.** The help docs list 21 metrics in five families, including DORA (deploy frequency, lead time, change failure rate, time to restore) and an AI impact and cost family: productivity uplift, AI-assisted percentage, CapEx and OpEx split, spend by tier.
- **Agent leaderboard.** Compares tools such as Claude Code, Copilot, Codex and Windsurf on adoption, cost and cycle time.
- **AI ROI view.** Converts hours returned into dollar figures.
- **Team, not individual.** GitKraken says it measures teams and workflows rather than individual developers.

## Where it connects to the talks

[Uber](running-software-factory-efficiently-at-uber-scale.md) and [Roblox](generation-got-cheap-trust-didnt.md) both built this measurement themselves from telemetry: cost by team, cost per merged PR, and which agent wrote what. GitKraken sells a packaged version, but it relies on vendor usage data, which Roblox said undercounts agent edits and counts generated code rather than merged code.

## Docs and getting started

- [AI impact metrics](https://help.gitkraken.com/gk-insights/gk-insights-ai-impact-metrics/)
- [AI adoption view](https://help.gitkraken.com/gk-insights/ai-adoption/)
- [State of AI in Engineering report](https://gitkraken.com/reports/state-of-ai)
- [Proving AI impact with DORA and velocity metrics](https://www.gitkraken.com/blog/proving-ai-impact-dora-and-velocity-metrics-guide-2026)
