---
title: "Lucidic AI: tuning the harness around production agents"
---

# Lucidic AI: tuning the harness around production agents

Booth visit: Lucidic AI · QCon SF 2026 · Mon Nov 16

> Lucidic AI sells agent optimization: it tunes an agent's prompts, tools, context, memory and policies, or trains the model and harness together.

## Key points

- Their site says it can tune the harness with model weights frozen, or train the model and harness together.
- Their site says it builds a simulated copy of a company's tools, data and customers, then replays failed agent runs from the step that went wrong.
- Their site reports benchmark wins, including a ServiceNow case study; these are the vendor's own figures, without the models or conditions behind most of them.

Booth, Monday Nov 16. Sources: Lucidic AI's site, docs and published benchmarks, read Nov 17, 2026. Figures and claims are the vendor's own until we test them.

## What it is

Lucidic AI tunes production agents. It changes the harness around a model (prompts, memory, tools, steps) with the weights frozen, or trains the model and harness together, using a simulated copy of the agent's world built from the customer's own data.

## How it works

- **Harness optimization.** You pick which parts may change; simulations search for the best configuration, which your agent then loads by a training ID.
- **Co-training.** Model weights and harness are trained together, with methods such as LoRA fine-tuning, distillation and GRPO.
- **Simulation and replay.** A replica of tools, data and simulated customers; when a run fails, it replays from the step that went wrong and keeps better paths.
- **Data curation.** Traces are clustered to keep failures, unusual cases and one example of each common pattern.

## Where it connects to the talks

The [Harness keynote](the-harness-is-the-new-operating-system.md) showed the same harness on different models, and different harnesses on the same model, moving scores by many points. Lucidic automates searching that space for a specific agent.

## Docs and getting started

- [Docs](https://docs.lucidic.ai)
- [Research](https://lucidic.ai/research/)
- [Trust center](https://trust.lucidic.ai/)
