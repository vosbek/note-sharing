---
title: "How To Kill the Code Review"
---

# How To Kill the Code Review

**Speaker:** Ankit Jain (Co-Founder & CEO, Aviator)  
QCon SF 2026 · Engineering the Developer Experience · Wed Nov 18, 15:55 · Ballroom A  
[Session page](https://qconsf.com/presentation/nov2026/how-kill-code-review)

> Aviator's Ankit Jain on keeping code review while killing line-by-line reading: agents find bugs and enforce team rules, and people review the decisions behind each change.

## Key points

- Ankit opened by saying he sells a replacement for code review, so the room should be suspicious of him and judge what fits its own scale.
- He said review was never mostly about bugs. At Microsoft 44% of developers ranked finding defects first, but 14% of comments were about defects. Google's study of 9 million changes found the same. Review builds shared mental models.
- He argued teams have already stopped reading AI-written diffs. He cited Faros figures (PRs merged with no review up 76%, incidents per month up 125%). On his own team, nine engineers merge 4x the PRs, and a person still approves each one without reading the diff.
- He said AI review is noisy, but humans were never good at it either: detection falls off past about 400 lines or 60 minutes. The result is review theater. Agents write and review in a loop, and a person skims and merges.
- He graded his March essay's five layers of trust. The structure was right, but no layer asked whether the team is building the right thing. He had missed human judgment.
- His replacement is six verbs. Argue: agents cross-examine before the PR. Capture: intent and acceptance criteria from the session. Codify: repeated comments become enforced invariants. Prove: evidence per criterion. Debate: people review decisions, not diffs. Own: teams own the rules.
- His team mined 11,400 review comments into 212 candidate rules and kept 64 invariants. Each has a rule, scope, verification method, provenance and owner. A system separate from the coding agent checks them.
- He showed an incident that passed every layer: a query on a large table without an index. Rollback finished 18 minutes after impact. They asked which rule was missing, not who approved it. A year in, his team reports median time to merge of 3.4 hours, down from 2.1 days.

From an audio recording and 109 photos of the deck, kept here as 98 slides. The deck has no printed slide numbers, so slides are numbered in the order they were shown, and earlier builds of the same slide were dropped. Only the first item of “Where decisions come from” (slide 74) was photographed; the other three are recovered from the recording. The section on essays, docs and repos is our own reading, done the same evening.

## The talk in brief

Ankit Jain opened by telling the room to be suspicious of him: he argues for killing the code review, and his company sells the replacement. Then he spent most of the hour on what review is actually for. Two large studies, one at Microsoft and one at Google, found that people say they review to find defects, while most of what reviews produce is shared understanding of the system. His claim is that teams have already stopped reading AI-written diffs, so that understanding is quietly going away while every PR still gets a human approval.

His March essay proposed five layers of automated trust, stacked like the Swiss cheese model. On stage he said that structure was right but that he had “missed the human judgment entirely”. The replacement is six verbs: **Argue** (agents cross-examine a change before the PR exists), **Capture** (record intent and acceptance criteria from the coding session), **Codify** (turn repeated review comments into enforced invariants, an “AI slop register”), **Prove** (evidence per criterion, not a green check), **Debate** (humans review decisions, not diffs) and **Own** (teams own the rules that verify the code). He showed a year of his own nine-person team running it, including an incident that passed every filter, and closed with a 90-day pilot plan.

> “Knowledge sharing was never a side effect of review. It was the product.” (Slide 70)

## In depth

This follows the order of the talk. Slide numbers are in each heading.

### Be suspicious of me, and what the essay got wrong (Slides 1–4, 31–32)

Ankit runs Aviator and the Hangar DX community that most speakers on this track came from. He was last on the track and said most of what he would cover had already come up in the earlier sessions. His disclaimer was explicit: he sells a replacement for code review, so the room should use its own judgment about what fits its scale and organization.

The talk revisits his March 2026 Latent Space essay, “How to Kill the Code Review”. That essay proposed five layers of trust between “specs plus agents” and the merge: compare multiple options (several agents try a change and are ranked by tests, diff size and dependencies), deterministic guardrails (linters, types, contracts), humans define acceptance criteria upstream, permission systems that scope what an agent may touch unattended, and adversarial verification by a separate agent. No single layer catches everything; stacked, the holes stop lining up.

![Slide 3: Code reviews are dead: the How to Kill the Code Review diagram of five Swiss cheese slices (compare multiple options, deterministic guardrails, acceptance criteria, permission systems, adversarial verification) between specs plus agents and the merge. latent.space/p/reviews-dead, Latent Space, March 2026.](../slides/how-to-kill-the-code-review/deep/s03.webp)

Slide 3. Code reviews are dead

![Slide 4: Five layers of trust: 1 compare multiple options, several agents try it, rank by tests, diff size, deps; 2 deterministic guardrails, linters, types, contracts, facts not opinions; 3 humans define acceptance criteria, written upstream before the code exists; 4 permission systems, scope what an agent may touch unattended; 5 adversarial verification, a separate agent tries to break it.](../slides/how-to-kill-the-code-review/deep/s04.webp)

Slide 4. Five layers of trust

Halfway through the talk he came back to that slide and graded it. Four of the five layers answer “is it right?”, one answers “is it what we meant?”, and none asks “are we building the right thing?”. His words: the structure was right, and he had missed the human judgment entirely.

**Takeaway.** This is a vendor revising his own published position in public, eight months later, toward keeping humans in the loop. That makes the second half of the talk more credible than the title suggests.

### Why we review code (Slides 5–11)

He grounded the argument in two studies. Bacchelli and Bird (ICSE 2013) surveyed developers at Microsoft and classified 570 review comments: 44% of programmers named finding defects as their first motivation, yet only 14% of comments were about defects. Most were about code improvements, understanding and alternative solutions. Google’s 2018 case study, covering 9 million reviewed changes, reached the same conclusion.

![Slide 6: Bar chart: 44% rank finding defects as their number one reason for review; 14% of actual comments are about defects. Bacchelli and Bird, ICSE 2013, 570 comments classified.](../slides/how-to-kill-the-code-review/deep/s06.webp)

Slide 6. 44% say it's to find defects

![Slide 7: 9,000,000 reviewed changes at Google, same finding. Sadowski et al., ICSE-SEIP 2018.](../slides/how-to-kill-the-code-review/deep/s07.webp)

Slide 7. 9,000,000

From there he made three short claims, one slide each: code review is not about the code, it is how a team builds mental models, and it is how knowledge moves. As long as people work in teams rather than alone, some review is needed. He closed the section with Addy Osmani’s line that we made writing cheap and understanding stayed exactly as expensive as it has always been. Understanding is the one cost AI has not lowered, and it is what review was protecting.

| Study                                     | Data                                                                   | Finding Ankit used                                                              |
|-------------------------------------------|------------------------------------------------------------------------|---------------------------------------------------------------------------------|
| Bacchelli and Bird, ICSE 2013 (Microsoft) | 873 programmers surveyed; 570 comments in 200 threads classified       | 44% rank finding defects first; 14% of comments concern defects                 |
| Sadowski et al., ICSE-SEIP 2018 (Google)  | 12 interviews, 44 survey responses, logs of 9 million reviewed changes | Review at Google is about education, norms and understanding as much as defects |

### The problem: we already stopped reading (Slides 12–18)

His real question was not whether to keep code review but how long until nobody reads the code. His answer: we already don’t. He cited Faros AI’s Q3 2026 report, “The Speed Trap” (22,000 developers, 4,000 teams): PRs merged with no review up 76%, average PR size up 72%, work restarts up 67% and incidents per month up 125%. On stage he described the first figure as over 75% of PRs merging unreviewed; the report and the slide describe a 76% increase, not a 76% share. DORA’s 2025 report found AI adoption raises delivery throughput and delivery instability at the same time, so a velocity chart and an incident chart can both be right.

![Slide 13: We already have: +76% PRs merged with no review at all, +72% average PR size, +67% work restarts, +125% incidents per month. Faros AI Engineering Report Q3 2026, The Speed Trap, 18 Sep 2026, 22,000 devs, 4,000 teams.](../slides/how-to-kill-the-code-review/deep/s13.webp)

Slide 13. We already have

![Slide 17: Our team, a year apart: 4x PRs merged per week, 9 engineers both years, every PR still approved by a human. Aviator engineering, Nov 2025 to Nov 2026.](../slides/how-to-kill-the-code-review/deep/s17.webp)

Slide 17. Our team, a year apart

He quoted Gergely Orosz on engineers who still review carefully feeling overloaded by AI slop PRs, and showed an r/ExperiencedDevs post from someone who announced at a company meeting that they would stop reviewing AI-generated PRs. Nobody voted to stop reviewing code; teams just stopped. His own team is the example: nine engineers both years, 4x the PRs merged per week, and every PR still approved by a human who no longer reads the diff.

### Can AI review the code? (Slides 19–30)

He took the common complaint head on: AI review gives 15 findings, 12 are noise, and you research each one to find the 3 that matter. Run it twice and you get different answers. But, he said, we were never good at reviewing either. The SmartBear study of Cisco’s reviews found defect detection falls off past about 400 lines and after about 60 minutes, and his team’s median AI-generated PR is 640 lines. Review the same PR twice yourself and you will leave different comments; humans are not deterministic reviewers either.

![Slide 22: Humans hit the same wall: 400 lines before defect detection falls off, 60 minutes before attention falls off, 640 lines in our median AI-generated PR. SmartBear, Cisco code review study, 2006, 2,500 reviews.](../slides/how-to-kill-the-code-review/deep/s22.webp)

Slide 22. Humans hit the same wall

![Slide 24: Instead, we built review theater: a loop of agent writes, AI reviews, agent revises, AI reviews again, then a human skims and merges.](../slides/how-to-kill-the-code-review/deep/s24.webp)

Slide 24. Review theater

The pattern he called review theater: an agent writes, an AI reviews, the agent revises, the AI reviews again, and a human skims and merges. Humans are still in the loop but no longer doing what the loop was for. His case for and against AI as the reviewer:

| The case for AI review                                   | The case against                           |
|----------------------------------------------------------|--------------------------------------------|
| It never gets tired or rushed                            | It never saw what was decided              |
| It reads every line, every time, even a 10,000-line diff | It was trained on the code it is reviewing |
| Same standard on every PR, from a senior or a new hire   | It will never tell you not to build it     |
| It is awake at 3am                                       | It cannot be accountable                   |

The biggest gap is that a diff cannot show what was decided, or what was deliberately not decided. Teams have done the opposite of what they should: handed judgment to the machine while spending human toil on line-by-line reading that no longer scales. He acknowledged the other side with Wealthfront Engineering’s position that it has no interest in removing human review as a bottleneck, and said they are right, because the replacement does not exist yet: today teams either review everything or rubber stamp.

![Slide 25: Can AI genuinely review code well? Case for: it never gets tired or rushed, reads every line every time, same standard on every PR, awake at 3am. Case against: it never saw what was decided, was trained on the code it is reviewing, will never tell you not to build it, cannot be accountable.](../slides/how-to-kill-the-code-review/deep/s25.webp)

Slide 25. Can AI genuinely review code well?

![Slide 29: Not everyone agrees. Quote: In the era of AI coding, human review is being scrutinized as a bottleneck to writing software. While that may be true, we have no current interest in removing that bottleneck. Wealthfront Engineering, 3 Aug 2026.](../slides/how-to-kill-the-code-review/deep/s29.webp)

Slide 29. Not everyone agrees

### The framework: the new shape of review (Slides 33–34)

The six verbs keep the essay’s concepts in a different order and add the missing human layer. The bottom row of each box on slide 34 names the job review used to do that the verb takes over, which is the clearest single slide in the deck.

![Slide 34: The new shape of review: six boxes. Argue, adversarial review, alternative solutions. Capture, intent plus criteria, knowledge transfer. Codify, the slop register, consistency. Prove, evidence per criterion, finding defects. Debate, the decisions, not in the essay. Own, the signature, gatekeeping.](../slides/how-to-kill-the-code-review/deep/s34.webp)

Slide 34. The new shape of review

| Verb    | What it is                                                  | Old job of review it takes over | Who does it                             |
|---------|-------------------------------------------------------------|---------------------------------|-----------------------------------------|
| Argue   | Adversarial review between agents before the PR exists      | Alternative solutions           | Agents; humans settle what they can’t   |
| Capture | Intent and acceptance criteria, from the session, on the PR | Knowledge transfer              | Agent drafts, author corrects           |
| Codify  | The slop register: repeated comments as invariants          | Consistency                     | Checks and agents, rules owned by teams |
| Prove   | Evidence per criterion                                      | Finding defects                 | Agents in a preview environment         |
| Debate  | Humans on the decisions                                     | Not in the March essay          | Author, reviewer and team               |
| Own     | The signature: who owns the rules                           | Gatekeeping                     | The team                                |

![The new shape of review: six verbs](../diagrams/how-to-kill-the-code-review-1.svg)

Our drawing of slides 34 and 92: who does the work at each step.

### 1. Argue: let the agents argue before the PR exists (Slides 35–41)

If a coding agent and a review agent are talking to each other, he asked, why do it in the PR interface at all? Run them locally before the PR is created and let them argue. Then, instead of reading 4,000 lines, read what they disagreed about. Slide 38 shows a real list: whether to block a whole batch when a listed check fails or only warn on reported checks (decided by the agents, with a reason), public docs for a new config key (won’t fix, with a reason), renaming the config key (follow-up ticket), and the one call a human made.

![Slide 38: What the agents argued about. Disagreement and how it settled: block the whole batch when a listed check fails or warn on reported checks only, decided by the agents with a reason; public docs for the new config key, won't fix with a reason; rename the config key, follow-up ticket; the one call a human made.](../slides/how-to-kill-the-code-review/deep/s38.webp)

Slide 38. What the agents argued about

![Slide 41: You can do this today: run two reviewers, different models; write a Skill that captures the disagreements; review that as part of the PR.](../slides/how-to-kill-the-code-review/deep/s41.webp)

Slide 41. You can do this today (Argue)

The layer’s rule is “capture the decisions, not the verdict”. What the agents resolved matters less than seeing which decisions they made; what they could not settle is what humans debate. That gives a reviewer a much smaller surface. His homework: run two reviewers on different models, write a skill that captures the disagreements, and put that on the pull request. Nothing in the human workflow changes.

### 2. Capture: the what and the why (Slides 42–48)

The popular answer to “what are we building” is to write the spec up front. He said specs fail for three reasons: they take time teams no longer have, there is no feedback loop, and the implementation drifts away from them. Without a loop that keeps specs true, that is the waterfall model discarded twenty years ago. A few organizations make spec-driven development work, he said, only because they built those feedback loops.

![Slide 44: Why specs fail? Requires time. There's no feedback loop. The implementation drifts. That's the waterfall model we discarded 20 years ago.](../slides/how-to-kill-the-code-review/deep/s44.webp)

Slide 44. Why specs fail

![Slide 45: What can replace spec? Intent: why are we making this change? Acceptance criteria: how should it behave? Works for a 1-line bug fix and for a 1000-lines feature.](../slides/how-to-kill-the-code-review/deep/s45.webp)

Slide 45. What can replace spec?

What replaces the spec is two lighter things. Intent: why are we making this change? Acceptance criteria: how should it behave? Each needs the other, because intent without criteria can’t be checked and criteria without intent can’t be judged. Neither is new; both come from behavior-driven development. They work for a one-line bug fix and a thousand-line feature.

Teams already produce both. The prompt that starts a session is the intent, and every time the agent stops to ask a question, or the engineer explains a behavior, an acceptance criterion is being written. Slide 46 shows this in a Claude Code session: “add a rate limit to the exports endpoint” is the intent, and “use the existing RateLimiter util”, “skip the auth, middleware handles /api/v2” and “use the Money type, not float” are criteria, each marked as a decision. Then the session ends and it is all thrown away. His second homework: a skill of fewer than 50 lines that writes intent and criteria into the pull request, so the reviewer reads what you decided without anyone changing how they review.

![Slide 46: Where do these live? A Claude Code session in exports-service: add a rate limit to the exports endpoint (intent); use the existing RateLimiter util, skip the auth since middleware handles /api/v2, use the Money type not float (acceptance criteria, marked DECISION).](../slides/how-to-kill-the-code-review/deep/s46.webp)

Slide 46. Where do these live?

![Slide 47: And we throw these away when the session ends, on a light slide.](../slides/how-to-kill-the-code-review/deep/s47.webp)

Slide 47. We throw these away

### 3. Codify: the AI slop register (Slides 49–58)

There are two kinds of review comment: “have you considered doing this differently?” and “use the Money type, not float”. Only the first needs human judgment. He walked through one of his own PRs, \#11318, which had fourteen threads: eight from a bot with one real bug, three rules he had already written on other PRs (one was to raise a retryable GraphQL exception so Celery retries), one nit, and two actual decisions. Teams post the same comments over and over; those belong in a register.

![Slide 51: What one of my reviews contained: PR \#11318, require /aviator revise at the start of a comment to trigger editing. Fourteen threads, bot and me, tagged NOISE, BUG, NIT, RULE and DECISION, for example: query hardcodes first 100, no pagination (noise); .delay() is duplicated in try and except (bug); use GraphQLRetryableException so Celery retries on it (rule); no comments extracted, tell the user on the PR? (decision).](../slides/how-to-kill-the-code-review/deep/s51.webp)

Slide 51. What one of my reviews contained

![Slide 52: Fourteen threads: 8 bot threads, 1 real bug; 3 rules I'd written on other PRs; 2 actual decisions.](../slides/how-to-kill-the-code-review/deep/s52.webp)

Slide 52. Fourteen threads

Putting rules in an agent instruction file is not enough, he said, because agents are non-deterministic, can ignore rules, and follow them less reliably as context grows. A register verified by a separate system creates back pressure. He calls each rule an invariant: a standing rule checked on every change, not remembered but enforced, like a smarter linter. Examples: the Money type for anything with a currency, no direct writes to the users table, structured logger only, and every error path emits a counter. Some become scripts; some still need an agent to judge.

![Slide 56: We mined a year of our comments: 11,400 review comments mined, 212 candidate rules, 64 invariants we kept. Reduce, extract, distill.](../slides/how-to-kill-the-code-review/deep/s56.webp)

Slide 56. We mined a year of comments

![Slide 57: An invariant, defined. Rule: every config change writes an audit-log entry, only when something changed. Scope: mutations and API handlers that write repo or account config. Verified by: save twice, read the audit log. Provenance: mined from 23 review threads across 17 PRs. Owner: platform team.](../slides/how-to-kill-the-code-review/deep/s57.webp)

Slide 57. An invariant, defined

| Field       | Example on slide 57                                                        | Why it is there                                                                                            |
|-------------|----------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------|
| Rule        | Every config change writes an audit-log entry, only when something changed | What is being enforced                                                                                     |
| Scope       | Mutations and API handlers that write repo or account config               | Which changes it applies to, so a frontend rule doesn’t run on a backend change and waste time and compute |
| Verified by | Save twice, read the audit log                                             | A script, an agent, or a code search                                                                       |
| Provenance  | Mined from 23 review threads across 17 PRs                                 | Why the rule exists, so it can be maintained                                                               |
| Owner       | Platform team                                                              | No rule survives without a team that wants it                                                              |

In the last year his team mined 11,400 review comments, found 212 candidate rules and kept 64. In Q&A he added that rules live in the repo so coding agents can browse them like code, that scopes (including ast-grep-based ones) keep each change to the rules that apply, that rules are independent so CI can split them across calls, and that a rule must always have a yes or no answer. The hard part is not generating rules, which an agent can do in one pass over your comments, but reading them and agreeing with them.

**Takeaway.** “Every review comment your team repeats is a guardrail you haven’t written.” This is the most copyable idea in the talk and needs no vendor.

### 4. Prove: evidence, not a green check (Slides 59–63)

A green CI check might mean no bugs, but it says nothing about behavior, especially when the same agent wrote the code and the tests. To prove a criterion: plan (each criterion becomes a scenario), spin up a preview environment from the PR, drive it (an agent clicks, calls and watches), and capture screenshots, requests, responses and logs. He pointed to a recent Addy Osmani post on how teams run this kind of verification.

![Slide 61: How to prove a criterion: 1 plan, each criterion becomes a scenario; 2 spin up a preview environment from the PR; 3 drive, an agent clicks, calls and watches; 4 capture screenshots, requests, responses, logs.](../slides/how-to-kill-the-code-review/deep/s61.webp)

Slide 61. How to prove a criterion

![Slide 62: Every criterion, its own proof: what the user sees, screenshot and DOM snapshot; an API contract, recorded request and response; side effects, network requests, server logs, DB state; a code rule, ast-grep match or a file:line citation; behavior over time, a test run and its trace.](../slides/how-to-kill-the-code-review/deep/s62.webp)

Slide 62. Every criterion, its own proof

| Criterion is about | Proven by                                     |
|--------------------|-----------------------------------------------|
| What the user sees | Screenshot, DOM snapshot                      |
| An API contract    | Recorded request and response                 |
| Side effects       | Network requests, server logs, database state |
| A code rule        | ast-grep match, or a file and line citation   |
| Behavior over time | A test run and its trace                      |

The human job becomes two checks: are the criteria right, and does the evidence match them. Then the limit: verification proves what you asked, not what you forgot to ask. That is where the talk turned to humans.

### 5. Debate: humans, on the decisions (Slides 64–76)

No verification layer answers whether we are building the right thing. The part that worries him most: code review is the only scheduled moment engineers talk to each other about the system. Automate it away and you delete shared understanding. He quoted Peter Naur: the death of a program happens when the programmer team possessing its theory is dissolved. That used to happen through attrition and backfills. Stop reading the code and you get there in a month.

![Slide 67: Code review is the only scheduled moment engineers talk to each other about the system.](../slides/how-to-kill-the-code-review/deep/s67.webp)

Slide 67. The only scheduled moment

![Slide 69: Quote: The death of a program happens when the programmer team possessing its theory is dissolved. Peter Naur, 1985. Programming as Theory Building, verified verbatim.](../slides/how-to-kill-the-code-review/deep/s69.webp)

Slide 69. Naur, 1985

So keep the conversation and change what it is about: tradeoffs, defaults, rejected options and scope cuts. He separated criteria from decisions carefully, and this distinction is the core of the talk:

|           | Acceptance criteria                | Decisions                                |
|-----------|------------------------------------|------------------------------------------|
| What      | What it should do                  | The calls made getting there             |
| When      | Written while you build            | Made by you and the agents along the way |
| Judged as | Pass or fail, not subjective       | Right or wrong, for a reason             |
| For       | Machines to prove                  | Humans to debate                         |
| Example   | A 429 is retried after Retry-After | Retry 5xx, never 4xx                     |

Decisions come from four places, per the recording (only the first item was photographed): while you build, when the agent asks about some choices and makes others silently; when agents argue with each other; in software factories, where decisions get made with no human in the loop; and when verification fails and someone, agent or human, chooses whether to fix the code or change the criterion. Slide 75 shows every decision on one retry-handling PR with where it came from and how it ended:

| Decision                                     | Where it came from  | Outcome          |
|----------------------------------------------|---------------------|------------------|
| Retry 5xx and timeouts, never 4xx            | While building      | Decided          |
| Exponential backoff, capped at 10 minutes    | While building      | Decided          |
| Honor Retry-After on a 429                   | Verification failed | Fixed            |
| Deduplicate retried deliveries (idempotence) | Agents disagreed    | Needs a human    |
| Give up after 24h, mark the endpoint failing | Review              | Follow-up ticket |

![Slide 75: Every decision on that PR, with where it came from and the outcome: retry 5xx and timeouts, never 4xx, while building, decided; exponential backoff capped at 10 minutes, while building, decided; honor Retry-After on a 429, verification failed, fixed; deduplicate retried deliveries, agents disagreed, needs a human; give up after 24h and mark the endpoint failing, review, follow-up ticket.](../slides/how-to-kill-the-code-review/deep/s75.webp)

Slide 75. Every decision on that PR

![Slide 76: How you review decisions: 1 skim what's settled, the calls the agents made with their reasons; 2 settle what they couldn't, the disagreements left open; 3 reopen any call you'd make differently, never edited, only reopened; 4 talk it through with the author, that conversation is where understanding gets built.](../slides/how-to-kill-the-code-review/deep/s76.webp)

Slide 76. How you review decisions

Reviewing decisions has four steps: skim what is settled (the calls the agents made, with their reasons), settle what they couldn’t, reopen any call you would make differently (decisions are never edited, only reopened), and talk it through with the author, because that conversation is where understanding gets built. In Q&A he said much of design review can happen through these micro decisions, though large designs still belong before the code exists.

### 6. Own: accountability moves to the team (Slides 77–79)

A model has no reputation, no liability and cannot be asked why. Responsibility used to sit with the author (wrote it, owned it) and the reviewer (read it, approved it). Now it sits with the team that writes the rules that verify the code. Ownership means owning the rules that govern the code and keeping the mental model behind them, not reading line by line. In Q&A he said rules should be owned by teams, never individuals, the same way as code ownership, whether or not you run a monorepo, and enforced as CI checks whose failures the coding agent can read and fix.

![Slide 79: Responsibility moved: the author wrote it and owned it, the reviewer read it and approved it, now the team writes the rules that verify it.](../slides/how-to-kill-the-code-review/deep/s79.webp)

Slide 79. Responsibility moved

### A bad day: every filter passed it (Slides 80–86)

He showed where the system failed. A change passed the author’s agent, a cross-examination (which argued ERROR versus FAILED and optional checks), an AI review bot that commented with nothing blocking, and acceptance criteria (6 of 7 passed, 1 accepted). It ran a query on a very large table without an index and caused an incident.

![Slide 81: Every filter passed it: 1 the author's agent wrote it with an engineer; 2 cross-examination argued ERROR vs FAILED and optional checks; 3 an AI review bot commented, nothing blocking; 4 acceptance criteria, 6 of 7 passed, 1 accepted.](../slides/how-to-kill-the-code-review/deep/s81.webp)

Slide 81. Every filter passed it

![Slide 82: Why it passed: the criteria described behavior, not cost at prod scale; the preview env has none of prod's data; both agents argued semantics and neither read the query plan; one of our own rules, filter in SQL, pushed toward it.](../slides/how-to-kill-the-code-review/deep/s82.webp)

Slide 82. Why it passed

Why it passed: the criteria described behavior, not cost at production scale; the preview environment had none of production’s data; both agents argued semantics and neither read the query plan; and one of their own invariants, “filter in SQL”, pushed toward the bad query. Impact started at 6:27 PM, was identified with rollback started at 6:30, rollback completed at 6:45 and the incident was resolved at 7:02, per their status page on Oct 26, 2026. The 18 minutes in the slide title is impact to rollback complete.

![Slide 83: 18 minutes: 6:27 PM impact starts, 6:30 identified and rollback started, 6:45 rollback complete, 7:02 resolved. status.aviator.co, Oct 26, 2026, Pacific Time.](../slides/how-to-kill-the-code-review/deep/s83.webp)

Slide 83. 18 minutes

![Slide 86: Queries on large tables stay bounded by an index: the invariant, two days later. Since then: caught an unbounded subselect on a 2.9M-row table, before merge.](../slides/how-to-kill-the-code-review/deep/s86.webp)

Slide 86. The invariant, two days later

Two lessons. None of this replaces continuous delivery: small releases, feature flags and fast rollback matter more with agents, not less. And the follow-up was not “who approved it?” but “which rule was missing?”. Two days later they had an invariant that queries on large tables stay bounded by an index, which has since caught an unbounded subselect on a 2.9-million-row table before merge. He added that he does not know whether a human reviewer would have caught it either.

### A year later, and how to start (Slides 87–92)

| Measure (Aviator, 9 engineers, Nov 2025 to Nov 2026) | Before   | After |
|------------------------------------------------------|----------|-------|
| PRs merged per week                                  | 1x       | 4x    |
| Median time to merge                                 | 2.1 days | 3.4 h |
| Human threads per PR                                 | 6.2      | 1.3   |
| Reverts per quarter (slide marked placeholder)       | 10       | 6     |

All four are Aviator’s own figures for its own team. The reverts chart (slide 88) carries a visible footer reading “placeholder numbers: replace before the talk”, so the 40% reduction should not be quoted until Aviator confirms it.

![Slide 89: The first 90 days were hard: month 1, double work, reviewing code and writing invariants; month 2, invariants catch enough that reviews shrink; month 3, you read intent and evidence, not code.](../slides/how-to-kill-the-code-review/deep/s89.webp)

Slide 89. The first 90 days were hard

![Slide 91: Run a 90-day pilot: 1 prerequisites first, CI, continuous delivery, flags, fast rollback; 2 pick one team, high PR volume, mature CI; 3 baseline before day one, reverts, incidents, time to merge, reviewer load; 4 mine, codify, capture, top 20 comments become invariants, intent on every PR; 5 decide at day 90 against kill criteria you wrote down up front.](../slides/how-to-kill-the-code-review/deep/s91.webp)

Slide 91. Run a 90-day pilot

The first 90 days were hard. Month one was double work: reviewing code and writing invariants. In month two, invariants caught enough that reviews shrank. By month three they read intent and evidence, not code. Their time now goes to refining invariants (tighten scope, retire noisy ones, promote stable ones), debating decisions, and improving verification (better scenarios, better evidence, faster preview environments).

His pilot plan: prerequisites first (CI, continuous delivery, flags, fast rollback); pick one team with high PR volume and mature CI; baseline reverts, incidents, time to merge and reviewer load before day one; mine and codify the top 20 comments as invariants and capture intent on every PR; then decide at day 90 against kill criteria written down up front. At scale: a named team owns each invariant and retires noisy ones; when two teams’ rules conflict, the team that owns the code path decides and the rule records why; auth, payments, migrations and infrastructure still get line-by-line review; and the approver signs the intent, the decisions and the evidence, not the diff.

![Slide 92: What changes at scale. Who owns an invariant? A team, named on the rule; it retires the noisy ones. Two teams' rules conflict? The team that owns the code path decides; the rule records why. What still gets line-by-line review? Auth, payments, migrations, infra. What does the approver sign? The intent, the decisions and the evidence, not the diff.](../slides/how-to-kill-the-code-review/deep/s92.webp)

Slide 92. What changes at scale

### Homework (Slides 93–98)

“Kill the line-by-line review theater”, not the review. AI is good at finding bugs, probably better than humans; humans are good at judgment. Six things to do:

1.  Run a second reviewer on a different model, before the PR exists. The slide notes PR-Agent is MIT-licensed and free.
2.  Write down what they settled: intent and acceptance criteria, on the PR.
3.  Harvest your last 1,000 review comments; the top 20 become invariants.
4.  Ask for evidence, not a green check: a screenshot, a request or a log per criterion.
5.  Change what the conversation is about: decisions, not the diff.
6.  Define ownership of rules, and what ownership now means.

![Slide 96: Six verbs, six things: 1 run a second reviewer, different model, PR-Agent is MIT and free; 2 write down what they settled, intent and acceptance criteria on the PR; 3 harvest your last 1000 review comments, the top 20 become invariants; 4 ask for evidence, not a green check, a screenshot, a request, a log per criterion; 5 change what the conversation is about, decisions, not the diff; 6 define ownership of rules and what ownership now means.](../slides/how-to-kill-the-code-review/deep/s96.webp)

Slide 96. Six verbs, six things

![Slide 97: Work on the tools and culture together: build tools to push decisions to the same PR; have a conversation with the team to change behavior; define guardrails to build the trust.](../slides/how-to-kill-the-code-review/deep/s97.webp)

Slide 97. Tools and culture together

Work on tools and culture together: build tools that push decisions onto the same PR, talk with the team to change behavior, and define guardrails to build trust. He closed with a line Andrej Karpathy has been citing: you can outsource your thinking, but you can’t outsource your understanding.

## The essays, docs and repos behind it

The talk is the latest step in a series Ankit has published since March. Reading them in order shows how the framework moved, and the product docs show how Aviator implements each verb. All of these are by Ankit or Aviator; several New Stack pieces are labelled as sponsored by Aviator.

| Date                  | Piece                                                                                                                                                                       | What it added                                                                                                                                                                                                                           |
|-----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Mar 3, 2026           | [How to Kill the Code Review](https://latent.space/p/reviews-dead) (Latent Space)                                                                                           | “Human-written code died in 2025, code reviews will die in 2026.” Five Swiss cheese layers; specs become the source of truth and you review steps, rules and contracts instead of code.                                                 |
| Jun 2, 2026           | [AI killed the code review. What happens to knowledge sharing?](https://www.cio.com/article/4179485/ai-killed-the-code-review-what-happens-to-knowledge-sharing.html) (CIO) | First turn toward the human side: much of review’s knowledge sharing was incidental, so decisions have to be reviewable on their own.                                                                                                   |
| Jun 29 to Jul 2, 2026 | [AI Engineer World’s Fair talk](https://ai.engineer/talks/how-to-kill-the-code-review)                                                                                      | Review has two jobs, semantic accuracy and alignment; the AI slop register; keep prompts and sessions as decision records.                                                                                                              |
| Jul 7, 2026           | [How to kill the code review](https://thenewstack.io/killing-the-code-review/) (The New Stack)                                                                              | Two layers: invariants and verified intent. “Deterministic where you can, LLM where you must.” Build the register first; don’t kill review on day one.                                                                                  |
| Sep 30, 2026          | [Kill the code review theater, keep the review](https://thenewstack.io/kill-code-review-theater/) (The New Stack)                                                           | “Six months ago I … was wrong.” Argue, Capture, Codify, Debate, Own. Most of today’s opening section, nearly word for word.                                                                                                             |
| Oct 20, 2026          | [We stopped reviewing code and started verifying intent](https://tessl.io/blog/we-stopped-reviewing-code-and-started-verifying-intent) (Tessl, AI Native DevCon)            | The five verbs as a workflow: argue before the PR, capture intent and criteria, codify comments, debate decisions, own the rules.                                                                                                       |
| After Sep 30, 2026    | [How to review AI code without reading the code](https://thenewstack.io/review-decisions-not-code) (The New Stack)                                                          | Decisions as threads, with humans and agents labelled separately; a reviewer can agree, challenge, override or make a decision a follow-up; decisions outlive the merge as memory for agents, so they don’t re-argue settled tradeoffs. |
| Nov 18, 2026          | This talk                                                                                                                                                                   | Adds Prove as its own verb (six, not five), the incident, a year of team numbers and the 90-day pilot.                                                                                                                                  |

### How Aviator Verify implements it

The [Verify docs](https://docs.aviator.co/verify/how-it-works) map closely onto the talk. A coding agent submits an intent and acceptance criteria generated from the session. Aviator turns that into a runbook, generates scenarios, runs them against a live preview of the change, and posts a verdict per criterion with evidence on the PR. Invariants live in a per-account catalog and are applied as extra criteria tagged `baseline_invariant`.

| Talk concept               | In the Verify docs                                                                                                                                                                                                                                                          |
|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Invariant fields           | Rule (one sentence stating the requirement, not the fix), scope conditions (file path glob, language), owner team, one of nine categories, enabled toggle                                                                                                                   |
| Where rules come from      | Manual, a starter template library, AI-drafted from repo signals, extracted from docs such as CONTRIBUTING.md, mined from recurring PR comments, or an `@aviator invariant` comment in GitHub or Slack. Anything not written by hand is a draft until an owner approves it. |
| Applying rules to a change | A selector filters by scope, then an LLM reads the intent, criteria and change set and picks the invariants that clearly fit                                                                                                                                                |
| Disagreeing with a rule    | Four waiver types recorded in an audit trail: false positive, doesn’t apply, accepted risk, fix in follow-up. Repeated waivers signal a rule needs rewording.                                                                                                               |
| Capture from the session   | A `/verify-submit` skill and hook run before the agent opens a PR; the engineer reviews the extracted intent and criteria first                                                                                                                                             |

Docs read Nov 18, 2026. Verify is a hosted service at app.aviator.co; we did not trial it.

### Repos

| Repo                                                                    | License       | What it is                                                                                                                                                                                                                                                                                               |
|-------------------------------------------------------------------------|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [aviator-co/agent-plugins](https://github.com/aviator-co/agent-plugins) | MIT           | Claude Code plugin marketplace. The `aviator` plugin adds `/verify-submit` (submit intent and criteria for code you wrote) and `/create-runbook` (Aviator’s agent writes code from a spec); `av-cli` teaches agents the stacked-PR CLI. Needs an Aviator account and connected repo. 11 stars when read. |
| [aviator-co/av](https://github.com/aviator-co/av)                       | MIT           | Go CLI for stacked pull requests: PRs that build on PRs, rebased automatically when a base changes. About 500 stars.                                                                                                                                                                                     |
| [The-PR-Agent/pr-agent](https://github.com/The-PR-Agent/pr-agent)       | MIT on GitHub | The open-source AI PR reviewer Ankit recommended as the second reviewer. Created by Qodo (CodiumAI) and handed to a community GitHub organization in April 2026. Runs as a GitHub Action, CLI or webhook, with your own model keys. About 13.6k stars.                                                   |

PR-Agent’s license has moved: GitHub showed MIT on Nov 18, while Qodo’s April 2026 handover post said the project was returning to Apache 2.0. Both are permissive; confirm the LICENSE file before any use.

### Papers and reports

- [Bacchelli and Bird, Expectations, Outcomes, and Challenges of Modern Code Review](https://doi.org/10.1109/ICSE.2013.6606617), ICSE 2013. The source of the 44% and 14%; its broader finding is that review delivers knowledge transfer, team awareness and alternative solutions more than defects.
- [Sadowski et al., Modern Code Review: A Case Study at Google](https://research.google/pubs/modern-code-review-a-case-study-at-google/), ICSE-SEIP 2018. The 9 million reviewed changes.
- [SmartBear, best practices from the Cisco study](https://smartbear.com/learn/code-review/best-practices-for-peer-code-review/): 2,500 reviews of 3.2 million lines over ten months in 2006; review under 400 lines and under 60 minutes at a time.
- Peter Naur, [Programming as Theory Building](https://en.wikipedia.org/wiki/Peter_Naur), 1985: a program is the theory in its team’s heads, and the code is a lossy record of it.
- [DORA, State of AI-assisted Software Development 2025](https://services.google.com/fh/files/misc/2025_state_of_ai_assisted_software_development.pdf): AI as an amplifier; throughput and instability both rise.
- [Faros AI, The Speed Trap](https://www.faros.ai/blog/ai-speed-trap-takeaways) (Q3 2026): 12 months of telemetry from 22,000 developers on 4,000 teams.

## Numbers we checked

Status: Checked found in the source; Caveat holds with a condition; Slide only taken from the slide, not verified.

| Claim                                                                         | Figure                                              | Source                                                                                                                                                                                                                              | Status     |
|-------------------------------------------------------------------------------|-----------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| Developers ranking finding defects as the top reason for review               | 44%                                                 | [Bacchelli and Bird 2013](https://doi.org/10.1109/ICSE.2013.6606617): 383 of 873 programmers                                                                                                                                        | Checked    |
| Classified review comments about defects                                      | 14%                                                 | Same paper: 78 of 570 comments                                                                                                                                                                                                      | Checked    |
| Reviewed changes in Google’s study                                            | 9 million                                           | [Sadowski et al. 2018](https://research.google/pubs/modern-code-review-a-case-study-at-google/)                                                                                                                                     | Checked    |
| “We made writing cheap, and understanding stayed exactly as expensive…”       | Quote                                               | [Addy Osmani, Agentic Code Review](https://addyosmani.com/blog/agentic-code-review/), Jun 15, 2026                                                                                                                                  | Checked    |
| PRs merged with no review                                                     | +76%                                                | [Faros, The Speed Trap](https://www.faros.ai/blog/ai-speed-trap-takeaways): 76.3%, up from a 31.3% rise six months earlier. Vendor telemetry; a relative increase, not a share of PRs, though Ankit said “over 75% of PRs” on stage | Caveat     |
| Average PR size                                                               | +72%                                                | Faros: 71.8%                                                                                                                                                                                                                        | Checked    |
| Work restarts                                                                 | +67%                                                | Faros: 66.7%                                                                                                                                                                                                                        | Checked    |
| Incidents per month                                                           | +125%                                               | Faros: 125.4%; incidents per PR rose 14.5% in the same report                                                                                                                                                                       | Checked    |
| AI raises throughput and instability                                          | Finding                                             | [DORA 2025](https://dora.dev/insights/balancing-ai-tensions/); survey of nearly 5,000 professionals                                                                                                                                 | Checked    |
| Devs “overloaded by AI slop PRs”                                              | Quote                                               | [The Pragmatic Engineer, The Pulse](https://blog.pragmaticengineer.com/the-pulse-new-trend-concern-about-massive-increase-in-code-review-load/); wording matches, Jul 23 date from the slide                                        | Checked    |
| r/ExperiencedDevs “won’t be reviewing AI generated PRs” post                  | 1.9K upvotes, 442 comments                          | Slide screenshot; post not found                                                                                                                                                                                                    | Slide only |
| Defect detection limits                                                       | 400 lines, 60 min                                   | [SmartBear / Cisco, 2006](https://smartbear.com/learn/code-review/best-practices-for-peer-code-review/), 2,500 reviews. SmartBear’s guidance is 200 to 400 lines and 60 to 90 minutes                                               | Caveat     |
| Aviator’s median AI-generated PR                                              | 640 lines                                           | Aviator’s own data                                                                                                                                                                                                                  | Slide only |
| AI review noise                                                               | 15 findings, 12 noise                               | Illustrative, no source given                                                                                                                                                                                                       | Slide only |
| Wealthfront has no interest in removing review as a bottleneck                | Quote                                               | [Wealthfront, Experiments with AI Code Review](https://eng.wealthfront.com/2026/08/03/experiments-with-ai-code-review/), Aug 3, 2026; post confirmed, exact wording not found in our read                                           | Caveat     |
| Aviator team, a year apart                                                    | 4x PRs/week, 9 engineers                            | Aviator’s own data                                                                                                                                                                                                                  | Slide only |
| PR \#11318 threads                                                            | 14: 8 bot (1 real bug), 3 rules, 1 nit, 2 decisions | Aviator’s own PR. Our count of slide 51 rows: 8 bot plus 6 by Ankit = 14                                                                                                                                                            | Slide only |
| Comment mining                                                                | 11,400 → 212 → 64                                   | Aviator’s own data; the recording said “over 11,000” and “200 plus”                                                                                                                                                                 | Slide only |
| Incident timeline                                                             | 18 minutes                                          | Slide citing status.aviator.co, Oct 26, 2026. Our arithmetic: 6:27 to 6:45 rollback complete is 18 minutes; resolved at 7:02, 35 minutes after impact                                                                               | Caveat     |
| Median time to merge                                                          | 3.4 h, was 2.1 days                                 | Aviator’s own data. 2.1 days is 50.4 hours, so about 15x faster                                                                                                                                                                     | Slide only |
| Human threads per PR                                                          | 1.3, was 6.2                                        | Aviator’s own data; a 79% drop                                                                                                                                                                                                      | Slide only |
| Reverts                                                                       | −40% (10 → 6 a quarter)                             | Arithmetic holds, but the slide footer reads “placeholder numbers: replace before the talk”. The recording also said 10 down to 6                                                                                                   | Caveat     |
| Naur: “The death of a program happens when…”                                  | Quote                                               | Programming as Theory Building, 1985; matches the published text                                                                                                                                                                    | Checked    |
| “You can outsource your thinking, but you can’t outsource your understanding” | Quote                                               | [Karpathy, Apr 30, 2026](https://x.com/karpathy/status/2049907410303865030), quoting an earlier post by @yacineMTB; Karpathy cites it, he did not coin it                                                                           | Caveat     |
| PR-Agent is MIT and free                                                      | License                                             | GitHub showed MIT on Nov 18; Qodo’s April 2026 post said Apache 2.0                                                                                                                                                                 | Caveat     |

## About the speaker

Ankit Jain is co-founder and CEO of [Aviator](https://www.aviator.co), a developer productivity company he started in 2021 with Spriha Tucker. Aviator went through Y Combinator’s Summer 2021 batch, announced a \$2.3 million seed round in 2022, and says it serves more than 1,000 teams. Its tools include stacked PRs, review routing and a merge queue; its focus this year is Verify, which checks AI-written changes against intent, acceptance criteria and team invariants. He previously worked at Shippo. He leads [The Hangar](https://dx.community), an Aviator-run community of senior engineers focused on developer experience, and Xoogler, the ex-Google alumni network.

He hosted the Engineering the Developer Experience track and gave the last talk on it. Earlier versions of this talk ran at the AI Engineer World’s Fair and LeadDev, and he has written about it for Latent Space, CIO and The New Stack. The vendor angle is direct: Aviator Verify sells most of what the talk describes. His homework, though, can be done without it.

## Terms and technologies

### Code review and its research

[Modern code review](https://en.wikipedia.org/wiki/Code_review)  
Lightweight, tool-based, asynchronous review of each change before merge, as in GitHub pull requests. The Microsoft and Google studies Ankit cited are the standard research on why teams do it.

[Mental model](https://en.wikipedia.org/wiki/Mental_model)  
A person’s internal picture of how a system works. Ankit’s claim is that building shared mental models, not finding bugs, is review’s main output.

[Programming as theory building](https://en.wikipedia.org/wiki/Peter_Naur)  
Peter Naur’s 1985 essay: a program is the theory its team holds, and it dies when that team disperses. Ankit used it to argue that skipping review kills that theory in months.

Review theater  
Ankit’s term for review that looks like scrutiny but isn’t: agents write and review in a loop, and a person skims and approves.

[Swiss cheese model](https://en.wikipedia.org/wiki/Swiss_cheese_model)  
A safety model where several imperfect layers stop failures that slip through any one of them. The March essay’s five layers were drawn as cheese slices.

[Agentic code review](https://addyosmani.com/blog/agentic-code-review/)  
Addy Osmani’s June 2026 post on reviewing agent-written changes: tier review by risk, gate on evidence, scrutinize test edits, keep CI strict and keep a human owner for each merge.

### Intent, criteria and decisions

[Acceptance criteria](https://en.wikipedia.org/wiki/Acceptance_testing)  
Pass or fail statements of how a change should behave. In the talk they are captured from the coding session and proven by agents, and differ from decisions, which humans debate.

[Behavior-driven development](https://en.wikipedia.org/wiki/Behavior-driven_development)  
A 2000s practice of describing behavior as examples agreed before coding, often in [Gherkin](https://cucumber.io/docs/gherkin/). Ankit said intent and criteria are BDD ideas that agents finally make cheap.

[Waterfall model](https://en.wikipedia.org/wiki/Waterfall_model)  
Sequential delivery with full specs before code. Ankit’s warning about writing big specs up front with no feedback loop.

[Architecture decision record](https://adr.github.io)  
A short record of a decision, its context and consequences, from [Michael Nygard’s 2011 post](https://www.cognitect.com/blog/2011/11/15/documenting-architecture-decisions); [MADR](https://adr.github.io/madr/) is a common Markdown template. Ankit’s PR decisions are much smaller, but the idea is the same.

### Rules and verification

[Invariant](https://docs.aviator.co/verify/concepts/invariants)  
In Ankit’s usage, a team rule every matching change must respect, with a rule, scope, verification method, provenance and owner, checked by a system separate from the coding agent.

AI slop register  
Aviator’s name for the running list of invariants: the patterns a team keeps correcting in AI-written code.

[Linter](https://en.wikipedia.org/wiki/Lint_(software))  
A static checker for code patterns. Ankit described invariants as smarter linters run on every change.

[ast-grep](https://ast-grep.github.io)  
An open-source (MIT) CLI for structural code search, linting and rewriting over syntax trees. Named as evidence for code rules and for scoping which invariants apply.

[DOM snapshot](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model)  
A saved copy of a web page’s document tree, used as evidence for what a user sees.

[Query plan](https://en.wikipedia.org/wiki/Query_plan)  
The steps a database will take to run a query, including whether it uses an [index](https://en.wikipedia.org/wiki/Database_index). Neither agent read it in the incident.

[Money type](https://martinfowler.com/eaaCatalog/money.html)  
A value type pairing an amount and currency, so money isn’t a floating-point number. Ankit’s standard example of a comment that should be a rule.

[Counter metric](https://prometheus.io/docs/concepts/metric_types/#counter)  
A metric that only goes up, such as errors seen. One of Aviator’s invariants is that every error path emits one.

### Agents and tools

[Claude Code](https://code.claude.com/docs/en/overview)  
Anthropic’s coding agent. Slide 46 shows intent and criteria arising in a Claude Code session.

[Agent skills](https://code.claude.com/docs/en/skills) and [hooks](https://code.claude.com/docs/en/hooks)  
Packaged instructions an agent loads on demand, and commands that run at fixed points such as before a tool call. Ankit’s homework is a skill to capture disagreements and another to publish intent and criteria; Aviator uses both.

[PR-Agent](https://github.com/The-PR-Agent/pr-agent)  
An open-source AI pull request reviewer, originally from Qodo, now community-run. Ankit’s suggestion for a free second reviewer.

[Aviator Verify](https://docs.aviator.co/verify/how-it-works)  
Aviator’s hosted service that verifies a PR against its intent, acceptance criteria and team invariants in a preview environment and attaches evidence.

[Stacked pull requests](https://github.com/aviator-co/av)  
Splitting a large change into a chain of small dependent PRs. Aviator’s open-source `av` CLI manages them.

[Monorepo](https://en.wikipedia.org/wiki/Monorepo)  
One repository for many projects. Asked in Q&A whether central rules imply a monorepo, Ankit said no: own rules per team as you own code.

[CODEOWNERS](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners)  
GitHub’s file mapping paths to owning teams. Not named in the talk, but an obvious place to start rule ownership.

### Delivery and HTTP

[Continuous delivery](https://en.wikipedia.org/wiki/Continuous_delivery)  
Keeping software releasable at all times with small, frequent releases. Ankit’s prerequisite before any of this.

[Feature flags](https://martinfowler.com/articles/feature-toggles.html)  
Switches that change behavior without a deploy, used for gradual rollout and fast rollback.

[HTTP 429](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/429)  
Too Many Requests. The example criterion: a 429 is retried after the server’s wait time.

[Retry-After](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Retry-After)  
The response header telling a client how long to wait before retrying.

[Exponential backoff](https://en.wikipedia.org/wiki/Exponential_backoff)  
Waiting longer after each failed retry. One of the decisions on slide 75, capped at 10 minutes.

[Idempotence](https://en.wikipedia.org/wiki/Idempotence)  
An operation that is safe to repeat. “Deduplicate retried deliveries” is the decision the agents couldn’t settle on slide 75.

[GraphQL](https://graphql.org) and [Celery](https://docs.celeryq.dev)  
The API query language and Python task queue in Ankit’s example PR, where a repeated rule was to raise a retryable GraphQL exception so Celery retries the task.

### Sources and communities

[Faros AI](https://www.faros.ai/blog/ai-speed-trap-takeaways)  
An engineering analytics vendor whose quarterly reports use telemetry from customer systems. Source of the four “we already have” figures.

[DORA](https://dora.dev)  
Google Cloud’s DevOps Research and Assessment program; its 2025 report covered AI-assisted development.

[Wealthfront Engineering](https://eng.wealthfront.com/2026/08/03/experiments-with-ai-code-review/)  
A fintech that built its own AI review harness and chose to keep human review. Ankit’s counterpoint.

[The Hangar (Hangar DX)](https://dx.community)  
Aviator’s invite-only community for senior engineers on developer experience, with a podcast, Slack and virtual meetups.

[Karpathy’s understanding line](https://x.com/karpathy/status/2049907410303865030)  
A post Andrej Karpathy has cited repeatedly this year. Ankit’s closing slide.

## Reading and tools

### Read first

- [Kill the code review theater, keep the review](https://thenewstack.io/kill-code-review-theater/): the written version of the first half of the talk.
- [How to review AI code without reading the code](https://thenewstack.io/review-decisions-not-code): the decisions idea in more depth, including decisions as agent memory after merge.
- [How to Kill the Code Review](https://latent.space/p/reviews-dead), the March essay, to see what changed.
- [Aviator docs: Invariants](https://docs.aviator.co/verify/concepts/invariants) and [How it works](https://docs.aviator.co/verify/how-it-works): the clearest written model of an invariant register.

### Tools named

- [PR-Agent](https://github.com/The-PR-Agent/pr-agent), the open-source second reviewer.
- [aviator-co/agent-plugins](https://github.com/aviator-co/agent-plugins), for the shape of a capture skill and hook.
- [ast-grep](https://ast-grep.github.io), for deterministic code rules.

### Related sessions

- Same track, earlier today: Kent Beck, [Features With Futures](https://qconsf.com/presentation/nov2026/features-futures); Adam Bender (Google), [No More Small Systems](https://qconsf.com/presentation/nov2026/no-more-small-systems-how-ai-may-bring-large-system-problems-everyone); Adam Berry (Netflix), [Growing Engineers in the Era of Agentic Coding](https://qconsf.com/presentation/nov2026/growing-engineers-era-agentic-coding); Margaret-Anne Storey, [Shipping Faster, Understanding Less](https://qconsf.com/presentation/nov2026/shipping-faster-understanding-less).
- From my notes this week: Atomic’s “Wait, You’re Still Doing PRs?” records each change against an intent; Roblox built AI review from its own review history; Forter reviews plain-English behavior tests instead of diffs; Netflix records one way to do each thing in the repo.
- Still ahead: none. This was the last session on the track, and the conference talks end today; Thursday and Friday are workshops.

## All slides

[![Slide 1: How to kill the code review. The gate is still there, it just isn&#x27;t stopping anything. Ankit Jain, Aviator.](../slides/how-to-kill-the-code-review/deep/s01.webp)](../slides/how-to-kill-the-code-review/deep/s01.webp)

Slide 1. Title

[![Slide 2: I&#x27;m going to argue we should kill the code review. I run a company that sells the replacement. So be suspicious of me.](../slides/how-to-kill-the-code-review/deep/s02.webp)](../slides/how-to-kill-the-code-review/deep/s02.webp)

Slide 2. Be suspicious of me

[![Slide 3: Code reviews are dead: the How to Kill the Code Review diagram of five Swiss cheese slices (compare multiple options, deterministic guardrails, acceptance criteria, permission systems, adversarial verification) between specs plus agents and the merge. latent.space/p/reviews-dead, Latent Space, March 2026.](../slides/how-to-kill-the-code-review/deep/s03.webp)](../slides/how-to-kill-the-code-review/deep/s03.webp)

Slide 3. Code reviews are dead

[![Slide 4: Five layers of trust: 1 compare multiple options, several agents try it, rank by tests, diff size, deps; 2 deterministic guardrails, linters, types, contracts, facts not opinions; 3 humans define acceptance criteria, written upstream before the code exists; 4 permission systems, scope what an agent may touch unattended; 5 adversarial verification, a separate agent tries to break it.](../slides/how-to-kill-the-code-review/deep/s04.webp)](../slides/how-to-kill-the-code-review/deep/s04.webp)

Slide 4. Five layers of trust

[![Slide 5: Section slide: Why do we review code.](../slides/how-to-kill-the-code-review/deep/s05.webp)](../slides/how-to-kill-the-code-review/deep/s05.webp)

Slide 5. Why do we review code

[![Slide 6: Bar chart: 44% rank finding defects as their number one reason for review; 14% of actual comments are about defects. Bacchelli and Bird, ICSE 2013, 570 comments classified.](../slides/how-to-kill-the-code-review/deep/s06.webp)](../slides/how-to-kill-the-code-review/deep/s06.webp)

Slide 6. 44% say it&#x27;s to find defects

[![Slide 7: 9,000,000 reviewed changes at Google, same finding. Sadowski et al., ICSE-SEIP 2018.](../slides/how-to-kill-the-code-review/deep/s07.webp)](../slides/how-to-kill-the-code-review/deep/s07.webp)

Slide 7. 9,000,000

[![Slide 8: Code review is not about the code.](../slides/how-to-kill-the-code-review/deep/s08.webp)](../slides/how-to-kill-the-code-review/deep/s08.webp)

Slide 8. Not about the code

[![Slide 9: Code review is to build mental models.](../slides/how-to-kill-the-code-review/deep/s09.webp)](../slides/how-to-kill-the-code-review/deep/s09.webp)

Slide 9. Mental models

[![Slide 10: Code review is for knowledge sharing, on a light slide.](../slides/how-to-kill-the-code-review/deep/s10.webp)](../slides/how-to-kill-the-code-review/deep/s10.webp)

Slide 10. Knowledge sharing

[![Slide 11: Quote: We made writing cheap, and understanding stayed exactly as expensive as it has always been. Addy Osmani, Agentic Code Review, 15 Jun 2026.](../slides/how-to-kill-the-code-review/deep/s11.webp)](../slides/how-to-kill-the-code-review/deep/s11.webp)

Slide 11. Understanding stayed expensive

[![Slide 12: Section slide: The problem. How long until we stop reading the code?](../slides/how-to-kill-the-code-review/deep/s12.webp)](../slides/how-to-kill-the-code-review/deep/s12.webp)

Slide 12. The problem

[![Slide 13: We already have: +76% PRs merged with no review at all, +72% average PR size, +67% work restarts, +125% incidents per month. Faros AI Engineering Report Q3 2026, The Speed Trap, 18 Sep 2026, 22,000 devs, 4,000 teams.](../slides/how-to-kill-the-code-review/deep/s13.webp)](../slides/how-to-kill-the-code-review/deep/s13.webp)

Slide 13. We already have

[![Slide 14: AI adoption raises delivery throughput and delivery instability at the same time. DORA, State of AI-assisted Software Development 2025.](../slides/how-to-kill-the-code-review/deep/s14.webp)](../slides/how-to-kill-the-code-review/deep/s14.webp)

Slide 14. Throughput and instability

[![Slide 15: Quote: Those devs who put the same effort and energy into code review as before feel overloaded by AI slop PRs sent their way. Gergely Orosz, The Pragmatic Engineer, 23 Jul 2026.](../slides/how-to-kill-the-code-review/deep/s15.webp)](../slides/how-to-kill-the-code-review/deep/s15.webp)

Slide 15. Overloaded by AI slop PRs

[![Slide 16: No one voted to stop reviewing code. We just stopped. Screenshot of an r/ExperiencedDevs post: Today I announced that I won&#x27;t be reviewing AI generated PRs at company meeting, 1.9K upvotes, 442 comments.](../slides/how-to-kill-the-code-review/deep/s16.webp)](../slides/how-to-kill-the-code-review/deep/s16.webp)

Slide 16. No one voted

[![Slide 17: Our team, a year apart: 4x PRs merged per week, 9 engineers both years, every PR still approved by a human. Aviator engineering, Nov 2025 to Nov 2026.](../slides/how-to-kill-the-code-review/deep/s17.webp)](../slides/how-to-kill-the-code-review/deep/s17.webp)

Slide 17. Our team, a year apart

[![Slide 18: A human still approves every PR. They just don&#x27;t read the diff anymore.](../slides/how-to-kill-the-code-review/deep/s18.webp)](../slides/how-to-kill-the-code-review/deep/s18.webp)

Slide 18. They don&#x27;t read the diff

[![Slide 19: Section slide: Can AI review the code?](../slides/how-to-kill-the-code-review/deep/s19.webp)](../slides/how-to-kill-the-code-review/deep/s19.webp)

Slide 19. Can AI review the code?

[![Slide 20: AI sucks at reviewing code: you get 15 findings, 12 are noise, now you research each one to find the 3 that matter.](../slides/how-to-kill-the-code-review/deep/s20.webp)](../slides/how-to-kill-the-code-review/deep/s20.webp)

Slide 20. AI sucks at reviewing code

[![Slide 21: But we were never that good at it either.](../slides/how-to-kill-the-code-review/deep/s21.webp)](../slides/how-to-kill-the-code-review/deep/s21.webp)

Slide 21. Never that good at it

[![Slide 22: Humans hit the same wall: 400 lines before defect detection falls off, 60 minutes before attention falls off, 640 lines in our median AI-generated PR. SmartBear, Cisco code review study, 2006, 2,500 reviews.](../slides/how-to-kill-the-code-review/deep/s22.webp)](../slides/how-to-kill-the-code-review/deep/s22.webp)

Slide 22. Humans hit the same wall

[![Slide 23: Because a diff is a bad place for review. One reviewer, reading once, from memory.](../slides/how-to-kill-the-code-review/deep/s23.webp)](../slides/how-to-kill-the-code-review/deep/s23.webp)

Slide 23. A diff is a bad place

[![Slide 24: Instead, we built review theater: a loop of agent writes, AI reviews, agent revises, AI reviews again, then a human skims and merges.](../slides/how-to-kill-the-code-review/deep/s24.webp)](../slides/how-to-kill-the-code-review/deep/s24.webp)

Slide 24. Review theater

[![Slide 25: Can AI genuinely review code well? Case for: it never gets tired or rushed, reads every line every time, same standard on every PR, awake at 3am. Case against: it never saw what was decided, was trained on the code it is reviewing, will never tell you not to build it, cannot be accountable.](../slides/how-to-kill-the-code-review/deep/s25.webp)](../slides/how-to-kill-the-code-review/deep/s25.webp)

Slide 25. Can AI genuinely review code well?

[![Slide 26: But a diff can&#x27;t tell you what was decided.](../slides/how-to-kill-the-code-review/deep/s26.webp)](../slides/how-to-kill-the-code-review/deep/s26.webp)

Slide 26. Can&#x27;t tell what was decided

[![Slide 27: Build tools for the things AI does well. Protect the things it cannot.](../slides/how-to-kill-the-code-review/deep/s27.webp)](../slides/how-to-kill-the-code-review/deep/s27.webp)

Slide 27. Build tools for what AI does well

[![Slide 28: We have been doing the exact opposite, on a light slide.](../slides/how-to-kill-the-code-review/deep/s28.webp)](../slides/how-to-kill-the-code-review/deep/s28.webp)

Slide 28. The exact opposite

[![Slide 29: Not everyone agrees. Quote: In the era of AI coding, human review is being scrutinized as a bottleneck to writing software. While that may be true, we have no current interest in removing that bottleneck. Wealthfront Engineering, 3 Aug 2026.](../slides/how-to-kill-the-code-review/deep/s29.webp)](../slides/how-to-kill-the-code-review/deep/s29.webp)

Slide 29. Not everyone agrees

[![Slide 30: They&#x27;re right. The replacement doesn&#x27;t exist yet.](../slides/how-to-kill-the-code-review/deep/s30.webp)](../slides/how-to-kill-the-code-review/deep/s30.webp)

Slide 30. They&#x27;re right

[![Slide 31: Five layers of trust, revisited: four layers answered is it right, one answered is it what we meant, none of them asked are we building the right thing.](../slides/how-to-kill-the-code-review/deep/s31.webp)](../slides/how-to-kill-the-code-review/deep/s31.webp)

Slide 31. Five layers, revisited

[![Slide 32: The structure was right. I missed the human judgment entirely.](../slides/how-to-kill-the-code-review/deep/s32.webp)](../slides/how-to-kill-the-code-review/deep/s32.webp)

Slide 32. I missed the human judgment

[![Slide 33: Section slide: The framework. Same concepts. Better order. Practical implementation.](../slides/how-to-kill-the-code-review/deep/s33.webp)](../slides/how-to-kill-the-code-review/deep/s33.webp)

Slide 33. The framework

[![Slide 34: The new shape of review: six boxes. Argue, adversarial review, alternative solutions. Capture, intent plus criteria, knowledge transfer. Codify, the slop register, consistency. Prove, evidence per criterion, finding defects. Debate, the decisions, not in the essay. Own, the signature, gatekeeping.](../slides/how-to-kill-the-code-review/deep/s34.webp)](../slides/how-to-kill-the-code-review/deep/s34.webp)

Slide 34. The new shape of review

[![Slide 35: Step 1 of 6, Argue: let the agents argue before the PR exists.](../slides/how-to-kill-the-code-review/deep/s35.webp)](../slides/how-to-kill-the-code-review/deep/s35.webp)

Slide 35. Argue

[![Slide 36: Why is there a UI for two machines talking to each other?](../slides/how-to-kill-the-code-review/deep/s36.webp)](../slides/how-to-kill-the-code-review/deep/s36.webp)

Slide 36. A UI for two machines?

[![Slide 37: Instead of reading 4000 lines, read what they disagreed about.](../slides/how-to-kill-the-code-review/deep/s37.webp)](../slides/how-to-kill-the-code-review/deep/s37.webp)

Slide 37. Read what they disagreed about

[![Slide 38: What the agents argued about. Disagreement and how it settled: block the whole batch when a listed check fails or warn on reported checks only, decided by the agents with a reason; public docs for the new config key, won&#x27;t fix with a reason; rename the config key, follow-up ticket; the one call a human made.](../slides/how-to-kill-the-code-review/deep/s38.webp)](../slides/how-to-kill-the-code-review/deep/s38.webp)

Slide 38. What the agents argued about

[![Slide 39: Layer 1, Argue: capture the decisions, not the verdict.](../slides/how-to-kill-the-code-review/deep/s39.webp)](../slides/how-to-kill-the-code-review/deep/s39.webp)

Slide 39. Capture the decisions, not the verdict

[![Slide 40: What they couldn&#x27;t settle is what you debate.](../slides/how-to-kill-the-code-review/deep/s40.webp)](../slides/how-to-kill-the-code-review/deep/s40.webp)

Slide 40. What they couldn&#x27;t settle

[![Slide 41: You can do this today: run two reviewers, different models; write a Skill that captures the disagreements; review that as part of the PR.](../slides/how-to-kill-the-code-review/deep/s41.webp)](../slides/how-to-kill-the-code-review/deep/s41.webp)

Slide 41. You can do this today (Argue)

[![Slide 42: Step 2 of 6, Capture: capture the what and the why.](../slides/how-to-kill-the-code-review/deep/s42.webp)](../slides/how-to-kill-the-code-review/deep/s42.webp)

Slide 42. Capture

[![Slide 43: The popular answer is to write the spec up front.](../slides/how-to-kill-the-code-review/deep/s43.webp)](../slides/how-to-kill-the-code-review/deep/s43.webp)

Slide 43. Write the spec up front

[![Slide 44: Why specs fail? Requires time. There&#x27;s no feedback loop. The implementation drifts. That&#x27;s the waterfall model we discarded 20 years ago.](../slides/how-to-kill-the-code-review/deep/s44.webp)](../slides/how-to-kill-the-code-review/deep/s44.webp)

Slide 44. Why specs fail

[![Slide 45: What can replace spec? Intent: why are we making this change? Acceptance criteria: how should it behave? Works for a 1-line bug fix and for a 1000-lines feature.](../slides/how-to-kill-the-code-review/deep/s45.webp)](../slides/how-to-kill-the-code-review/deep/s45.webp)

Slide 45. What can replace spec?

[![Slide 46: Where do these live? A Claude Code session in exports-service: add a rate limit to the exports endpoint (intent); use the existing RateLimiter util, skip the auth since middleware handles /api/v2, use the Money type not float (acceptance criteria, marked DECISION).](../slides/how-to-kill-the-code-review/deep/s46.webp)](../slides/how-to-kill-the-code-review/deep/s46.webp)

Slide 46. Where do these live?

[![Slide 47: And we throw these away when the session ends, on a light slide.](../slides/how-to-kill-the-code-review/deep/s47.webp)](../slides/how-to-kill-the-code-review/deep/s47.webp)

Slide 47. We throw these away

[![Slide 48: Do this today: capture intent and criteria during the session; publish them on the pull request, so the reviewer reads what you decided.](../slides/how-to-kill-the-code-review/deep/s48.webp)](../slides/how-to-kill-the-code-review/deep/s48.webp)

Slide 48. Do this today (Capture)

[![Slide 49: Step 3 of 6, Codify: turn repeated comments into deterministic rules.](../slides/how-to-kill-the-code-review/deep/s49.webp)](../slides/how-to-kill-the-code-review/deep/s49.webp)

Slide 49. Codify

[![Slide 50: Two kinds of review comment: Have you considered doing this differently? Use the Money type, not float. Only one of them needs human judgment.](../slides/how-to-kill-the-code-review/deep/s50.webp)](../slides/how-to-kill-the-code-review/deep/s50.webp)

Slide 50. Two kinds of review comment

[![Slide 51: What one of my reviews contained: PR \#11318, require /aviator revise at the start of a comment to trigger editing. Fourteen threads, bot and me, tagged NOISE, BUG, NIT, RULE and DECISION, for example: query hardcodes first 100, no pagination (noise); .delay() is duplicated in try and except (bug); use GraphQLRetryableException so Celery retries on it (rule); no comments extracted, tell the user on the PR? (decision).](../slides/how-to-kill-the-code-review/deep/s51.webp)](../slides/how-to-kill-the-code-review/deep/s51.webp)

Slide 51. What one of my reviews contained

[![Slide 52: Fourteen threads: 8 bot threads, 1 real bug; 3 rules I&#x27;d written on other PRs; 2 actual decisions.](../slides/how-to-kill-the-code-review/deep/s52.webp)](../slides/how-to-kill-the-code-review/deep/s52.webp)

Slide 52. Fourteen threads

[![Slide 53: Codify, the AI slop register: the running list of patterns your team keeps correcting.](../slides/how-to-kill-the-code-review/deep/s53.webp)](../slides/how-to-kill-the-code-review/deep/s53.webp)

Slide 53. The AI slop register

[![Slide 54: Codified as invariants: standing rules, checked on every change. Not remembered. Enforced.](../slides/how-to-kill-the-code-review/deep/s54.webp)](../slides/how-to-kill-the-code-review/deep/s54.webp)

Slide 54. Invariants

[![Slide 55: Codified as invariants: Money type for anything with a currency; no direct writes to the users table; structured logger only, no print; every error path emits a counter.](../slides/how-to-kill-the-code-review/deep/s55.webp)](../slides/how-to-kill-the-code-review/deep/s55.webp)

Slide 55. Codified as invariants

[![Slide 56: We mined a year of our comments: 11,400 review comments mined, 212 candidate rules, 64 invariants we kept. Reduce, extract, distill.](../slides/how-to-kill-the-code-review/deep/s56.webp)](../slides/how-to-kill-the-code-review/deep/s56.webp)

Slide 56. We mined a year of comments

[![Slide 57: An invariant, defined. Rule: every config change writes an audit-log entry, only when something changed. Scope: mutations and API handlers that write repo or account config. Verified by: save twice, read the audit log. Provenance: mined from 23 review threads across 17 PRs. Owner: platform team.](../slides/how-to-kill-the-code-review/deep/s57.webp)](../slides/how-to-kill-the-code-review/deep/s57.webp)

Slide 57. An invariant, defined

[![Slide 58: Every review comment your team repeats is a guardrail you haven&#x27;t written, on a light slide.](../slides/how-to-kill-the-code-review/deep/s58.webp)](../slides/how-to-kill-the-code-review/deep/s58.webp)

Slide 58. A guardrail you haven&#x27;t written

[![Slide 59: Step 4 of 6, Prove: prove it works, with evidence.](../slides/how-to-kill-the-code-review/deep/s59.webp)](../slides/how-to-kill-the-code-review/deep/s59.webp)

Slide 59. Prove

[![Slide 60: A green check might mean no bugs. It says nothing about the behavior.](../slides/how-to-kill-the-code-review/deep/s60.webp)](../slides/how-to-kill-the-code-review/deep/s60.webp)

Slide 60. A green check

[![Slide 61: How to prove a criterion: 1 plan, each criterion becomes a scenario; 2 spin up a preview environment from the PR; 3 drive, an agent clicks, calls and watches; 4 capture screenshots, requests, responses, logs.](../slides/how-to-kill-the-code-review/deep/s61.webp)](../slides/how-to-kill-the-code-review/deep/s61.webp)

Slide 61. How to prove a criterion

[![Slide 62: Every criterion, its own proof: what the user sees, screenshot and DOM snapshot; an API contract, recorded request and response; side effects, network requests, server logs, DB state; a code rule, ast-grep match or a file:line citation; behavior over time, a test run and its trace.](../slides/how-to-kill-the-code-review/deep/s62.webp)](../slides/how-to-kill-the-code-review/deep/s62.webp)

Slide 62. Every criterion, its own proof

[![Slide 63: Verification proves what you asked. Not what you forgot to ask.](../slides/how-to-kill-the-code-review/deep/s63.webp)](../slides/how-to-kill-the-code-review/deep/s63.webp)

Slide 63. Verification proves what you asked

[![Slide 64: Step 5 of 6, Debate: humans, on the decisions.](../slides/how-to-kill-the-code-review/deep/s64.webp)](../slides/how-to-kill-the-code-review/deep/s64.webp)

Slide 64. Debate

[![Slide 65: No verification layer answers this.](../slides/how-to-kill-the-code-review/deep/s65.webp)](../slides/how-to-kill-the-code-review/deep/s65.webp)

Slide 65. No verification layer answers this

[![Slide 66: And here&#x27;s the part that worries me.](../slides/how-to-kill-the-code-review/deep/s66.webp)](../slides/how-to-kill-the-code-review/deep/s66.webp)

Slide 66. The part that worries me

[![Slide 67: Code review is the only scheduled moment engineers talk to each other about the system.](../slides/how-to-kill-the-code-review/deep/s67.webp)](../slides/how-to-kill-the-code-review/deep/s67.webp)

Slide 67. The only scheduled moment

[![Slide 68: Automate code review, and you delete shared understanding, on a light slide.](../slides/how-to-kill-the-code-review/deep/s68.webp)](../slides/how-to-kill-the-code-review/deep/s68.webp)

Slide 68. Delete shared understanding

[![Slide 69: Quote: The death of a program happens when the programmer team possessing its theory is dissolved. Peter Naur, 1985. Programming as Theory Building, verified verbatim.](../slides/how-to-kill-the-code-review/deep/s69.webp)](../slides/how-to-kill-the-code-review/deep/s69.webp)

Slide 69. Naur, 1985

[![Slide 70: Knowledge sharing was never a side effect of review. It was the product.](../slides/how-to-kill-the-code-review/deep/s70.webp)](../slides/how-to-kill-the-code-review/deep/s70.webp)

Slide 70. It was the product

[![Slide 71: So keep the conversation. Change what it&#x27;s about.](../slides/how-to-kill-the-code-review/deep/s71.webp)](../slides/how-to-kill-the-code-review/deep/s71.webp)

Slide 71. Change what it&#x27;s about

[![Slide 72: Debate decisions not diffs: tradeoffs, defaults, rejected options, scope cuts.](../slides/how-to-kill-the-code-review/deep/s72.webp)](../slides/how-to-kill-the-code-review/deep/s72.webp)

Slide 72. Debate decisions, not diffs

[![Slide 73: Criteria vs decisions. Acceptance criteria: what it should do, written while you build, pass or fail, for example a 429 is retried after Retry-After. Decisions: the calls made getting there, made by you and the agents along the way, right or wrong for a reason, for example retry 5xx, never 4xx.](../slides/how-to-kill-the-code-review/deep/s73.webp)](../slides/how-to-kill-the-code-review/deep/s73.webp)

Slide 73. Criteria vs decisions

[![Slide 74: Where decisions come from, first item only: while you build, the agent asks about some choices and makes others silently. The later items were not photographed.](../slides/how-to-kill-the-code-review/deep/s74.webp)](../slides/how-to-kill-the-code-review/deep/s74.webp)

Slide 74. Where decisions come from (first build)

[![Slide 75: Every decision on that PR, with where it came from and the outcome: retry 5xx and timeouts, never 4xx, while building, decided; exponential backoff capped at 10 minutes, while building, decided; honor Retry-After on a 429, verification failed, fixed; deduplicate retried deliveries, agents disagreed, needs a human; give up after 24h and mark the endpoint failing, review, follow-up ticket.](../slides/how-to-kill-the-code-review/deep/s75.webp)](../slides/how-to-kill-the-code-review/deep/s75.webp)

Slide 75. Every decision on that PR

[![Slide 76: How you review decisions: 1 skim what&#x27;s settled, the calls the agents made with their reasons; 2 settle what they couldn&#x27;t, the disagreements left open; 3 reopen any call you&#x27;d make differently, never edited, only reopened; 4 talk it through with the author, that conversation is where understanding gets built.](../slides/how-to-kill-the-code-review/deep/s76.webp)](../slides/how-to-kill-the-code-review/deep/s76.webp)

Slide 76. How you review decisions

[![Slide 77: Step 6 of 6, Own: what happens to accountability?](../slides/how-to-kill-the-code-review/deep/s77.webp)](../slides/how-to-kill-the-code-review/deep/s77.webp)

Slide 77. Own

[![Slide 78: A model has no reputation. A model has no liability. A model cannot be asked why.](../slides/how-to-kill-the-code-review/deep/s78.webp)](../slides/how-to-kill-the-code-review/deep/s78.webp)

Slide 78. A model has no reputation

[![Slide 79: Responsibility moved: the author wrote it and owned it, the reviewer read it and approved it, now the team writes the rules that verify it.](../slides/how-to-kill-the-code-review/deep/s79.webp)](../slides/how-to-kill-the-code-review/deep/s79.webp)

Slide 79. Responsibility moved

[![Slide 80: What owning the rules looks like on a bad day.](../slides/how-to-kill-the-code-review/deep/s80.webp)](../slides/how-to-kill-the-code-review/deep/s80.webp)

Slide 80. On a bad day

[![Slide 81: Every filter passed it: 1 the author&#x27;s agent wrote it with an engineer; 2 cross-examination argued ERROR vs FAILED and optional checks; 3 an AI review bot commented, nothing blocking; 4 acceptance criteria, 6 of 7 passed, 1 accepted.](../slides/how-to-kill-the-code-review/deep/s81.webp)](../slides/how-to-kill-the-code-review/deep/s81.webp)

Slide 81. Every filter passed it

[![Slide 82: Why it passed: the criteria described behavior, not cost at prod scale; the preview env has none of prod&#x27;s data; both agents argued semantics and neither read the query plan; one of our own rules, filter in SQL, pushed toward it.](../slides/how-to-kill-the-code-review/deep/s82.webp)](../slides/how-to-kill-the-code-review/deep/s82.webp)

Slide 82. Why it passed

[![Slide 83: 18 minutes: 6:27 PM impact starts, 6:30 identified and rollback started, 6:45 rollback complete, 7:02 resolved. status.aviator.co, Oct 26, 2026, Pacific Time.](../slides/how-to-kill-the-code-review/deep/s83.webp)](../slides/how-to-kill-the-code-review/deep/s83.webp)

Slide 83. 18 minutes

[![Slide 84: None of this replaces continuous delivery. Small releases. Flags. Fast rollback.](../slides/how-to-kill-the-code-review/deep/s84.webp)](../slides/how-to-kill-the-code-review/deep/s84.webp)

Slide 84. None of this replaces CD

[![Slide 85: Nobody asked who approved it. We asked which rule was missing.](../slides/how-to-kill-the-code-review/deep/s85.webp)](../slides/how-to-kill-the-code-review/deep/s85.webp)

Slide 85. Which rule was missing

[![Slide 86: Queries on large tables stay bounded by an index: the invariant, two days later. Since then: caught an unbounded subselect on a 2.9M-row table, before merge.](../slides/how-to-kill-the-code-review/deep/s86.webp)](../slides/how-to-kill-the-code-review/deep/s86.webp)

Slide 86. The invariant, two days later

[![Slide 87: A year later: 4x PRs merged per week; 3.4h median time to merge, was 2.1 days; 1.3 human threads per PR, was 6.2; -40% reverts. 9 engineers, one team, Nov 2025 to Nov 2026.](../slides/how-to-kill-the-code-review/deep/s87.webp)](../slides/how-to-kill-the-code-review/deep/s87.webp)

Slide 87. A year later

[![Slide 88: Fewer reverts, at 4x the volume: 10 reverts a quarter in Nov 2025, 6 in Nov 2026. The slide footer reads: PLACEHOLDER NUMBERS, replace before the talk.](../slides/how-to-kill-the-code-review/deep/s88.webp)](../slides/how-to-kill-the-code-review/deep/s88.webp)

Slide 88. Fewer reverts

[![Slide 89: The first 90 days were hard: month 1, double work, reviewing code and writing invariants; month 2, invariants catch enough that reviews shrink; month 3, you read intent and evidence, not code.](../slides/how-to-kill-the-code-review/deep/s89.webp)](../slides/how-to-kill-the-code-review/deep/s89.webp)

Slide 89. The first 90 days were hard

[![Slide 90: Where our time goes now: refining invariants, tighten the scope, retire the noisy ones, promote the stable ones to rules; debating decisions, the calls the agents couldn&#x27;t settle and the ones we&#x27;d make differently; improving verification, better scenarios, better evidence, faster preview environments.](../slides/how-to-kill-the-code-review/deep/s90.webp)](../slides/how-to-kill-the-code-review/deep/s90.webp)

Slide 90. Where our time goes now

[![Slide 91: Run a 90-day pilot: 1 prerequisites first, CI, continuous delivery, flags, fast rollback; 2 pick one team, high PR volume, mature CI; 3 baseline before day one, reverts, incidents, time to merge, reviewer load; 4 mine, codify, capture, top 20 comments become invariants, intent on every PR; 5 decide at day 90 against kill criteria you wrote down up front.](../slides/how-to-kill-the-code-review/deep/s91.webp)](../slides/how-to-kill-the-code-review/deep/s91.webp)

Slide 91. Run a 90-day pilot

[![Slide 92: What changes at scale. Who owns an invariant? A team, named on the rule; it retires the noisy ones. Two teams&#x27; rules conflict? The team that owns the code path decides; the rule records why. What still gets line-by-line review? Auth, payments, migrations, infra. What does the approver sign? The intent, the decisions and the evidence, not the diff.](../slides/how-to-kill-the-code-review/deep/s92.webp)](../slides/how-to-kill-the-code-review/deep/s92.webp)

Slide 92. What changes at scale

[![Slide 93: Section slide: Here&#x27;s your homework.](../slides/how-to-kill-the-code-review/deep/s93.webp)](../slides/how-to-kill-the-code-review/deep/s93.webp)

Slide 93. Homework

[![Slide 94: Kill the line-by-line review theater.](../slides/how-to-kill-the-code-review/deep/s94.webp)](../slides/how-to-kill-the-code-review/deep/s94.webp)

Slide 94. Kill the theater

[![Slide 95: AI is good at finding bugs. Humans are good at judgment.](../slides/how-to-kill-the-code-review/deep/s95.webp)](../slides/how-to-kill-the-code-review/deep/s95.webp)

Slide 95. Bugs and judgment

[![Slide 96: Six verbs, six things: 1 run a second reviewer, different model, PR-Agent is MIT and free; 2 write down what they settled, intent and acceptance criteria on the PR; 3 harvest your last 1000 review comments, the top 20 become invariants; 4 ask for evidence, not a green check, a screenshot, a request, a log per criterion; 5 change what the conversation is about, decisions, not the diff; 6 define ownership of rules and what ownership now means.](../slides/how-to-kill-the-code-review/deep/s96.webp)](../slides/how-to-kill-the-code-review/deep/s96.webp)

Slide 96. Six verbs, six things

[![Slide 97: Work on the tools and culture together: build tools to push decisions to the same PR; have a conversation with the team to change behavior; define guardrails to build the trust.](../slides/how-to-kill-the-code-review/deep/s97.webp)](../slides/how-to-kill-the-code-review/deep/s97.webp)

Slide 97. Tools and culture together

[![Slide 98: Hangar DX, dx.community, with a QR code. Quote: You can outsource your thinking, but you can&#x27;t outsource your understanding, Andrej Karpathy. @ankitxg. Aviator, aviator.co/verify.](../slides/how-to-kill-the-code-review/deep/s98.webp)](../slides/how-to-kill-the-code-review/deep/s98.webp)

Slide 98. Close
