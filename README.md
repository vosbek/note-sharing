# QCon San Francisco 2026: talk notes

My notes from QCon San Francisco 2026, November 16 to 19: 21 sessions and 17 expo booths. Each page has the slides, the speaker's main points, the figures checked against their sources, and links to the tools, papers and repos that came up.

## Start here

- [Themes across the conference](themes.md): the topics that ran through the talks, how ten companies handle agent-written code, and where each kind of check sits.
- [Tools and technologies](tools.md): the tools, settings and practices named on stage or at a booth, grouped by what they do, with side-by-side comparisons.

## Talks

### Monday, November 16

| Time | Talk | Speakers |
|---|---|---|
| 09:00 | [The Harness Is the New Operating System](talks/the-harness-is-the-new-operating-system.md) | Manju Rajashekhar |
| 10:35 | [Running Software Factory Efficiently at Uber Scale: Holding Agent Spend Steady While Requests Grew 9X](talks/running-software-factory-efficiently-at-uber-scale.md) | Uday Kiran Medisetty |
| 11:45 | [Beyond the Model: Engineering the Agent Harness for Autonomous Software Delivery](talks/beyond-the-model-engineering-the-agent-harness.md) | Jayant Kulkarni |
| 13:35 | [Stop Fighting the Remodel: API Design for Models That Outgrew Their Boundaries](talks/stop-fighting-the-remodel.md) | Aarti Gupta |
| 15:55 | [Generation Got Cheap, Trust Didn't: Scaling Agentic Changes from Prompt to Prod at Roblox](talks/generation-got-cheap-trust-didnt.md) | Kushan Mehta, Jay Moorthi |
| 17:05 | [Into the Labyrinth: What Distributed Systems Have Taught Us About Guardrails](talks/into-the-labyrinth.md) | Akshay Shah |
|   | [Wait, You're Still Doing PRs?](talks/wait-you-re-still-doing-prs.md) | Lee Faus |

### Tuesday, November 17

| Time | Talk | Speakers |
|---|---|---|
| 09:00 | [Learning Out Loud (Under Near-Existential Pressure)](talks/learning-out-loud-under-near-existential-pressure.md) | Laura Savino |
| 10:35 | [Skills, Memory, or Fine-Tuning? The Engineering Loop Behind Production Agents](talks/skills-memory-or-fine-tuning.md) | Abhinav Sinha |
| 11:45 | [Use AI to Multiply Your Team as a Staff Engineer](talks/use-ai-to-multiply-your-team-as-a-staff-engineer.md) | Jordan Cutler |
| 13:35 | [Drawing the Rest of the Owl: A Blueprint for Your Software Factory](talks/drawing-the-rest-of-the-owl.md) | Chris Kelly |
| 14:45 | [Lessons from Building a $100M Product in Six Weeks at OpenAI](talks/building-a-100m-product-at-openai.md) | Brian Yang |
| 15:55 | [Bridging Retrieval and Ranking: From LLM Embeddings and Graph Features to a GPU-Served DLRM](talks/bridging-retrieval-and-ranking.md) | Sudarshan Srinivasa Ramanujam |

### Wednesday, November 18

| Time | Talk | Speakers |
|---|---|---|
| 09:00 | [The Execution Muscle: Why Great Teams Are Built, Not Hired](talks/the-execution-muscle-why-great-teams-are-built-not-hired.md) | Charlotte Mestwerdt |
| 10:35 | [How Netflix Retrofitted Its SDLC for AI Coding Agents](talks/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents.md) | Mark Khuzam |
| 11:45 | [Legacy as Leverage: How Brownfield Work Builds Technical Judgment](talks/legacy-as-leverage-how-brownfield-work-builds-technical-judgment.md) | Shine Garg |
| 13:35 | [Observability: The Missing Control Plane for Agentic Engineering](talks/observability-the-missing-control-plane-for-agentic-engineering.md) | Rachael Wonnacott |
| 14:45 | [You Can't Read the Code Anymore - Verifying Software in the Age of AI](talks/you-cant-read-the-code-anymore.md) | Omer van Kloeten |
| 15:55 | [How To Kill the Code Review](talks/how-to-kill-the-code-review.md) | Ankit Jain |
| 17:15 | [Game Time: How to (Unsuccessfully) 10x in a Week & (Successfully) 10x in a Year](talks/game-time-10x-in-a-week-and-in-a-year.md) | Plum Ertz |

### Thursday, November 19

| Time | Talk | Speakers |
|---|---|---|
| 13:00 | [AI-Assisted Coding Master Class: Build Your Mission Control](talks/ai-assisted-coding-master-class-build-your-mission-control.md) | Sepehr Khosravi, Dev Bali |

## Booths

Vendor booths from the expo floor. Figures and claims on these pages are the vendors' own unless a page says otherwise.

| Day | Company | What they showed |
|---|---|---|
| Mon | [Antithesis](talks/booth-antithesis.md) | Deterministic simulation testing as a gate for agent pull requests |
| Mon | [Arcjet](talks/booth-arcjet.md) | Runtime security policy for AI agents and coding agents |
| Mon | [Atomic](talks/booth-atomic.md) | Version control that records what AI changed and why |
| Mon | [Azul](talks/booth-azul.md) | An AI-readable page about Azul and its Java products |
| Mon | [GitKraken](talks/booth-gitkraken.md) | Insights compares AI coding tools by adoption, cost and cycle time |
| Mon | [Lucidic AI](talks/booth-lucidic-ai.md) | Tuning the harness around production agents |
| Mon | [Materialize](talks/booth-materialize.md) | A live context layer kept current from operational data |
| Mon | [Nutrient](talks/booth-nutrient.md) | An API that turns PDFs, scans and Office files into structured data |
| Mon | [Sonar](talks/booth-sonar.md) | Vortex guides coding agents and checks their changes with SonarQube |
| Mon | [Tacnode](talks/booth-tacnode.md) | A Context Lake for real-time automated decisions |
| Mon | [Unblocked](talks/booth-unblocked.md) | A context layer for coding agents |
| Wed | [groundcover](talks/booth-groundcover.md) | eBPF observability in your own cloud, readable by coding agents over MCP |
| Wed | [Nu](talks/booth-nu.md) | The bank behind Monday's Pix infrastructure talk, and its claims on AI adoption |
| Wed | [OutSystems](talks/booth-outsystems.md) | A low-code platform that outside coding agents drive through MCP |
| Wed | [Testkube](talks/booth-testkube.md) | Existing test suites run inside your own Kubernetes clusters, reachable from agents |
| Wed | [TuxCare](talks/booth-tuxcare.md) | Rebuilt, patched open-source packages, including for end-of-life Spring and Angular |
| Wed | [YugabyteDB](talks/booth-yugabytedb.md) | Distributed Postgres, with a database per agent and zero-copy branches |

## About these notes

The slides belong to their speakers and appear here as photos taken in the sessions. The official decks and recordings are on [qconsf.com](https://qconsf.com). Figures quoted from the talks were checked against their sources where possible, and each page's "Numbers we checked" table says which could not be confirmed. "My take" sections are my own opinion.
