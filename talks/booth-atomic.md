---
title: "Atomic: version control that records what AI changed and why"
kind: "booth"
company: "Atomic"
day: "2026-11-16"
summary: "Atomic is a version control system, from Atomic Software, that records who made each change, why, which AI model helped and how it was reviewed."
---

# Atomic: version control that records what AI changed and why

Booth visit: Atomic · QCon SF 2026 · Mon Nov 16

> Atomic is a version control system, from Atomic Software, that records who made each change, why, which AI model helped and how it was reviewed.

## Key points

- Its docs describe a semantic change graph that tracks memories, intents, provenance, attestations and patches, working like Pijul for changes, reverts and merges.
- Its docs say it records which AI provider and model made a change, as a cryptographic attestation.
- Atomic ships as a CLI with a Git import and a Git shim. Its docs mention team collaboration and self-hosting; pricing is not shown.

Booth, Monday Nov 16. Sources: Atomic's docs and GitHub, plus the Atomic talk the same day, read Nov 17, 2026. Figures and claims are the vendor's own; I haven't tested them.

## What it is

Atomic is a version control system built on patch theory, from Atomic Software. Alongside the code it records why each change was made, which agent and model produced it, what it cost, and how it was reviewed. Lee Faus covered it in depth in [Wait, You're Still Doing PRs?](wait-you-re-still-doing-prs.md); this page is the short product view.

## How it works

- **Change graph.** Changes are nodes in a causal graph, as in Pijul, so a change can be inserted where it belongs without a rebase.
- **Intents and provenance.** Each change links to an intent with acceptance criteria, and to the agent session, model, tokens and cost.
- **Attestations.** Reviews and checks are hashed and signed, so later edits are detectable.
- **Git bridge.** A CLI with Git import and a Git shim, so it can sit alongside existing repositories.

## Docs and getting started

- [Quick start](https://docs.atomic.dev/getting-started/quick-start)
- [Atomic on GitHub](https://github.com/atomicdotdev/atomic)
- [Claude Code integration](https://github.com/atomicdotdev/atomic-claude)
