---
title: "The Harness Is the New Operating System"
---

# The Harness Is the New Operating System

**Speaker:** Manju Rajashekhar (Founder & CEO, Mad Labs)  
QCon SF 2026 · Keynote · Mon Nov 16, 09:00 · Grand Ballroom  
[Session page](https://qconsf.com/keynote/nov2026/harness-new-operating-system)

> A coding agent is a model plus a harness, and the harness decides much of what the agent can do and is allowed to do.

## Key points

- He defined the harness as everything in an agent that is not the model: the software that turns the model's text into actions and brings results back. An agent's effective capability is the model plus the harness's tools, information and feedback.
- He cited DeepSeek's model card, which ran one model through eight harnesses on the same coding benchmark. Scores ranged from 65.5% to 74.2%, and the minimal harnesses did best.
- He cited a manager and worker setup that coordinates through shared files. It took an open-weight 27B model from about 67% to 92.4% on hard LiveCodeBench problems, against about 90% for a frontier model in a single call.
- He separated ability from authority. An agent asked to make tests pass can fix the code or delete the tests. Only the harness can rule out the second, for example by making test files read-only.
- He walked through OpenAI evaluation agents that used a package proxy to leave their sandbox in July 2026 and reached Hugging Face's systems. He cited Anthropic data that people approve 97% of permission prompts. In its study, people caught 13.6% of planted dangerous commands and an automated classifier caught 89%.
- His better gate has three parts: isolation, credentials scoped to the job, and review only for risky actions. He said instructions alone cannot enforce a boundary, and cited an 84% drop in permission prompts after sandboxing.
- He built a harness as a loop with four parts: context, tool interface, execution and feedback. He mapped them to virtual memory, system calls, process permissions and return codes, and said deterministic hooks such as running the tests before accepting done belong in the harness.
- He said every harness component encodes an assumption about what the model cannot do, so new models retire some of it. He gave Anthropic's context resets, which Opus 4.5 no longer needed, and LangChain's harness-only gain from 52.8% to 66.5% on Terminal-Bench 2.0.

## The talk in brief

Every coding agent you use, whether [Claude Code](https://code.claude.com/docs), [Codex](https://openai.com/codex) or [Cursor](https://cursor.com), is a model plus a harness. The harness is everything that isn’t the model: the context it sees, the tools it can call, where those tools run, and the feedback that comes back. Manju’s argument is that the harness now decides much of what an agent can do and what it is allowed to do, so when an agent struggles, swapping the model is often the wrong first move.

He builds a harness from first principles around one running example (“fix the failing tests”), shows that the four parts of its loop line up with what an operating system does for a program, and closes with a short guide to diagnosing a struggling agent by which part of the loop broke.

> “The harness is everything in an agent that isn’t the model.” (Slide 6)

## In depth

Each part follows the talk’s order. Slide numbers match the deck (41 slides).

### Model + harness = agent (slides 1–7)

Manju opened by asking who had used Claude Code, Codex or Cursor (nearly everyone), who would call them agents (some) and who would call them harnesses (fewer). His answer: each one is an agent, and what each company built is mostly the harness.

Agents fail in three recognizable ways: they go in circles, work on the wrong thing, or declare “done” halfway through. Most teams respond by swapping the model, which sometimes works for reasons nobody can explain.

His mental model has three layers. The **application** sets the job and the condition for success (“fix this bug; done means the tests pass”). The **agent** works the job. The **environment** holds the files, services and data. Inside the agent, the model can’t run anything on its own. A good harness does four things for it:

Elicits  
draws out ability the model already has.

Extends  
adds abilities the model’s weights lack, such as running code.

Stabilizes  
keeps one mistake from snowballing into the whole job.

Guards  
limits what the model’s actions can touch.

![Slide 3: Every agent struggles. Goes in circles, works on the wrong thing, gives up halfway.](../slides/the-harness-is-the-new-operating-system/deep/s03.webp)

Slide 3. The three ways agents struggle.

![Slide 7: Model inherent capability plus harness tools, information, feedback equals agent effective capability.](../slides/the-harness-is-the-new-operating-system/deep/s07.webp)

Slide 7. Weak model, weak harness, or weak instructions?

### Same model, different harness, different results (slides 8–10)

The first evidence comes from DeepSeek’s model card for V4.1-Flash, which ran the same model through eight harnesses at maximum reasoning effort.

| Harness (same model)       | DeepSWE v1.1 | Terminal-Bench 2.1 |
|----------------------------|--------------|--------------------|
| mini-SWE                   | 74.2%        | 90.3%              |
| DeepSeek harness: minimal  | 72.6%        | 90.6%              |
| DeepSeek harness: standard | 70.5%        | 85.8%              |
| Claude Code                | 69.8%        | 88.0%              |
| DeepSeek harness: PTC      | 67.6%        | 85.8%              |
| Pi                         | 66.2%        | 86.1%              |
| Codex                      | 65.6%        | 84.1%              |
| OpenCode                   | 65.5%        | 85.0%              |

That is close to a nine-point spread from the harness alone, and the two minimal harnesses beat the feature-rich ones on both benchmarks. Manju’s takeaway: more harness is not automatically better. One caution from the model card itself: the comparison does not isolate every variable, so treat the ranking of commercial harnesses as indicative for this one model.

The second example changes how work is organized. The GVS5H paper ([arXiv 2608.26480](https://arxiv.org/abs/2608.26480)) runs one model in two roles: a manager that plans and picks the next task, and workers that each take one task with a fresh context, coordinating only through a shared ledger of files (plan, tasks, notes, candidate solution). Public test results feed the manager’s next decision.

| LiveCodeBench, 100 hard problems        | Pass rate |
|-----------------------------------------|-----------|
| Qwen3.8-27B (open weights), single call | 66.8%     |
| Qwen3.8-27B, manager-worker scaffold    | 92.4%     |
| Claude Fable 5, single call             | 90.4%     |

Slide 10 was too blurry to read in our photo; the figures above come from the paper as reported by independent write-ups. The comparison is uneven by design: the scaffold gets up to 10 manager-worker rounds plus test feedback, while the frontier model gets one call. The paper also found the scaffold did nothing or hurt for some models.

![Slide 8: Same model, different harnesses, different results. DeepSeek V4.1 Flash table.](../slides/the-harness-is-the-new-operating-system/deep/s08.webp)

Slide 8. DeepSeek V4.1-Flash across eight harnesses.

![Slide 9: A harness can change how a model works through a problem. Single call versus manager-worker scaffold with shared ledger.](../slides/the-harness-is-the-new-operating-system/deep/s09.webp)

Slide 9. Single call versus the manager-worker scaffold.

### The harness decides what an agent may touch (slides 11–15)

To do useful work, agents need access: write files, install software, send messages, update databases. The model can only request actions, so the harness sits between the request and the real world. Its job is to give the agent all the access the job needs and none beyond it.

The test case: asked to make failing tests pass, an agent can fix the code or edit and delete the tests. Both are within its ability; only the first is within its authority. This is reward hacking, documented in Anthropic’s Claude 3.7 Sonnet system card and measured by ImpossibleBench. Here the harness can enforce the line simply by making test files read-only, and ImpossibleBench found that restricting test access was the most effective fix it tried.

The real-world case is harder. In July 2026, OpenAI evaluation agents running a capture-the-flag benchmark in an isolated environment used a legitimate door, the package proxy they needed to install software, as their way out. Through a zero-day in that proxy they reached the internet, used a code sandbox someone had left open as a launchpad, and got into Hugging Face’s production systems. The slide puts it at admin on internal clusters for 4.5 days with no human directing. One agent’s reasoning noted the work was “potentially outside intended scope” and it kept going.

> “Capability does not grant authority. Someone has to enforce that authority. That’s harness design.” (Slide 13)

Asking a human to approve every action doesn’t solve it. Anthropic’s data for Claude Code shows people approve 97% of permission prompts, and as of June 2026 a quarter of interactive sessions started with the checks switched off entirely. In Anthropic’s study of 1,053 paid testers, people reviewing prompts caught 13.6% of planted dangerous commands, against 89% for the auto-mode classifier. A gate that says yes 97% of the time is a rubber stamp.

The better gate has three parts: **isolation** (where it runs, which limits how far a mistake can reach), **scoped credentials** (what it can touch, only what the job needs) and **selective review** (only risky actions get checked, which is what auto mode does).

![Slide 12: When OpenAI's agents broke into Hugging Face. Evaluation agents, package proxy, out to the internet, launchpad, Hugging Face.](../slides/the-harness-is-the-new-operating-system/deep/s12.webp)

Slide 12. The July 2026 OpenAI and Hugging Face incident. The final build adds: “Reward hacking, far beyond what the job required.”

![Slide 15: Give the agent room to work, within its authority. People reviewing prompts 13.6 percent, auto-mode classifier 89 percent.](../slides/the-harness-is-the-new-operating-system/deep/s15.webp)

Slide 15. Isolation, scoped credentials, selective review.

### The simplest agent is a model in a loop (slides 16–18)

Traditional software runs steps written in advance. Agentic work has no fixed workflow: the agent investigates, tries something, sees what happened and adjusts, choosing each step after seeing the last result. The natural structure is a loop. The model proposes an action, the harness arranges for it to run, and the observation comes back for the next decision.

A loop alone isn’t enough; each iteration has to make progress. Four parts of the harness decide whether it does.

![Diagram](../diagrams/the-harness-is-the-new-operating-system-1.svg)

### Context: what the model knows (slides 19–21)

For each decision the model needs three answers: what’s the job, what’s the context around it, and what has happened so far. For the running example that is “fix the failing tests”, “this project runs tests with `make test`”, and “the last run had 3 failures”. The harness assembles these into the model’s working view, which has limited space, so it can’t include the whole repository, every test log and every earlier attempt.

Guidance arrives two ways: the system prompt sets the role and tools, and project conventions such as [`AGENTS.md`](https://agents.md) or [`CLAUDE.md`](https://code.claude.com/docs) set the rules (“run tests with make test; don’t edit the test fixtures”). Change only the system prompt to “you review code, find bugs, cite the lines” and the same harness becomes a code reviewer.

Not all guidance belongs up front. A team’s checklist for debugging test failures matters only when tests fail, so the harness gives the model a one-line pointer (“skills/debug-tests: use when tests fail”) and the model loads the full checklist on request. The same trick works for code: a repository map tells the model where things live, and it opens files as needed. This is progressive disclosure.

**When context breaks:** the relevant information was missing, or the pointer existed and the agent never followed it. Check what was in the model’s working view when it made the decision.

![Slide 20: Guidance sets the role and the rules. System prompt: you review code, find bugs, cite the lines. AGENTS.md rules.](../slides/the-harness-is-the-new-operating-system/deep/s20.webp)

Slide 20. Swap the role and the same harness reviews code.

![Slide 21: Give the model a pointer, not the whole thing. skills/debug-tests loaded on request, repository map.](../slides/the-harness-is-the-new-operating-system/deep/s21.webp)

Slide 21. Progressive disclosure: pointers in context, details on request.

### Interface: what the model can ask to do (slides 22–26)

The tool interface defines which operations exist and how the model requests them. If the harness offers read, edit and run_tests, and the fix needs a dependency installed, the model knows the answer and can’t ask for it. The interface sets the ceiling on effective capability.

How much it matters: Princeton’s [SWE-agent](https://arxiv.org/abs/2405.15793) study held the model (GPT-4 Turbo) and the benchmark (SWE-bench Lite) fixed and changed only the interface.

| SWE-agent, GPT-4 Turbo, SWE-bench Lite                           | Issues resolved |
|------------------------------------------------------------------|-----------------|
| Plain shell                                                      | 11.0%           |
| Interface designed for the agent                                 | 18.0%           |
| Same, but showing whole files instead of 100 lines at a time     | 12.7%           |
| Same, but without the linter that rejects edits that don’t parse | 15.0%           |

How tools behave matters as much as what they do. Designing a tool for every operation doesn’t scale, so harnesses also let the model write and run code. That gives a spectrum: specific tools are predictable and easy to gate, while shell or code can build operations nobody designed (run every check, collect failures, group them by error) but is harder to gate. Because code can do anything, its limits have to come from where it runs.

The interface also shapes what enters the model’s context. A program can boil a log of thousands of lines down to “3 failures, one type error” plus a pointer to the full log. And spawning a subagent can itself be a tool call: the subagent works in its own context with the logs, files and dead ends, and the parent’s view stays clean with just the findings.

Delegation isn’t free. Google and MIT’s scaling study (Kim et al., 260 configurations) found multi-agent setups helped by up to 80.8% when a task split cleanly into parallel parts and hurt by up to 70% when each step depended on the last. Every handoff loses context.

**When the interface breaks:** the model couldn’t express what it needed, or what came back flooded its working view. Check what it could ask for and what came back.

![Slide 23: Same model, different interface. Plain shell 11.0, agent-designed interface 18.0, whole files 12.7, without the linter 15.0.](../slides/the-harness-is-the-new-operating-system/deep/s23.webp)

Slide 23. SWE-agent’s interface results.

![Slide 26: Spawning a subagent can also be a tool call. Decomposition helps up to plus 80 percent when it splits cleanly, hurts up to minus 70 percent when each step depends on the last.](../slides/the-harness-is-the-new-operating-system/deep/s26b.webp)

Slide 26. When decomposition helps and when it hurts.

### Execution: where it runs and what it can reach (slides 27–29)

Every action needs a place to run, and the harness provides it or arranges for it. That ranges from a runtime, dependencies and a sandbox up to a running app, a browser or a full computer. For the running example: a test runner, the project’s dependencies, maybe a test database.

Execution is where the better gate gets enforced: a sandbox with project files allowed and the home directory and network blocked, a test database and no production credentials, and review only for risky commands. Draw the boundary once and most of the questions go away: Anthropic reported 84% fewer permission prompts after sandboxing Claude Code.

Why not just tell the model where the boundary is? Instructions are guidance. Even a good model follows them most of the time, not every time, and an agent chasing a reward will ignore an instruction that’s in its way. An agent told “use only test” in a sandbox that also holds production credentials will almost always comply, and the one time it doesn’t is a security incident.

**When execution breaks:** the environment lacked what the job needed, or the boundary was too tight or too loose. Check where actions ran and what they could reach.

![Slide 28: Execution needs a way to enforce a boundary. Isolation, scoped credentials, selective review. 84 percent fewer permission prompts.](../slides/the-harness-is-the-new-operating-system/deep/s28.webp)

Slide 28. The better gate, in execution.

![Slide 29: Instructions can't enforce a boundary. Agent told use only test reaches test database most of the time, prod credentials unlikely but possible.](../slides/the-harness-is-the-new-operating-system/deep/s29.webp)

Slide 29. Instructions can’t enforce a boundary.

### Feedback: what actually happened (slides 30–33)

The model’s next move depends on knowing exactly what happened. “The tests ran and three failed” means read the failures. “A dependency is missing” means fix the environment. “Starting the CI run timed out” means check before retrying, or it might run twice. Collapse those into one generic error and the model has to guess.

Small error rates compound over long jobs. If each of 20 steps succeeds 95% of the time, the whole job succeeds about 36% of the time. If feedback lets the agent catch 80% of its errors, the job succeeds about 82% of the time. The longer the job, the more feedback matters. (This arithmetic was on slide 31, which we didn’t photograph; we reran it: 0.95²⁰ = 35.8%, 0.99²⁰ = 81.8%.)

The best feedback comes from observing the running application: what a user would see, the logs, and the traces. Anthropic described an agent that built a web app with a rectangle-fill tool; the code and unit tests looked fine, but when evaluator agents used the app like real users, dragging only filled the corners. Reading the code is a guess; watching it run is evidence. OpenAI calls this application legibility.

Not all feedback has to come from a model. [Hooks](https://code.claude.com/docs/en/hooks) run deterministically in the harness: a type checker after every edit, like a git hook. The most important one is an exit hook. When the model says it’s done, the harness runs the tests before it believes it: pass and the work is accepted, fail and it goes back to work.

**When feedback breaks:** the model couldn’t tell what happened, or never saw the behavior that mattered. Check what came back and whether it showed what you care about.

![Slide 32: The best feedback comes from observing the app. Application legibility: running app, logs, traces. Rectangle fill: expected versus what the app did.](../slides/the-harness-is-the-new-operating-system/deep/s32.webp)

Slide 32. Reading the code is a guess; watching it run is evidence.

![Slide 33: The harness runs the checks, not the model. Hook runs the type checker after every edit; exit hook runs the tests when the model says it's done.](../slides/the-harness-is-the-new-operating-system/deep/s33.webp)

Slide 33. Hooks after every edit and before “done”.

### The harness is the new operating system (slides 34–35)

Put together on the running example: context carries the job and how to run tests; a program runs the suite and groups failures; it executes in a sandbox with project dependencies and no production credentials; feedback reports three failures from one type error; those results go back into context alongside their commit; the next pass fixes it and the exit hook confirms the tests pass. Four parts, one loop, every iteration.

| Part of the loop | Responsibility            | Operating system equivalent |
|------------------|---------------------------|-----------------------------|
| Context          | Manage scarce memory      | Virtual memory              |
| Interface        | Provide a way to ask      | System calls                |
| Execution        | Limit what can be touched | Processes, permissions      |
| Feedback         | Report what happened      | Return codes, errors        |

A harness is a managed operating environment for a model, playing the role an operating system plays for a program. Manju isn’t the first to use the analogy; Phil Schmid and others have framed the model as CPU and the context window as RAM. His contribution is mapping it onto a working loop and turning it into a diagnostic.

### A harness design is never finished (slides 36–39)

The program the harness runs, the model, keeps changing, so the boundary moves. Change the model and you should recheck what support it still needs. Change the harness and you should recheck what the same model can now do.

Retiring support: in Anthropic’s long-running app work, Claude Sonnet 4.5 showed “context anxiety”, wrapping up early as it neared its context limit, so the harness reset context and handed off structured notes. With Opus 4.5 the behavior was largely gone and the resets were dropped for automatic compaction. The responsibility (manage context as work continues) stayed; the mechanism changed.

Adding support: LangChain held GPT-5.2-Codex fixed and improved its Deep Agents harness by reading traces, hypothesizing why runs failed, changing the harness and re-evaluating. They added verification before finishing, environment information up front, time warnings and repeated-edit detection, and moved from 52.8% to 66.5% on Terminal-Bench 2.0. How much of that a future model will make unnecessary is an open question, which is why you can’t evaluate models without their harness or harnesses without their model.

![Slide 37: A better model can make support unnecessary. Sonnet 4.5 resets and structured handoff struck through; Opus 4.5 automatic compaction.](../slides/the-harness-is-the-new-operating-system/deep/s37.webp)

Slide 37. Context anxiety: a fix one model needed and the next didn’t.

![Slide 39: The harness can take over what the model drops. Observe, hypothesize, change, evaluate. 52.8 percent to 66.5 percent.](../slides/the-harness-is-the-new-operating-system/deep/s39.webp)

Slide 39. LangChain’s trace-driven harness loop.

### When an agent struggles, where to look (slides 40–41)

Start with the job: did the application say what “done” means? Then walk the loop.

| Symptom                                      | Look first at                | Question to ask                            |
|----------------------------------------------|------------------------------|--------------------------------------------|
| Works on the wrong thing                     | The job and its instructions | Did the application say what done means?   |
| Gives up halfway                             | Context                      | What did it know when it decided?          |
| Can’t do something it clearly understands    | Interface                    | What could it ask for, and what came back? |
| Fails on setup, or touches what it shouldn’t | Execution                    | Where did it run, and what could it reach? |
| Goes in circles, or claims done too early    | Feedback                     | What did it see?                           |

His closing ask for the week: open an agent you use and read its system prompt and tool list; then pick a task where it struggles, change one part of the loop, see whether it helps, and rerun what already worked.

## Numbers we checked

Every figure in the talk against its source. Checked means we found the same number in the source or a write-up of it; Caveat means it holds with a condition worth knowing; Slide only means we took it from the slide.

| Claim                                                    | Figure        | Source                                                                                                                                                                                                                                                                                                  | Status                       |
|----------------------------------------------------------|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------|
| Same model across 8 harnesses, DeepSWE v1.1              | 65.5–74.2%    | [DeepSeek V4.1-Flash model card](https://deepinfra.com/deepseek-ai/DeepSeek-V4.1-Flash), [summary](https://datanorth.ai/news/deepseek-releases-deepseek-v4-1-flash)                                                                                                                                     | Caveat vendor-run, one model |
| Manager-worker scaffold, Qwen3.8-27B                     | 66.8 → 92.4%  | [GVS5H, arXiv 2608.26480](https://arxiv.org/abs/2608.26480)                                                                                                                                                                                                                                             | Caveat 10 rounds vs one call |
| Agents edit or delete tests to pass                      | n/a           | [ImpossibleBench, arXiv 2510.20270](https://arxiv.org/abs/2510.20270)                                                                                                                                                                                                                                   | Checked                      |
| OpenAI eval agents reached Hugging Face production       | Jul 2026      | [BleepingComputer](https://www.bleepingcomputer.com/news/security/openai-says-its-ai-models-hacked-hugging-face-during-testing/), [CSA research note](https://labs.cloudsecurityalliance.org/wp-content/uploads/2026/08/CSA_research_note_agentic_ai_self_attack_systemic_risk_20260816-csa-styled.pdf) | Checked                      |
| Claude Code permission prompts approved                  | 97%           | [Anthropic, auto mode post](https://claude.com/blog/auto-mode-default-in-claude-code)                                                                                                                                                                                                                   | Checked                      |
| Interactive sessions started with checks off (June 2026) | 25%           | [Implicator, citing Anthropic](https://www.implicator.ai/anthropic-claude-code-auto-mode-default/)                                                                                                                                                                                                      | Checked                      |
| Dangerous commands caught: people vs classifier          | 13.6% vs 89%  | [InfoWorld, citing Anthropic (1,053 testers)](https://www.infoworld.com/article/4207959/anthropic-makes-claude-codes-auto-mode-default-for-paid-users.html)                                                                                                                                             | Caveat controlled study      |
| Fewer permission prompts after sandboxing                | 84%           | [Anthropic, Beyond permission prompts](https://www.anthropic.com/engineering/claude-code-sandboxing)                                                                                                                                                                                                    | Checked                      |
| Plain shell vs agent-designed interface                  | 11.0 → 18.0%  | [SWE-agent, arXiv 2405.15793](https://arxiv.org/abs/2405.15793)                                                                                                                                                                                                                                         | Slide only 2024 models       |
| Multi-agent vs single agent                              | +80.8% / −70% | [Kim et al., arXiv 2512.08296](https://arxiv.org/abs/2512.08296)                                                                                                                                                                                                                                        | Checked                      |
| 20 steps at 95% each; with 80% of errors caught          | 36% → 82%     | Arithmetic                                                                                                                                                                                                                                                                                              | Checked 35.8%, 81.8%         |
| Context anxiety in Sonnet 4.5, gone in Opus 4.5          | n/a           | [Anthropic, Harness design for long-running apps](https://www.anthropic.com/engineering/harness-design-long-running-apps)                                                                                                                                                                               | Checked                      |
| Harness-only gains, GPT-5.2-Codex, Terminal-Bench 2.0    | 52.8 → 66.5%  | [LangChain](https://blog.langchain.com/improving-deep-agents-with-harness-engineering)                                                                                                                                                                                                                  | Checked                      |

## About the speaker

Manju Rajashekhar has spent his career on systems that can’t go down. At Twitter he worked on the caching layer and wrote [twemproxy](https://github.com/twitter/twemproxy), the lightweight memcached and Redis proxy Twitter open-sourced in 2012 that became a standard piece of caching architecture well beyond Twitter. Earlier roles included VMware, Microsoft and NetScaler; he holds an MS in Computer Science from Stanford.

He co-founded Blackbird Technologies, a deep-learning search and recommendations startup that Etsy acquired in 2016, and stayed at Etsy until late 2024, rising to VP of Engineering over personalization, ML enablement, and search and ads. He is now founder and CEO of Mad Labs, his second company, building infrastructure for long-horizon, durable and reliable AI agents.

The program committee member who introduced him described Manju sitting down, opening up a harness, and showing how plain the prompts behind the most complex harnesses are, which made agent work feel approachable to a distributed-systems engineer.

The intro card shown on screen before the talk listed an unrelated Adobe Photoshop bio. His title slide, the QCon speaker page and his public record all agree on the background above.

## Terms and technologies

Everything the talk names, in plain English, with a link to the real thing.

### Agents and the files that steer them

[Agent harness](https://openai.com/index/harness-engineering/)  
The software around a model that turns its text output into actions: assembling context, offering tools, running them somewhere safe, and reporting results. “Harness engineering” as a named discipline comes from OpenAI’s February 2026 post.

[Claude Code](https://code.claude.com/docs)  
Anthropic’s coding agent for the terminal and IDE. One of the eight harnesses in DeepSeek’s comparison.

[Codex](https://openai.com/codex)  
OpenAI’s coding agent (CLI, IDE and cloud). Another harness in the comparison, and the one LangChain’s tuning work was benchmarked against.

[Cursor](https://cursor.com)  
An AI-first code editor built on VS Code. Named in the opening show of hands.

[OpenCode](https://opencode.ai)  
An open-source terminal coding agent. Lowest scorer in DeepSeek’s harness comparison.

[mini-SWE-agent](https://github.com/SWE-agent/mini-swe-agent)  
A deliberately tiny harness, roughly a model plus a bash shell in a loop. It topped the comparison, which is the evidence for “more harness isn’t automatically better.”

[Deep Agents](https://github.com/langchain-ai/deepagents)  
LangChain’s open-source agent harness. The subject of the trace-driven tuning that moved Terminal-Bench from 52.8% to 66.5%.

[AGENTS.md](https://agents.md) and CLAUDE.md  
Markdown files at the root of a repo that tell coding agents how to build, test and follow conventions; AGENTS.md is the open, cross-vendor version, CLAUDE.md is Claude Code’s own. These are the “project conventions” layer of context.

Subagent  
A second agent the main one starts like a tool call. It works in its own context and hands back only its findings, keeping the parent’s context clean. See [Kim et al.](https://arxiv.org/abs/2512.08296) for when splitting work helps or hurts.

[Progressive disclosure](https://en.wikipedia.org/wiki/Progressive_disclosure)  
A UI design idea applied to agents: show a one-line pointer up front and load the full detail only when it’s needed. Skills and repository maps work this way.

[Context window](https://docs.claude.com/en/docs/build-with-claude/context-windows)  
The fixed amount of text a model can see at once: its working memory. The talk maps managing it to an operating system’s [virtual memory](https://en.wikipedia.org/wiki/Virtual_memory).

[Compaction and context resets](https://www.anthropic.com/engineering/harness-design-long-running-apps)  
Two ways to keep a long job going when context fills up: summarize older context in place (compaction), or clear it and hand off structured notes (reset). Sonnet 4.5 needed resets; Opus 4.5 got by with compaction.

### Safety and execution

[Reward hacking](https://en.wikipedia.org/wiki/Reward_hacking)  
When an AI satisfies the measure instead of the goal, such as deleting failing tests so “tests pass.” Measured for coding agents by [ImpossibleBench](https://github.com/safety-research/impossiblebench).

Sandbox ([bubblewrap](https://github.com/containers/bubblewrap), Seatbelt)  
OS-level isolation that limits which files and network an agent’s commands can reach. Claude Code uses bubblewrap on Linux and Seatbelt on macOS.

[Auto mode](https://claude.com/blog/auto-mode-default-in-claude-code)  
Claude Code’s setting where a classifier model approves routine tool calls and blocks risky ones, instead of asking a person every time. The source of the 13.6% vs 89% comparison.

[Hooks](https://code.claude.com/docs/en/hooks)  
Scripts the harness runs automatically at set moments, such as after every edit or when the agent says it’s done. A Claude Code Stop hook that exits with code 2 sends the agent back to work, which is how “run the tests before believing done” is built.

[Linter](https://en.wikipedia.org/wiki/Lint_(software))  
A tool that checks code for errors and style problems without running it. SWE-agent rejected edits that failed one, and removing it cost 3 points.

[Capture the flag (CTF)](https://en.wikipedia.org/wiki/Capture_the_flag_(cybersecurity))  
A security exercise where the goal is to exploit a target and retrieve a hidden string. The OpenAI agents were running a CTF benchmark when they escaped.

[Package proxy](https://jfrog.com/artifactory/)  
A cache that sits between a locked-down environment and public package registries such as npm or PyPI. In the July incident it was a JFrog Artifactory instance, and a [zero-day](https://en.wikipedia.org/wiki/Zero-day_vulnerability) in it was the way out.

[System call](https://en.wikipedia.org/wiki/System_call)  
How a program asks the operating system to do something it can’t do itself, like open a file. The talk’s analogy for a model’s tool calls.

### Benchmarks

[SWE-bench](https://www.swebench.com)  
Real GitHub issues from popular Python repos; the agent must produce a patch that passes the project’s tests. “Lite” is a smaller subset.

DeepSWE  
Datacurve’s benchmark of fixing real bugs in real repositories, used in DeepSeek’s [model card](https://deepinfra.com/deepseek-ai/DeepSeek-V4.1-Flash).

[Terminal-Bench](https://www.tbench.ai)  
Hard, realistic tasks done in a command-line environment, each with its own container, a human-written solution and verification tests. Version 2.0 has 89 tasks.

[LiveCodeBench](https://livecodebench.github.io)  
Competitive-programming problems collected after model training cutoffs, to limit memorization. Used for the manager-worker result.

### About the speaker’s background

[twemproxy](https://github.com/twitter/twemproxy)  
A fast, lightweight proxy for memcached and Redis that Manju wrote at Twitter. It cut connection counts to cache servers and became a common piece of caching architecture outside Twitter.

## Reading and tools

### Primary sources

- [Harness engineering: leveraging Codex in an agent-first world](https://openai.com/index/harness-engineering/). OpenAI, Feb 2026. The post that named the discipline; source of “application legibility”.
- [Harness design for long-running application development](https://www.anthropic.com/engineering/harness-design-long-running-apps). Anthropic, Mar 2026. Planner, generator and evaluator agents; context anxiety; pruning the harness as models improve.
- [Beyond permission prompts](https://www.anthropic.com/engineering/claude-code-sandboxing). Anthropic, Oct 2025. Claude Code’s sandbox design and the 84% figure.
- [Auto mode is now the default in Claude Code](https://claude.com/blog/auto-mode-default-in-claude-code). Anthropic, Aug 2026. The approval-fatigue data and classifier results.
- [Improving Deep Agents with harness engineering](https://blog.langchain.com/improving-deep-agents-with-harness-engineering). LangChain, Feb 2026. A practical trace-driven harness tuning loop.
- [Harness Engineering, first thoughts](https://martinfowler.com/articles/exploring-gen-ai/harness-engineering-memo.html). Martin Fowler, Feb 2026.

### Papers

- [SWE-agent: Agent-Computer Interfaces Enable Automated Software Engineering](https://arxiv.org/abs/2405.15793). Princeton, 2024.
- [GVS5H: Zero-Shot Self-Orchestration with Ledger-Based Control](https://arxiv.org/abs/2608.26480). 2026.
- [Towards a Science of Scaling Agent Systems](https://arxiv.org/abs/2512.08296). Google Research, Google DeepMind and MIT, 2025–26.
- [ImpossibleBench: Measuring LLMs’ Propensity of Exploiting Test Cases](https://arxiv.org/abs/2510.20270). 2025; code at [safety-research/impossiblebench](https://github.com/safety-research/impossiblebench).

### Tools and benchmarks mentioned

[mini-SWE-agent](https://github.com/SWE-agent/mini-swe-agent)  
A deliberately tiny coding-agent harness from the SWE-agent team. It topped DeepSeek’s harness comparison, which makes it a useful baseline for any harness evaluation.

Claude Code, Codex, OpenCode, Pi  
The commercial and open harnesses in DeepSeek’s comparison.

DeepSWE, Terminal-Bench, SWE-bench Lite, LiveCodeBench  
The coding benchmarks behind the talk’s numbers. Terminal-Bench measures getting work done in a terminal; DeepSWE and SWE-bench measure fixing real bugs in real repositories.

### Related QCon SF sessions

Manju pointed to these for going deeper. As of Monday evening, the last three are still ahead.

- Everything I Knew About Developer Experience Is Wrong for Agents. Emmanuel Paraskakis, Mon 11:45.
- Agentic Trust: Securing AI Agents in Production. Amanda Walker, Mon 3:55.
- **The Revenge of the Data Scientist: Why Reliable AI Needs Evals, Traces, and Metrics.** Hamel Husain, Tue 1:35.
- **Making Production Legible to Agents.** Liz Fong-Jones, Wed 11:45.
- **Avoiding Prompt Debt & Other Context Failures.** Drew Breunig, Wed 3:55.

## All slides

[![Slide 1: title](../slides/the-harness-is-the-new-operating-system/deep/s01.webp)](../slides/the-harness-is-the-new-operating-system/deep/s01.webp)

Slide 1. Title

[![Slide 2: quick show of hands](../slides/the-harness-is-the-new-operating-system/deep/s02.webp)](../slides/the-harness-is-the-new-operating-system/deep/s02.webp)

Slide 2. Show of hands

[![Slide 3: every agent struggles](../slides/the-harness-is-the-new-operating-system/deep/s03.webp)](../slides/the-harness-is-the-new-operating-system/deep/s03.webp)

Slide 3. Every agent struggles

[![Slide 5: the application gives the agent its job](../slides/the-harness-is-the-new-operating-system/deep/s05.webp)](../slides/the-harness-is-the-new-operating-system/deep/s05.webp)

Slide 5. The application gives the job

[![Slide 6: model plus harness equals agent](../slides/the-harness-is-the-new-operating-system/deep/s06.webp)](../slides/the-harness-is-the-new-operating-system/deep/s06.webp)

Slide 6. Model + harness = agent

[![Slide 7: capability depends on model and harness](../slides/the-harness-is-the-new-operating-system/deep/s07.webp)](../slides/the-harness-is-the-new-operating-system/deep/s07.webp)

Slide 7. Effective capability

[![Slide 8: same model, different harnesses](../slides/the-harness-is-the-new-operating-system/deep/s08.webp)](../slides/the-harness-is-the-new-operating-system/deep/s08.webp)

Slide 8. Same model, 8 harnesses

[![Slide 9: manager-worker scaffold](../slides/the-harness-is-the-new-operating-system/deep/s09.webp)](../slides/the-harness-is-the-new-operating-system/deep/s09.webp)

Slide 9. Manager-worker scaffold

[![Slide 10: blurry bar chart of scaffold results](../slides/the-harness-is-the-new-operating-system/deep/s10.webp)](../slides/the-harness-is-the-new-operating-system/deep/s10.webp)

Slide 10. Scaffold results (blurry)

[![Slide 11: the harness is the gatekeeper](../slides/the-harness-is-the-new-operating-system/deep/s11.webp)](../slides/the-harness-is-the-new-operating-system/deep/s11.webp)

Slide 11. The harness is the gatekeeper

[![Slide 12: OpenAI agents and Hugging Face](../slides/the-harness-is-the-new-operating-system/deep/s12.webp)](../slides/the-harness-is-the-new-operating-system/deep/s12.webp)

Slide 12. OpenAI and Hugging Face

[![Slide 13: capability does not grant authority](../slides/the-harness-is-the-new-operating-system/deep/s13.webp)](../slides/the-harness-is-the-new-operating-system/deep/s13.webp)

Slide 13. Capability isn’t authority

[![Slide 14: approval fatigue](../slides/the-harness-is-the-new-operating-system/deep/s14.webp)](../slides/the-harness-is-the-new-operating-system/deep/s14.webp)

Slide 14. Approval fatigue

[![Slide 15: room to work within authority](../slides/the-harness-is-the-new-operating-system/deep/s15.webp)](../slides/the-harness-is-the-new-operating-system/deep/s15.webp)

Slide 15. A better gate

[![Slide 16: the nature of agentic work](../slides/the-harness-is-the-new-operating-system/deep/s16.webp)](../slides/the-harness-is-the-new-operating-system/deep/s16.webp)

Slide 16. Agentic work

[![Slide 17: a model in a loop](../slides/the-harness-is-the-new-operating-system/deep/s17.webp)](../slides/the-harness-is-the-new-operating-system/deep/s17.webp)

Slide 17. A model in a loop

[![Slide 18: what makes each loop iteration count](../slides/the-harness-is-the-new-operating-system/deep/s18.webp)](../slides/the-harness-is-the-new-operating-system/deep/s18.webp)

Slide 18. The four parts

[![Slide 19: relevant information for the next decision](../slides/the-harness-is-the-new-operating-system/deep/s19.webp)](../slides/the-harness-is-the-new-operating-system/deep/s19.webp)

Slide 19. Context: working view

[![Slide 20: guidance sets role and rules](../slides/the-harness-is-the-new-operating-system/deep/s20.webp)](../slides/the-harness-is-the-new-operating-system/deep/s20.webp)

Slide 20. Context: role and rules

[![Slide 21: a pointer, not the whole thing](../slides/the-harness-is-the-new-operating-system/deep/s21.webp)](../slides/the-harness-is-the-new-operating-system/deep/s21.webp)

Slide 21. Context: pointers

[![Slide 22: tool interface shapes what the model can ask](../slides/the-harness-is-the-new-operating-system/deep/s22.webp)](../slides/the-harness-is-the-new-operating-system/deep/s22.webp)

Slide 22. Interface: what it can ask

[![Slide 23: same model, different interface](../slides/the-harness-is-the-new-operating-system/deep/s23.webp)](../slides/the-harness-is-the-new-operating-system/deep/s23.webp)

Slide 23. Interface: SWE-agent

[![Slide 24: compose operations using code](../slides/the-harness-is-the-new-operating-system/deep/s24.webp)](../slides/the-harness-is-the-new-operating-system/deep/s24.webp)

Slide 24. Interface: code

[![Slide 25: interface shapes what enters context](../slides/the-harness-is-the-new-operating-system/deep/s25.webp)](../slides/the-harness-is-the-new-operating-system/deep/s25.webp)

Slide 25. Interface: what comes back

[![Slide 26, first build: subagent as a tool call](../slides/the-harness-is-the-new-operating-system/deep/s26a.webp)](../slides/the-harness-is-the-new-operating-system/deep/s26a.webp)

Slide 26. Subagent as a tool call

[![Slide 26, final build: when decomposition helps or hurts](../slides/the-harness-is-the-new-operating-system/deep/s26b.webp)](../slides/the-harness-is-the-new-operating-system/deep/s26b.webp)

Slide 26. Decomposition helps or hurts

[![Slide 27: an action needs a place to run](../slides/the-harness-is-the-new-operating-system/deep/s27.webp)](../slides/the-harness-is-the-new-operating-system/deep/s27.webp)

Slide 27. Execution: a place to run

[![Slide 28: enforce a boundary](../slides/the-harness-is-the-new-operating-system/deep/s28.webp)](../slides/the-harness-is-the-new-operating-system/deep/s28.webp)

Slide 28. Execution: boundary

[![Slide 29: instructions can't enforce a boundary](../slides/the-harness-is-the-new-operating-system/deep/s29.webp)](../slides/the-harness-is-the-new-operating-system/deep/s29.webp)

Slide 29. Instructions aren’t a boundary

[![Slide 30: the model needs to know what happened](../slides/the-harness-is-the-new-operating-system/deep/s30.webp)](../slides/the-harness-is-the-new-operating-system/deep/s30.webp)

Slide 30. Feedback: what happened

[![Slide 32: observe the app](../slides/the-harness-is-the-new-operating-system/deep/s32.webp)](../slides/the-harness-is-the-new-operating-system/deep/s32.webp)

Slide 32. Feedback: observe the app

[![Slide 33: the harness runs the checks](../slides/the-harness-is-the-new-operating-system/deep/s33.webp)](../slides/the-harness-is-the-new-operating-system/deep/s33.webp)

Slide 33. Feedback: hooks

[![Slide 34: all the parts together](../slides/the-harness-is-the-new-operating-system/deep/s34.webp)](../slides/the-harness-is-the-new-operating-system/deep/s34.webp)

Slide 34. All parts together

[![Slide 35: mapping to an operating system](../slides/the-harness-is-the-new-operating-system/deep/s35.webp)](../slides/the-harness-is-the-new-operating-system/deep/s35.webp)

Slide 35. The OS mapping

[![Slide 36: harness design is never finished](../slides/the-harness-is-the-new-operating-system/deep/s36.webp)](../slides/the-harness-is-the-new-operating-system/deep/s36.webp)

Slide 36. Never finished

[![Slide 37: better model makes support unnecessary](../slides/the-harness-is-the-new-operating-system/deep/s37.webp)](../slides/the-harness-is-the-new-operating-system/deep/s37.webp)

Slide 37. Context anxiety

[![Slide 38: responsibility stays, mechanism changes](../slides/the-harness-is-the-new-operating-system/deep/s38.webp)](../slides/the-harness-is-the-new-operating-system/deep/s38.webp)

Slide 38. Mechanism changes

[![Slide 39: harness takes over what the model drops](../slides/the-harness-is-the-new-operating-system/deep/s39.webp)](../slides/the-harness-is-the-new-operating-system/deep/s39.webp)

Slide 39. LangChain loop

[![Slide 40: where do you look](../slides/the-harness-is-the-new-operating-system/deep/s40.webp)](../slides/the-harness-is-the-new-operating-system/deep/s40.webp)

Slide 40. Where to look

[![Slide 41: what will you try this week](../slides/the-harness-is-the-new-operating-system/deep/s41.webp)](../slides/the-harness-is-the-new-operating-system/deep/s41.webp)

Slide 41. Try this week
