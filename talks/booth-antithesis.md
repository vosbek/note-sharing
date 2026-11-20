---
title: "Antithesis: deterministic simulation testing as a gate for agent pull requests"
---

# Antithesis: deterministic simulation testing as a gate for agent pull requests

Booth visit: Antithesis · QCon SF 2026 · Mon Nov 16

> Antithesis runs a whole system inside a deterministic hypervisor, injects faults and replays any failure exactly, and pitches it as a check on agent-written pull requests.

## Key points

- Their product page says every run is reproducible to the instruction, with clock, scheduling, network and storage faults injected and a time-travel debugger for failures.
- The page aims at teams whose pull requests are written by agents, offers agent skills for onboarding and triage, and says it can sit in an agent's feedback loop.
- Systems under test ship as containers on Docker Compose or Kubernetes on x86, with SDKs including Java, Python and JavaScript. Antithesis can run in the customer's own AWS VPC and is sold through AWS Marketplace.
- No prices are shown and there is no free or open-source version; the testimonial figures on the page are the vendor's own.

Booth, Monday Nov 16. Sources: Antithesis's product page and docs, read Nov 17, 2026. Figures and claims are the vendor's own until we test them.

## What it is

Antithesis is an autonomous testing platform for distributed systems. It runs your whole system, dependencies included, inside a deterministic hypervisor, explores unusual inputs and injected faults, and replays any failure exactly. It is the commercial home of deterministic simulation testing, the technique Akshay Shah walked through in his talk.

## How it works

- **Deterministic hypervisor.** The system runs on one CPU core with instruction-level determinism, so every run is reproducible; many runs execute in parallel.
- **Exploration and faults.** A feedback-guided search generates odd inputs and injects clock, scheduling, network and storage faults with no extra configuration.
- **Properties.** You state what must always or sometimes hold. SDKs exist for C, C++, Go, Java, JavaScript, .NET, Python and Rust.
- **Debugging.** Deterministic replay, unified distributed traces and a debugger that can rewind a run.
- **Agents.** Agent skills and a plugin help write manifests, state properties and triage bugs, and the product page pitches it as a verification gate in an agent coding loop.

## Where it connects to the talks

This is the vendor behind [Into the Labyrinth](into-the-labyrinth.md). Akshay's argument: people write the properties, agents search for violations, and every finding arrives with a replayable workload, which filters out false positives. Antithesis also has a session still ahead, *Trust, but Verify: Delivering Quality with Agentic Workflows*, on Tuesday at 2:45.

## Docs and getting started

- [Antithesis docs](https://antithesis.com/docs)
- [Hands-on tutorial](https://github.com/antithesishq/hands-on-tutorial-1)
- [Agent skills for onboarding and triage](https://github.com/antithesishq/antithesis-skills)
- [Product overview](https://antithesis.com/product/)
