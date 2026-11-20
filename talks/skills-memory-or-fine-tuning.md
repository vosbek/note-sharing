---
title: "Skills, Memory, or Fine-Tuning? The Engineering Loop Behind Production Agents"
---

# Skills, Memory, or Fine-Tuning? The Engineering Loop Behind Production Agents

**Speaker:** Abhinav Sinha (CEO, Lucidic AI)  
QCon SF 2026 · Engineering AI Systems · Tue Nov 17, 10:35 · Ballroom A  
[Session page](https://qconsf.com/presentation/nov2026/skills-memory-or-fine-tuning-engineering-loop-behind-self-improving-agents)

> Lucidic AI's CEO sorts every bad agent trace into six failure types, each with a ladder of fixes. Most fixes are small scoped calls, curated skills and cleaned-up memory, tested on held-out cases.

## Key points

- Abhinav sorts agent failures into six types: reasoning, context, preference, lack of knowledge, lack of ability and long tail. Name the type before choosing a fix.
- In Lucidic's data, new agents fail mostly on context and missing tools; mature agents mostly on reasoning and preference.
- For reasoning failures: give every call a small scope, then spend more tokens. Split into read, write, verify and send calls, and let code decide when it's done.
- He reported a ServiceNow ticket agent gaining 20 points of accuracy and closing twice the tickets after splitting, for 15% more tokens.
- More context is not better context. Load short chunks only when the task needs them.
- He cited SkillsBench: human-curated skills added 16.2 points; skills the model wrote for itself lost 1.3. Lucidic has people approve AI drafts ten lines at a time.
- A weekly dreaming job merges duplicate memories, drops stale ones and promotes repeats into skills, with a person approving the change.
- Preferences can be learned from saved draft-and-edit pairs; an LLM turns 30 to 40 pairs into written rules before anyone trains on them.
- Test fixes on held-out cases run three times each and judge by pass^k: a 90% agent passes only 73% of tasks at k=3.

From the session audio and 68 of roughly 73 slides. The phone transcript garbles names and numbers, so every figure here comes from a slide or its source. Lucidic’s own figures (the failure mix, the ServiceNow result, the legal curriculum) are the vendor’s measurements and are marked that way.

## The talk in brief

When an agent trace goes wrong, teams reach for whatever fix they know: a bigger model, another prompt line in capitals, a new skill, fine-tuning. Abhinav Sinha, whose company Lucidic tunes production agents, argued that the first job is to name the failure. He sorts every bad trace into one of six buckets (reasoning, context, preference, lack of knowledge, lack of ability, long tail), and each bucket has its own ladder of fixes, cheapest first.

The middle of most ladders is skills and memory, not fine-tuning. His strongest claims were that agents do better with small scopes and more tokens than with one huge window, that AI-written skills don’t help (backed by SkillsBench), and that a fix only counts once it holds on cases you held back, run more than once.

> “Skills and memory are the middle of most ladders. Fine-tuning is the last rung, and only on some of them.” (Slide 71)

## In depth

The talk followed the six failure types in order, then testing. Slide numbers are the deck’s own where visible.

### Six ways an agent fails (slides 3–8)

He opened on a research-agent trace with 318k tokens in one window and two of three claims unsupported, next to the usual list of things you could change: the prompt, skills, memory, the harness, a bigger model, fine-tuning, or the word “IMPORTANT” in capitals. All of those work sometimes, which is the problem. His taxonomy is meant to tell you which one fits. Cost and latency were out of scope.

| Failure           | The tell                                           | New agents | Mature agents |
|-------------------|----------------------------------------------------|------------|---------------|
| Reasoning         | It had everything it needed and still got it wrong | 7%         | 39%           |
| Context           | Your company knew something it was never told      | 37%        | 17%           |
| Preference        | You see why it did that; you just don’t want it    | 17%        | 26%           |
| Lack of knowledge | No context fixes it; it doesn’t know how           | 4%         | 4%            |
| Lack of ability   | No tool, no access                                 | 23%        | 8%            |
| Long tail         | Formats, overflow, error handling                  | 12%        | 6%            |

Share of failures from Lucidic’s own deployments across production agents (slide 8). Vendor data; not independently checked.

![Slide listing six types of failures in an agent trace: reasoning, context, preference, lack of knowledge, lack of ability, long tail.](../slides/skills-memory-or-fine-tuning/deep/p5919.webp)

Slide 7. The six failure types.

![Slide: the mix flips as an agent matures. New agents fail mostly on context and lack of ability; mature agents on reasoning and preference.](../slides/skills-memory-or-fine-tuning/deep/p5920.webp)

Slide 8. How the mix shifts with maturity.

**Takeaway:** early on, give the agent context and tools; once those are fixed, your remaining failures are reasoning and taste.

### Reasoning: why it gets things wrong with everything in front of it (slides 10–16)

His example was the April 2026 PocketOS incident: a coding agent on a routine staging task hit a credential mismatch, found an unrelated token and deleted a production volume, backups included, in nine seconds. Its rules said never to guess. Asked why, it listed the rules it had just broken. (The data was later restored.)

He blamed attention, not intelligence. A 300k-token window is about 25 hours of nonstop talk at speaking pace, and then you ask the model about one sentence in it. Lost in the Middle showed the U shape: GPT-3.5-Turbo answered 75.8% correctly with the answer document first, 53.8% with it in the middle, and 56.1% with no documents at all. Chroma’s context-rot work shows the U deepening as context grows. Shouting “IMPORTANT” at the top works mostly because the top of the U is where the model reads closely, not because of the capitals. Two agents that wiped production databases had their rule in capitals; one had been told eleven times.

![Slide: a coding agent wiped a production database in nine seconds. It had the rule never guess and later said that's exactly what I did.](../slides/skills-memory-or-fine-tuning/deep/p5921.webp)

Slide 10. The PocketOS deletion, as a reasoning failure.

![Chart of U-shaped attention from Lost in the Middle: 75.8% with the answer first, 53.8% in the middle, 63.2% at the end; 56.1% with no documents.](../slides/skills-memory-or-fine-tuning/deep/p5924.webp)

Slide 14. Models lose the middle.

### The fix: split, verify, debate (slides 18–29)

His main takeaway: give every call a small scope, then throw more tokens at it. You wouldn’t hand a junior engineer the whole architecture; you’d agree a design, then go one step at a time. He cited Anthropic’s multi-agent research system, where sub-agents with their own windows beat a single agent by 90.2% while using about 15 times the tokens of a chat. Raising the thinking budget does the same thing inside one call.

- **Split.** One job per call, each reading only what it needs: read (pull quotes, write nothing), write (one page from the quotes), verify (does each source say that?), send. The rule of thumb: if you need “and” to describe a call, split it again. Pass forward results, not raw output, and keep state in files.
- **Verify.** A second call checks the first in a fresh window that opens the sources, not the writer’s notes. A check only counts if it could have failed: check the outcome, not the action, and let code, not the model, decide when the work is done. He cited ImpossibleBench on agents passing tests by cheating.
- **Debate.** For the hardest calls, a proposer, a critic and a judge. A critic alone over-rejects (his once complained about comment style), so add a judge that hears both sides and cap the loop at two or three rounds.

![Table: one job per call. Read, write, verify, send, with what each reads, token counts and model size.](../slides/skills-memory-or-fine-tuning/deep/p5932.webp)

Slide 22. Split it like a newsroom.

![Code comparison: one growing loop versus a harness with four windows where code decides when it's done.](../slides/skills-memory-or-fine-tuning/deep/p5936.webp)

Slide 26. Stop appending, start passing.

Lucidic’s production result on a ServiceNow ticket-closure agent, measured on the half of real traffic it never trained on:

| Measure                            | One loop | Split and verify | Change     |
|------------------------------------|----------|------------------|------------|
| Closure accuracy, held-out         | 61%      | 81%              | +20 points |
| Tickets closed per 1,000, held-out | 212      | 431              | 2.0×       |
| Tokens per ticket, all windows     | 286k     | 329k             | +15%       |
| Largest single window              | 286k     | 96k              | −66%       |

Slide 27, Lucidic’s own measurement on a 50/50 split of real traffic. Not independently checked.

Only after the harness does he reach for a bigger model on the calls that fail (“this is what you pay the labs for”), then re-run the held-out set. Fine-tuning for reasoning is last, and it means policy-based RL such as GRPO that rewards the whole trajectory, not supervised fine-tuning on answers. Few companies are at that stage.

**Takeaway:** a few more tokens in total, spread over several smaller windows, is the whole trade.

### Context: the agent was never told (slides 31–43)

Even in mature agents, 17% of failures are context. His example was Cursor’s support bot in April 2025, which told a user that one device per subscription was a security policy. No such policy existed, and customers cancelled before the company corrected it. The model wasn’t dumb; it was missing one fact and filled the gap with something that sounded right.

His definitions: context is everything the model sees on this call; a skill is instructions for one kind of task, saved as a file and loaded when that task shows up; memory is facts learned from past runs, saved as files and loaded when relevant. Most context is bad for three reasons:

1.  **Teams add too much.** The fix for context rot is short context loaded only when the task needs it. His example loaded 371 tokens out of 48,200 on disk.
2.  **AI writes it.** In SkillsBench, human-curated skills raised pass rates 16.2 points and self-generated skills lowered them 1.3. An AI-written skill reads fine but says nothing specific: no names, no queues, no rule you could test. His reasoning: an agent only improves when it learns something it didn’t already know, so improvement needs outside information such as a person, a trace or a test result. Since nobody hand-writes everything, Lucidic uses a meta-skill: the AI drafts, shows ten lines at a time, and saves nothing until a person types “I approve”; anything else is an edit.
3.  **Nobody cleans it up.** Once a week a “dreaming” job rereads the week’s runs and the memory store, merges duplicates, drops stale and contradictory entries, promotes repeats into skills, and opens a PR a person approves. In his chart the store held near 20k tokens instead of growing toward 96k, and the share of loaded memory that was relevant stayed near 85% instead of falling to 35%. Anthropic ships the same idea as dreaming in Claude Managed Agents.

![Slide: don't use AI to write all your skills. Plus 16.2 points when a person wrote the skill, minus 1.3 when the model wrote its own, on 84 tasks.](../slides/skills-memory-or-fine-tuning/deep/p5948.webp)

Slide 37. Who writes the skill matters.

![Diagram: a weekly dream job replays runs, merges duplicates, drops stale entries, promotes repeats to skills, and opens a PR a person approves.](../slides/skills-memory-or-fine-tuning/deep/p5952.webp)

Slide 41. Once a week, it dreams.

Asked how to manage skills and rules across a large organisation, he described a shared file store with a weekly agent that treats contradictions like merge conflicts and hands the hard ones to a person. Asked about graphs, he said agents are tuned for code, so a file system with a good markdown index usually beats a context graph except at very large scale.

**Takeaway:** try a small prompt change first, then short skills each with an owner, then shared memory with dreaming. Supervised fine-tuning can bake context in, but only to cut cost.

### Preference: right, but not how you want it (slides 44–57)

Preference failures grow from 17% to 26% as agents mature. You can defend the output; you just wouldn’t send it. His example was the em dash: correct English that became a tell for AI writing. The root cause is organisational: the team building the agent isn’t the team doing the work, and the rules live in the other team’s heads.

His ladder, cheapest first:

1.  **Write down the rules you know**, the way you’d review a junior engineer’s PR. Every comment you’d leave becomes a line the agent reads.
2.  **Sit with the people who do the work** and ask why they changed what they changed.
3.  **Mock direct preference optimization.** Save every draft-and-edit as a pair, or swipe left and right on two drafts. An LLM reads 30 to 40 pairs, guesses the rules, drafts with them and fixes its misses. In Lucidic’s experiment, rule-following rose from 51% to 88% on seen picks and 84% on held-back ones.
4.  **Real DPO** when you have 5,000 to 10,000 pairs and want to change weights, not a page of rules.

He pointed to Shopify’s Sidekick as the same loop elsewhere: its LLM judge went from near-random agreement with experts (Cohen’s kappa 0.02) to 0.61, against 0.69 between the human experts themselves.

![Chart: an LLM reads preference pairs and writes rules; agreement rises from 51% to 88% over six rounds, 84% on held-back picks.](../slides/skills-memory-or-fine-tuning/deep/p5965.webp)

Slide 53. Rules from picks, not weights.

![Table: preference fixes in order. Write down known rules, ask the people who do the work, mock DPO, then direct preference optimization.](../slides/skills-memory-or-fine-tuning/deep/p5968.webp)

Slide 56. The preference ladder.

Asked where people add the most value as models improve, he said preference: there are many right ways to do anything, and depth in your own field is harder to commoditise than shallow knowledge.

### Lack of knowledge, lack of ability, and the long tail (slides 58–64)

Lack of knowledge is about 4% of failures. His example was TaxCalcBench: given every input, frontier models in mid-2025 computed fewer than a third of simple federal returns correctly, misusing tax tables and misjudging eligibility. No prompt fixes that. Lucidic’s experiment for a legal agent was a curriculum: law-school material in prerequisite order, easy to hard, turned into skill files. On a held-out legal benchmark the agent went from 11% with no help to 21% with curriculum-built skills, and 24% with post-training on top. His honest advice for most teams: at 4%, it probably isn’t worth solving; wait for a better base model.

Lack of ability means the agent never had the tool, and the fix is a pull request for the tool, its auth and its limits. The long tail is plumbing: timeouts, malformed tool arguments, rate limits, wrong output formats and oversized tool output. Retries with backoff, schema guards, and writing big results to a file and passing the path cover 93% of it in his data. None of those are prompt changes.

### Did it get better, or did it pass the one trace? (slides 65–70)

1.  **Cluster the failures**, with embeddings or by asking an LLM, and name each group. At scale he pointed to Anthropic’s Clio.
2.  **Split each cluster in half**: a training half you look at and a held-out half you never read. He suggests closer to 50/50 than the usual 90/10, because agents overfit easily and need little data.
3.  **Test in widening circles**: one case three times, then five cases three times each, then the training half, then the held-out half, then everything else, with a significance test.
4.  **Use pass^k.** From τ-bench: a case passes only if every run passes. A 90% agent is a 73% agent at k=3 (0.9³). In his example, one of five cases passed all three runs before the fix, where a single run would have said 60%; four of five passed after.
5.  **Pick the cases that tell you the most.** Once you have run history, cases that move together are one signal; keep one per group. tinyBenchmarks showed 100 well-picked MMLU questions standing in for all 14,000.

![Grid: five cases run three times before and after a fix; one of five passes all runs before, four of five after; pass^k curves.](../slides/skills-memory-or-fine-tuning/deep/p5980.webp)

Slide 68. Run each case three times.

![Diagram of three loops at three speeds: seconds for the harness, days for skills and memory, months for fine-tuning.](../slides/skills-memory-or-fine-tuning/deep/p5982.webp)

Slide 70. Three loops at three speeds.

He closed with three loops at three speeds: the harness (verify, retry) in seconds, skills and memory in days, and fine-tuning in months. Most wins live in the inner two.

### The slide to photograph (slide 71)

| Failure           | The tell                    | Try first                       | Then                                     | Last                           |
|-------------------|-----------------------------|---------------------------------|------------------------------------------|--------------------------------|
| Reasoning         | Had everything, still wrong | A bigger model, more thinking   | Split, verify, debate                    | RL fine-tuning (GRPO)          |
| Context           | A rule nobody wrote down    | One small prompt change         | Short context chunks, each with an owner | Shared memory plus dreaming    |
| Preference        | Defensible, not your way    | Write down known rules          | Mock DPO: pairs in, rules out            | Direct preference optimization |
| Lack of knowledge | Right answer out of reach   | Curriculum-built skills         | A better base model                      | Post-training on top           |
| Lack of ability   | No tool, no access          | Ship the tool                   |                                          |                                |
| Long tail         | Plumbing                    | Retries, guards, write to files |                                          |                                |

## Numbers we checked

Checked on Nov 17, 2026. Lucidic’s own measurements are marked “Vendor”.

| Claim                                                          | Figure                                                          | Source                                                                                                                          | Status                                    |
|----------------------------------------------------------------|-----------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------|
| Answer position changes accuracy (GPT-3.5-Turbo, 20 documents) | 75.8% first, 53.8% middle, 56.1% closed-book, 88.3% answer only | [Liu et al., Lost in the Middle](https://arxiv.org/abs/2307.03172)                                                              | Checked                                   |
| Performance falls as input grows                               | Curve values on slide 16                                        | [Chroma, Context Rot, July 2025](https://research.trychroma.com/context-rot)                                                    | Caveat trend checked, slide values not    |
| Sub-agents beat one agent                                      | 90.2% better, about 15× the tokens of a chat                    | [Anthropic, June 2025](https://www.anthropic.com/engineering/multi-agent-research-system)                                       | Caveat Anthropic’s internal research eval |
| Human-written vs AI-written skills                             | +16.2 vs −1.3 points, 84 tasks                                  | [SkillsBench, Li et al., 2026](https://arxiv.org/abs/2602.12670)                                                                | Checked                                   |
| 2 or 3 skills vs 4 or more                                     | +18.6 vs +5.9 points                                            | Slide 33; the paper reports focused 2–3 module skills doing best                                                                | Slide only                                |
| LLM judge agreement with experts                               | Kappa 0.02 to 0.61; experts 0.69                                | [Shopify Engineering](https://shopify.engineering/building-production-ready-agentic-systems)                                    | Checked                                   |
| Models computing tax returns                                   | Fewer than 1 in 3 correct, mid-2025                             | [TaxCalcBench, Bock et al.](https://arxiv.org/abs/2507.16126)                                                                   | Checked                                   |
| Small eval set stands in for a large one                       | 100 curated vs 14,000 MMLU questions                            | [tinyBenchmarks, ICML 2024](https://arxiv.org/abs/2402.14992)                                                                   | Checked                                   |
| A 90% agent at k=3                                             | 73% (0.9³ = 0.729)                                              | [τ-bench pass^k](https://arxiv.org/abs/2406.12045); arithmetic rerun                                                            | Checked                                   |
| 300k tokens is a 25-hour meeting                               | 300k × 0.75 words ÷ 150 words a minute = 25 hours               | Arithmetic rerun on the slide’s assumptions                                                                                     | Checked                                   |
| Agent deleted a production database                            | 9 seconds, backups included; data later restored                | [Decrypt](https://decrypt.co/365897/ai-agent-deletes-startup-database-9-seconds-founder-says), April 2026                       | Checked                                   |
| Support bot invented a policy                                  | “One device per subscription”, April 2025                       | [CX Today](https://www.cxtoday.com/conversational-ai/a-contact-center-chatbot-invents-company-policies-now-customers-want-out/) | Checked                                   |
| Failure mix, new vs mature agents                              | Context 37% → 17%; reasoning 7% → 39%                           | Lucidic deployments                                                                                                             | Vendor                                    |
| ServiceNow ticket agent after split and verify                 | +20 points, 2.0× closed, +15% tokens                            | Lucidic, slide 27                                                                                                               | Vendor                                    |
| Legal curriculum                                               | 11% to 21%, 24% with post-training                              | Lucidic, slide 61                                                                                                               | Vendor                                    |

## About the speaker

Abhinav Sinha is CEO of Lucidic AI, which takes companies’ production agent data and helps them improve their agents; he says it has seen tens of billions of production traces. Before Lucidic he did reinforcement-learning research at the Stanford AI Lab, worked on deep-learning trading strategies at Citadel and SIG, and did distributed systems and early AI engineering at Apple. Lucidic also had a booth this week; see [the Lucidic booth notes](booth-lucidic-ai.md).

## Terms and technologies

### Context and memory

[Lost in the Middle](https://arxiv.org/abs/2307.03172)  
2023 study showing models use information at the start and end of a long input far better than the middle. The basis for his U-shaped attention argument.

[Context rot](https://research.trychroma.com/context-rot)  
Chroma’s 2025 term for the drop in reliability as input length grows, measured across 18 models.

Skill  
Instructions for one kind of task, saved as a file (often SKILL.md) and loaded only when that task appears.

Agent memory  
Facts learned from past runs, saved as files and loaded when relevant.

[SkillsBench](https://arxiv.org/abs/2602.12670)  
2026 benchmark of agent skills across 11 domains, comparing no skills, human-curated skills and self-generated skills.

[Dreaming](https://platform.claude.com/docs/en/managed-agents/dreams)  
A scheduled job that reviews past sessions and a memory store, then writes back a cleaner store. Anthropic offers it in research preview for Claude Managed Agents; Lucidic described its own version.

### Reasoning and harness design

[Sub-agents](https://www.anthropic.com/engineering/multi-agent-research-system)  
Separate model calls with their own context windows, each doing one part of a job and returning a short summary.

[Chain of thought](https://arxiv.org/abs/2201.11903)  
Letting a model write intermediate steps before the answer (Wei et al., 2022). Raising a “thinking” setting buys more of this scratch work.

LLM-as-judge and debate  
A second model grades or critiques the first. He uses a proposer, a critic and a judge so that one over-eager critic doesn’t block everything.

[ImpossibleBench](https://arxiv.org/abs/2510.20270)  
2025 benchmark that makes tasks impossible to pass honestly, to measure how often agents cheat on tests. Why he says a check only counts if it could have failed.

### Training

[Direct preference optimization (DPO)](https://arxiv.org/abs/2305.18290)  
2023 Stanford method that trains a model directly on pairs of preferred and rejected outputs, with no separate reward model.

GRPO  
Group relative policy optimization, a reinforcement-learning method that scores groups of attempts at the same task. His last resort for reasoning failures.

Supervised fine-tuning (SFT)  
Training on examples of correct answers. He said it can bake in context to cut cost, but doesn’t fix reasoning.

### Evaluation

[τ-bench and pass^k](https://arxiv.org/abs/2406.12045)  
Sierra’s 2024 agent benchmark, which introduced pass^k: the chance that all k runs of the same task succeed.

[tinyBenchmarks](https://arxiv.org/abs/2402.14992)  
Method for picking a small set of evaluation cases that predicts the full benchmark’s result.

[Shopify Sidekick evaluation](https://shopify.engineering/building-production-ready-agentic-systems)  
Shopify’s write-up of calibrating LLM judges against human experts, using Cohen’s kappa.

[TaxCalcBench](https://arxiv.org/abs/2507.16126)  
Column Tax’s benchmark of 51 federal returns; his example of a knowledge gap no context fixes.

### Incidents

[PocketOS deletion](https://decrypt.co/365897/ai-agent-deletes-startup-database-9-seconds-founder-says)  
April 2026: a Cursor agent deleted a startup’s production volume and backups through one infrastructure API call. His reasoning-failure example.

[Cursor support bot](https://www.cxtoday.com/conversational-ai/a-contact-center-chatbot-invents-company-policies-now-customers-want-out/)  
April 2025: Cursor’s AI support agent invented a device policy. His context-failure example.

## Reading and tools

- Li et al., [SkillsBench](https://arxiv.org/abs/2602.12670) (2026). Read this before anyone bulk-generates skills.
- Anthropic, [How we built our multi-agent research system](https://www.anthropic.com/engineering/multi-agent-research-system) (June 2025).
- Liu et al., [Lost in the Middle](https://arxiv.org/abs/2307.03172) (2023), and Chroma, [Context Rot](https://research.trychroma.com/context-rot) (2025).
- Shopify Engineering, [Building production-ready agentic systems](https://shopify.engineering/building-production-ready-agentic-systems) (2025).
- Claude Platform docs, [Dreams](https://platform.claude.com/docs/en/managed-agents/dreams), and the [launch post](https://claude.com/blog/new-in-claude-managed-agents) (May 2026).
- Yao et al., [τ-bench](https://arxiv.org/abs/2406.12045) (2024); Maia Polo et al., [tinyBenchmarks](https://arxiv.org/abs/2402.14992) (2024).
- Zhong, Raghunathan and Carlini, [ImpossibleBench](https://arxiv.org/abs/2510.20270) (2025); Bock et al., [TaxCalcBench](https://arxiv.org/abs/2507.16126) (2025).

### Related sessions

- [Generation Got Cheap, Trust Didn’t](generation-got-cheap-trust-didnt.md) (Roblox, Monday). Mining review history for review rules is the same “asymmetric information” idea.
- [The Harness Is the New Operating System](the-harness-is-the-new-operating-system.md) (Monday keynote). Same argument that the harness, not the model, is where most gains are.

## All slides

[![Slide: Title](../slides/skills-memory-or-fine-tuning/deep/p5914.webp)](../slides/skills-memory-or-fine-tuning/deep/p5914.webp)

Slide 1. Title

[![Slide: Keep it up if it works 100% of the time](../slides/skills-memory-or-fine-tuning/deep/p5915.webp)](../slides/skills-memory-or-fine-tuning/deep/p5915.webp)

Slide 2. Keep it up if it works 100% of the time

[![Slide: You’re staring at a bad trace. What do you change?](../slides/skills-memory-or-fine-tuning/deep/p5916.webp)](../slides/skills-memory-or-fine-tuning/deep/p5916.webp)

Slide 3. You’re staring at a bad trace. What do you change?

[![Slide: What I’ll cover](../slides/skills-memory-or-fine-tuning/deep/p5917.webp)](../slides/skills-memory-or-fine-tuning/deep/p5917.webp)

Slide 4. What I’ll cover

[![Slide: Speaker intro](../slides/skills-memory-or-fine-tuning/deep/p5918.webp)](../slides/skills-memory-or-fine-tuning/deep/p5918.webp)

Slide 5. Speaker intro

[![Slide: Types of failures in an agent trace](../slides/skills-memory-or-fine-tuning/deep/p5919.webp)](../slides/skills-memory-or-fine-tuning/deep/p5919.webp)

Slide 6. Types of failures in an agent trace

[![Slide: The mix flips as an agent matures](../slides/skills-memory-or-fine-tuning/deep/p5920.webp)](../slides/skills-memory-or-fine-tuning/deep/p5920.webp)

Slide 7. The mix flips as an agent matures

[![Slide: A coding agent wiped a production database](../slides/skills-memory-or-fine-tuning/deep/p5921.webp)](../slides/skills-memory-or-fine-tuning/deep/p5921.webp)

Slide 8. A coding agent wiped a production database

[![Slide: 2:35 was a break](../slides/skills-memory-or-fine-tuning/deep/p5922.webp)](../slides/skills-memory-or-fine-tuning/deep/p5922.webp)

Slide 9. 2:35 was a break

[![Slide: A 300k-token context is a 25-hour meeting](../slides/skills-memory-or-fine-tuning/deep/p5923.webp)](../slides/skills-memory-or-fine-tuning/deep/p5923.webp)

Slide 10. A 300k-token context is a 25-hour meeting

[![Slide: U-shaped attention](../slides/skills-memory-or-fine-tuning/deep/p5924.webp)](../slides/skills-memory-or-fine-tuning/deep/p5924.webp)

Slide 11. U-shaped attention

[![Slide: “IMPORTANT!!!” at the very top](../slides/skills-memory-or-fine-tuning/deep/p5925.webp)](../slides/skills-memory-or-fine-tuning/deep/p5925.webp)

Slide 12. “IMPORTANT!!!” at the very top

[![Slide: The more you put in, the worse it gets](../slides/skills-memory-or-fine-tuning/deep/p5926.webp)](../slides/skills-memory-or-fine-tuning/deep/p5926.webp)

Slide 13. The more you put in, the worse it gets

[![Slide: Brief an agent like a junior engineer](../slides/skills-memory-or-fine-tuning/deep/p5927.webp)](../slides/skills-memory-or-fine-tuning/deep/p5927.webp)

Slide 14. Brief an agent like a junior engineer

[![Slide: Small scope, more tokens](../slides/skills-memory-or-fine-tuning/deep/p5928.webp)](../slides/skills-memory-or-fine-tuning/deep/p5928.webp)

Slide 15. Small scope, more tokens

[![Slide: More tokens means more scratch work](../slides/skills-memory-or-fine-tuning/deep/p5929.webp)](../slides/skills-memory-or-fine-tuning/deep/p5929.webp)

Slide 16. More tokens means more scratch work

[![Slide: Split, verify, debate](../slides/skills-memory-or-fine-tuning/deep/p5930.webp)](../slides/skills-memory-or-fine-tuning/deep/p5930.webp)

Slide 17. Split, verify, debate

[![Slide: One 318k window becomes four small jobs](../slides/skills-memory-or-fine-tuning/deep/p5931.webp)](../slides/skills-memory-or-fine-tuning/deep/p5931.webp)

Slide 18. One 318k window becomes four small jobs

[![Slide: One job per call](../slides/skills-memory-or-fine-tuning/deep/p5932.webp)](../slides/skills-memory-or-fine-tuning/deep/p5932.webp)

Slide 19. One job per call

[![Slide: A second call checks the first](../slides/skills-memory-or-fine-tuning/deep/p5933.webp)](../slides/skills-memory-or-fine-tuning/deep/p5933.webp)

Slide 20. A second call checks the first

[![Slide: A check only counts if it could have failed](../slides/skills-memory-or-fine-tuning/deep/p5934.webp)](../slides/skills-memory-or-fine-tuning/deep/p5934.webp)

Slide 21. A check only counts if it could have failed

[![Slide: A small debate loop](../slides/skills-memory-or-fine-tuning/deep/p5935.webp)](../slides/skills-memory-or-fine-tuning/deep/p5935.webp)

Slide 22. A small debate loop

[![Slide: Stop appending, start passing](../slides/skills-memory-or-fine-tuning/deep/p5936.webp)](../slides/skills-memory-or-fine-tuning/deep/p5936.webp)

Slide 23. Stop appending, start passing

[![Slide: ServiceNow result](../slides/skills-memory-or-fine-tuning/deep/p5937.webp)](../slides/skills-memory-or-fine-tuning/deep/p5937.webp)

Slide 24. ServiceNow result

[![Slide: First: try a bigger model](../slides/skills-memory-or-fine-tuning/deep/p5938.webp)](../slides/skills-memory-or-fine-tuning/deep/p5938.webp)

Slide 25. First: try a bigger model

[![Slide: Reasoning: what to try, in order](../slides/skills-memory-or-fine-tuning/deep/p5939.webp)](../slides/skills-memory-or-fine-tuning/deep/p5939.webp)

Slide 26. Reasoning: what to try, in order

[![Slide: Fine-tuning for reasoning](../slides/skills-memory-or-fine-tuning/deep/p5940.webp)](../slides/skills-memory-or-fine-tuning/deep/p5940.webp)

Slide 27. Fine-tuning for reasoning

[![Slide: 02 / 06 Context](../slides/skills-memory-or-fine-tuning/deep/p5941.webp)](../slides/skills-memory-or-fine-tuning/deep/p5941.webp)

Slide 28. 02 / 06 Context

[![Slide: A support bot made up a policy](../slides/skills-memory-or-fine-tuning/deep/p5942.webp)](../slides/skills-memory-or-fine-tuning/deep/p5942.webp)

Slide 29. A support bot made up a policy

[![Slide: Context, skill, memory](../slides/skills-memory-or-fine-tuning/deep/p5944.webp)](../slides/skills-memory-or-fine-tuning/deep/p5944.webp)

Slide 30. Context, skill, memory

[![Slide: Three reasons context is bad](../slides/skills-memory-or-fine-tuning/deep/p5945.webp)](../slides/skills-memory-or-fine-tuning/deep/p5945.webp)

Slide 31. Three reasons context is bad

[![Slide: More context is not better context](../slides/skills-memory-or-fine-tuning/deep/p5946.webp)](../slides/skills-memory-or-fine-tuning/deep/p5946.webp)

Slide 32. More context is not better context

[![Slide: Load 371 tokens, not 48,200](../slides/skills-memory-or-fine-tuning/deep/p5947.webp)](../slides/skills-memory-or-fine-tuning/deep/p5947.webp)

Slide 33. Load 371 tokens, not 48,200

[![Slide: Don’t use AI to write all your skills](../slides/skills-memory-or-fine-tuning/deep/p5948.webp)](../slides/skills-memory-or-fine-tuning/deep/p5948.webp)

Slide 34. Don’t use AI to write all your skills

[![Slide: A meta-skill for approving skills](../slides/skills-memory-or-fine-tuning/deep/p5949.webp)](../slides/skills-memory-or-fine-tuning/deep/p5949.webp)

Slide 35. A meta-skill for approving skills

[![Slide: Type “I approve” ten times](../slides/skills-memory-or-fine-tuning/deep/p5950.webp)](../slides/skills-memory-or-fine-tuning/deep/p5950.webp)

Slide 36. Type “I approve” ten times

[![Slide: Improvement needs outside information](../slides/skills-memory-or-fine-tuning/deep/p5951.webp)](../slides/skills-memory-or-fine-tuning/deep/p5951.webp)

Slide 37. Improvement needs outside information

[![Slide: Once a week, it dreams](../slides/skills-memory-or-fine-tuning/deep/p5952.webp)](../slides/skills-memory-or-fine-tuning/deep/p5952.webp)

Slide 38. Once a week, it dreams

[![Slide: What dreaming buys you](../slides/skills-memory-or-fine-tuning/deep/p5954.webp)](../slides/skills-memory-or-fine-tuning/deep/p5954.webp)

Slide 39. What dreaming buys you

[![Slide: Context: what to try, in order](../slides/skills-memory-or-fine-tuning/deep/p5955.webp)](../slides/skills-memory-or-fine-tuning/deep/p5955.webp)

Slide 40. Context: what to try, in order

[![Slide: 03 / 06 Preference](../slides/skills-memory-or-fine-tuning/deep/p5956.webp)](../slides/skills-memory-or-fine-tuning/deep/p5956.webp)

Slide 41. 03 / 06 Preference

[![Slide: An em dash isn’t wrong](../slides/skills-memory-or-fine-tuning/deep/p5957.webp)](../slides/skills-memory-or-fine-tuning/deep/p5957.webp)

Slide 42. An em dash isn’t wrong

[![Slide: Nothing is wrong with this email](../slides/skills-memory-or-fine-tuning/deep/p5958.webp)](../slides/skills-memory-or-fine-tuning/deep/p5958.webp)

Slide 43. Nothing is wrong with this email

[![Slide: The builders aren’t the users](../slides/skills-memory-or-fine-tuning/deep/p5959.webp)](../slides/skills-memory-or-fine-tuning/deep/p5959.webp)

Slide 44. The builders aren’t the users

[![Slide: Write it down like a PR review](../slides/skills-memory-or-fine-tuning/deep/p5960.webp)](../slides/skills-memory-or-fine-tuning/deep/p5960.webp)

Slide 45. Write it down like a PR review

[![Slide: Step two: meditate](../slides/skills-memory-or-fine-tuning/deep/p5961.webp)](../slides/skills-memory-or-fine-tuning/deep/p5961.webp)

Slide 46. Step two: meditate

[![Slide: Mock direct preference optimization](../slides/skills-memory-or-fine-tuning/deep/p5962.webp)](../slides/skills-memory-or-fine-tuning/deep/p5962.webp)

Slide 47. Mock direct preference optimization

[![Slide: Save both versions](../slides/skills-memory-or-fine-tuning/deep/p5963.webp)](../slides/skills-memory-or-fine-tuning/deep/p5963.webp)

Slide 48. Save both versions

[![Slide: Swipe on drafts](../slides/skills-memory-or-fine-tuning/deep/p5964.webp)](../slides/skills-memory-or-fine-tuning/deep/p5964.webp)

Slide 49. Swipe on drafts

[![Slide: An LLM writes down the rules](../slides/skills-memory-or-fine-tuning/deep/p5965.webp)](../slides/skills-memory-or-fine-tuning/deep/p5965.webp)

Slide 50. An LLM writes down the rules

[![Slide: The rules you never wrote down](../slides/skills-memory-or-fine-tuning/deep/p5966.webp)](../slides/skills-memory-or-fine-tuning/deep/p5966.webp)

Slide 51. The rules you never wrote down

[![Slide: Anywhere taste matters](../slides/skills-memory-or-fine-tuning/deep/p5967.webp)](../slides/skills-memory-or-fine-tuning/deep/p5967.webp)

Slide 52. Anywhere taste matters

[![Slide: Preference: what to try, in order](../slides/skills-memory-or-fine-tuning/deep/p5968.webp)](../slides/skills-memory-or-fine-tuning/deep/p5968.webp)

Slide 53. Preference: what to try, in order

[![Slide: Train on thousands of picks](../slides/skills-memory-or-fine-tuning/deep/p5969.webp)](../slides/skills-memory-or-fine-tuning/deep/p5969.webp)

Slide 54. Train on thousands of picks

[![Slide: 04 / 06 Lack of knowledge](../slides/skills-memory-or-fine-tuning/deep/p5970.webp)](../slides/skills-memory-or-fine-tuning/deep/p5970.webp)

Slide 55. 04 / 06 Lack of knowledge

[![Slide: It still couldn’t do the taxes](../slides/skills-memory-or-fine-tuning/deep/p5971.webp)](../slides/skills-memory-or-fine-tuning/deep/p5971.webp)

Slide 56. It still couldn’t do the taxes

[![Slide: Teach it like a first-year](../slides/skills-memory-or-fine-tuning/deep/p5972.webp)](../slides/skills-memory-or-fine-tuning/deep/p5972.webp)

Slide 57. Teach it like a first-year

[![Slide: The order did the work](../slides/skills-memory-or-fine-tuning/deep/p5973.webp)](../slides/skills-memory-or-fine-tuning/deep/p5973.webp)

Slide 58. The order did the work

[![Slide: Knowledge: what to try, in order](../slides/skills-memory-or-fine-tuning/deep/p5974.webp)](../slides/skills-memory-or-fine-tuning/deep/p5974.webp)

Slide 59. Knowledge: what to try, in order

[![Slide: 05 / 06 It never had the tool](../slides/skills-memory-or-fine-tuning/deep/p5975.webp)](../slides/skills-memory-or-fine-tuning/deep/p5975.webp)

Slide 60. 05 / 06 It never had the tool

[![Slide: 06 / 06 Everything else is plumbing](../slides/skills-memory-or-fine-tuning/deep/p5976.webp)](../slides/skills-memory-or-fine-tuning/deep/p5976.webp)

Slide 61. 06 / 06 Everything else is plumbing

[![Slide: Testing agents in production](../slides/skills-memory-or-fine-tuning/deep/p5977.webp)](../slides/skills-memory-or-fine-tuning/deep/p5977.webp)

Slide 62. Testing agents in production

[![Slide: Cluster the failures](../slides/skills-memory-or-fine-tuning/deep/p5978.webp)](../slides/skills-memory-or-fine-tuning/deep/p5978.webp)

Slide 63. Cluster the failures

[![Slide: Test in widening circles](../slides/skills-memory-or-fine-tuning/deep/p5979.webp)](../slides/skills-memory-or-fine-tuning/deep/p5979.webp)

Slide 64. Test in widening circles

[![Slide: Hold out five, run three times](../slides/skills-memory-or-fine-tuning/deep/p5980.webp)](../slides/skills-memory-or-fine-tuning/deep/p5980.webp)

Slide 65. Hold out five, run three times

[![Slide: Pick the cases that tell you the most](../slides/skills-memory-or-fine-tuning/deep/p5981.webp)](../slides/skills-memory-or-fine-tuning/deep/p5981.webp)

Slide 66. Pick the cases that tell you the most

[![Slide: Three loops at three speeds](../slides/skills-memory-or-fine-tuning/deep/p5982.webp)](../slides/skills-memory-or-fine-tuning/deep/p5982.webp)

Slide 67. Three loops at three speeds

[![Slide: Name the failure, take its ladder](../slides/skills-memory-or-fine-tuning/deep/p5983.webp)](../slides/skills-memory-or-fine-tuning/deep/p5983.webp)

Slide 68. Name the failure, take its ladder
