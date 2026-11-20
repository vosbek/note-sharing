---
title: "Slides: How To Kill the Code Review"
---

# Slides: How To Kill the Code Review

[Back to the notes](../talks/how-to-kill-the-code-review.md)

[![Slide 1: How to kill the code review. The gate is still there, it just isn't stopping anything. Ankit Jain, Aviator.](../slides/how-to-kill-the-code-review/deep/s01.webp)](../slides/how-to-kill-the-code-review/deep/s01.webp)

*Slide 1: Title*

[![Slide 2: I'm going to argue we should kill the code review. I run a company that sells the replacement. So be suspicious of me.](../slides/how-to-kill-the-code-review/deep/s02.webp)](../slides/how-to-kill-the-code-review/deep/s02.webp)

*Slide 2: Be suspicious of me*

[![Slide 3: Code reviews are dead: the How to Kill the Code Review diagram of five Swiss cheese slices (compare multiple options, deterministic guardrails, acceptance criteria, permission systems, adversarial verification) between specs plus agents and the merge. latent.space/p/reviews-dead, Latent Space, March 2026.](../slides/how-to-kill-the-code-review/deep/s03.webp)](../slides/how-to-kill-the-code-review/deep/s03.webp)

*Slide 3: Code reviews are dead*

[![Slide 4: Five layers of trust: 1 compare multiple options, several agents try it, rank by tests, diff size, deps; 2 deterministic guardrails, linters, types, contracts, facts not opinions; 3 humans define acceptance criteria, written upstream before the code exists; 4 permission systems, scope what an agent may touch unattended; 5 adversarial verification, a separate agent tries to break it.](../slides/how-to-kill-the-code-review/deep/s04.webp)](../slides/how-to-kill-the-code-review/deep/s04.webp)

*Slide 4: Five layers of trust*

[![Slide 5: Section slide: Why do we review code.](../slides/how-to-kill-the-code-review/deep/s05.webp)](../slides/how-to-kill-the-code-review/deep/s05.webp)

*Slide 5: Why do we review code*

[![Slide 6: Bar chart: 44% rank finding defects as their number one reason for review; 14% of actual comments are about defects. Bacchelli and Bird, ICSE 2013, 570 comments classified.](../slides/how-to-kill-the-code-review/deep/s06.webp)](../slides/how-to-kill-the-code-review/deep/s06.webp)

*Slide 6: 44% say it's to find defects*

[![Slide 7: 9,000,000 reviewed changes at Google, same finding. Sadowski et al., ICSE-SEIP 2018.](../slides/how-to-kill-the-code-review/deep/s07.webp)](../slides/how-to-kill-the-code-review/deep/s07.webp)

*Slide 7: 9,000,000*

[![Slide 8: Code review is not about the code.](../slides/how-to-kill-the-code-review/deep/s08.webp)](../slides/how-to-kill-the-code-review/deep/s08.webp)

*Slide 8: Not about the code*

[![Slide 9: Code review is to build mental models.](../slides/how-to-kill-the-code-review/deep/s09.webp)](../slides/how-to-kill-the-code-review/deep/s09.webp)

*Slide 9: Mental models*

[![Slide 10: Code review is for knowledge sharing, on a light slide.](../slides/how-to-kill-the-code-review/deep/s10.webp)](../slides/how-to-kill-the-code-review/deep/s10.webp)

*Slide 10: Knowledge sharing*

[![Slide 11: Quote: We made writing cheap, and understanding stayed exactly as expensive as it has always been. Addy Osmani, Agentic Code Review, 15 Jun 2026.](../slides/how-to-kill-the-code-review/deep/s11.webp)](../slides/how-to-kill-the-code-review/deep/s11.webp)

*Slide 11: Understanding stayed expensive*

[![Slide 12: Section slide: The problem. How long until we stop reading the code?](../slides/how-to-kill-the-code-review/deep/s12.webp)](../slides/how-to-kill-the-code-review/deep/s12.webp)

*Slide 12: The problem*

[![Slide 13: We already have: +76% PRs merged with no review at all, +72% average PR size, +67% work restarts, +125% incidents per month. Faros AI Engineering Report Q3 2026, The Speed Trap, 18 Sep 2026, 22,000 devs, 4,000 teams.](../slides/how-to-kill-the-code-review/deep/s13.webp)](../slides/how-to-kill-the-code-review/deep/s13.webp)

*Slide 13: We already have*

[![Slide 14: AI adoption raises delivery throughput and delivery instability at the same time. DORA, State of AI-assisted Software Development 2025.](../slides/how-to-kill-the-code-review/deep/s14.webp)](../slides/how-to-kill-the-code-review/deep/s14.webp)

*Slide 14: Throughput and instability*

[![Slide 15: Quote: Those devs who put the same effort and energy into code review as before feel overloaded by AI slop PRs sent their way. Gergely Orosz, The Pragmatic Engineer, 23 Jul 2026.](../slides/how-to-kill-the-code-review/deep/s15.webp)](../slides/how-to-kill-the-code-review/deep/s15.webp)

*Slide 15: Overloaded by AI slop PRs*

[![Slide 16: No one voted to stop reviewing code. We just stopped. Screenshot of an r/ExperiencedDevs post: Today I announced that I won't be reviewing AI generated PRs at company meeting, 1.9K upvotes, 442 comments.](../slides/how-to-kill-the-code-review/deep/s16.webp)](../slides/how-to-kill-the-code-review/deep/s16.webp)

*Slide 16: No one voted*

[![Slide 17: Our team, a year apart: 4x PRs merged per week, 9 engineers both years, every PR still approved by a human. Aviator engineering, Nov 2025 to Nov 2026.](../slides/how-to-kill-the-code-review/deep/s17.webp)](../slides/how-to-kill-the-code-review/deep/s17.webp)

*Slide 17: Our team, a year apart*

[![Slide 18: A human still approves every PR. They just don't read the diff anymore.](../slides/how-to-kill-the-code-review/deep/s18.webp)](../slides/how-to-kill-the-code-review/deep/s18.webp)

*Slide 18: They don't read the diff*

[![Slide 19: Section slide: Can AI review the code?](../slides/how-to-kill-the-code-review/deep/s19.webp)](../slides/how-to-kill-the-code-review/deep/s19.webp)

*Slide 19: Can AI review the code?*

[![Slide 20: AI sucks at reviewing code: you get 15 findings, 12 are noise, now you research each one to find the 3 that matter.](../slides/how-to-kill-the-code-review/deep/s20.webp)](../slides/how-to-kill-the-code-review/deep/s20.webp)

*Slide 20: AI sucks at reviewing code*

[![Slide 21: But we were never that good at it either.](../slides/how-to-kill-the-code-review/deep/s21.webp)](../slides/how-to-kill-the-code-review/deep/s21.webp)

*Slide 21: Never that good at it*

[![Slide 22: Humans hit the same wall: 400 lines before defect detection falls off, 60 minutes before attention falls off, 640 lines in our median AI-generated PR. SmartBear, Cisco code review study, 2006, 2,500 reviews.](../slides/how-to-kill-the-code-review/deep/s22.webp)](../slides/how-to-kill-the-code-review/deep/s22.webp)

*Slide 22: Humans hit the same wall*

[![Slide 23: Because a diff is a bad place for review. One reviewer, reading once, from memory.](../slides/how-to-kill-the-code-review/deep/s23.webp)](../slides/how-to-kill-the-code-review/deep/s23.webp)

*Slide 23: A diff is a bad place*

[![Slide 24: Instead, we built review theater: a loop of agent writes, AI reviews, agent revises, AI reviews again, then a human skims and merges.](../slides/how-to-kill-the-code-review/deep/s24.webp)](../slides/how-to-kill-the-code-review/deep/s24.webp)

*Slide 24: Review theater*

[![Slide 25: Can AI genuinely review code well? Case for: it never gets tired or rushed, reads every line every time, same standard on every PR, awake at 3am. Case against: it never saw what was decided, was trained on the code it is reviewing, will never tell you not to build it, cannot be accountable.](../slides/how-to-kill-the-code-review/deep/s25.webp)](../slides/how-to-kill-the-code-review/deep/s25.webp)

*Slide 25: Can AI genuinely review code well?*

[![Slide 26: But a diff can't tell you what was decided.](../slides/how-to-kill-the-code-review/deep/s26.webp)](../slides/how-to-kill-the-code-review/deep/s26.webp)

*Slide 26: Can't tell what was decided*

[![Slide 27: Build tools for the things AI does well. Protect the things it cannot.](../slides/how-to-kill-the-code-review/deep/s27.webp)](../slides/how-to-kill-the-code-review/deep/s27.webp)

*Slide 27: Build tools for what AI does well*

[![Slide 28: We have been doing the exact opposite, on a light slide.](../slides/how-to-kill-the-code-review/deep/s28.webp)](../slides/how-to-kill-the-code-review/deep/s28.webp)

*Slide 28: The exact opposite*

[![Slide 29: Not everyone agrees. Quote: In the era of AI coding, human review is being scrutinized as a bottleneck to writing software. While that may be true, we have no current interest in removing that bottleneck. Wealthfront Engineering, 3 Aug 2026.](../slides/how-to-kill-the-code-review/deep/s29.webp)](../slides/how-to-kill-the-code-review/deep/s29.webp)

*Slide 29: Not everyone agrees*

[![Slide 30: They're right. The replacement doesn't exist yet.](../slides/how-to-kill-the-code-review/deep/s30.webp)](../slides/how-to-kill-the-code-review/deep/s30.webp)

*Slide 30: They're right*

[![Slide 31: Five layers of trust, revisited: four layers answered is it right, one answered is it what we meant, none of them asked are we building the right thing.](../slides/how-to-kill-the-code-review/deep/s31.webp)](../slides/how-to-kill-the-code-review/deep/s31.webp)

*Slide 31: Five layers, revisited*

[![Slide 32: The structure was right. I missed the human judgment entirely.](../slides/how-to-kill-the-code-review/deep/s32.webp)](../slides/how-to-kill-the-code-review/deep/s32.webp)

*Slide 32: I missed the human judgment*

[![Slide 33: Section slide: The framework. Same concepts. Better order. Practical implementation.](../slides/how-to-kill-the-code-review/deep/s33.webp)](../slides/how-to-kill-the-code-review/deep/s33.webp)

*Slide 33: The framework*

[![Slide 34: The new shape of review: six boxes. Argue, adversarial review, alternative solutions. Capture, intent plus criteria, knowledge transfer. Codify, the slop register, consistency. Prove, evidence per criterion, finding defects. Debate, the decisions, not in the essay. Own, the signature, gatekeeping.](../slides/how-to-kill-the-code-review/deep/s34.webp)](../slides/how-to-kill-the-code-review/deep/s34.webp)

*Slide 34: The new shape of review*

[![Slide 35: Step 1 of 6, Argue: let the agents argue before the PR exists.](../slides/how-to-kill-the-code-review/deep/s35.webp)](../slides/how-to-kill-the-code-review/deep/s35.webp)

*Slide 35: Argue*

[![Slide 36: Why is there a UI for two machines talking to each other?](../slides/how-to-kill-the-code-review/deep/s36.webp)](../slides/how-to-kill-the-code-review/deep/s36.webp)

*Slide 36: A UI for two machines?*

[![Slide 37: Instead of reading 4000 lines, read what they disagreed about.](../slides/how-to-kill-the-code-review/deep/s37.webp)](../slides/how-to-kill-the-code-review/deep/s37.webp)

*Slide 37: Read what they disagreed about*

[![Slide 38: What the agents argued about. Disagreement and how it settled: block the whole batch when a listed check fails or warn on reported checks only, decided by the agents with a reason; public docs for the new config key, won't fix with a reason; rename the config key, follow-up ticket; the one call a human made.](../slides/how-to-kill-the-code-review/deep/s38.webp)](../slides/how-to-kill-the-code-review/deep/s38.webp)

*Slide 38: What the agents argued about*

[![Slide 39: Layer 1, Argue: capture the decisions, not the verdict.](../slides/how-to-kill-the-code-review/deep/s39.webp)](../slides/how-to-kill-the-code-review/deep/s39.webp)

*Slide 39: Capture the decisions, not the verdict*

[![Slide 40: What they couldn't settle is what you debate.](../slides/how-to-kill-the-code-review/deep/s40.webp)](../slides/how-to-kill-the-code-review/deep/s40.webp)

*Slide 40: What they couldn't settle*

[![Slide 41: You can do this today: run two reviewers, different models; write a Skill that captures the disagreements; review that as part of the PR.](../slides/how-to-kill-the-code-review/deep/s41.webp)](../slides/how-to-kill-the-code-review/deep/s41.webp)

*Slide 41: You can do this today (Argue)*

[![Slide 42: Step 2 of 6, Capture: capture the what and the why.](../slides/how-to-kill-the-code-review/deep/s42.webp)](../slides/how-to-kill-the-code-review/deep/s42.webp)

*Slide 42: Capture*

[![Slide 43: The popular answer is to write the spec up front.](../slides/how-to-kill-the-code-review/deep/s43.webp)](../slides/how-to-kill-the-code-review/deep/s43.webp)

*Slide 43: Write the spec up front*

[![Slide 44: Why specs fail? Requires time. There's no feedback loop. The implementation drifts. That's the waterfall model we discarded 20 years ago.](../slides/how-to-kill-the-code-review/deep/s44.webp)](../slides/how-to-kill-the-code-review/deep/s44.webp)

*Slide 44: Why specs fail*

[![Slide 45: What can replace spec? Intent: why are we making this change? Acceptance criteria: how should it behave? Works for a 1-line bug fix and for a 1000-lines feature.](../slides/how-to-kill-the-code-review/deep/s45.webp)](../slides/how-to-kill-the-code-review/deep/s45.webp)

*Slide 45: What can replace spec?*

[![Slide 46: Where do these live? A Claude Code session in exports-service: add a rate limit to the exports endpoint (intent); use the existing RateLimiter util, skip the auth since middleware handles /api/v2, use the Money type not float (acceptance criteria, marked DECISION).](../slides/how-to-kill-the-code-review/deep/s46.webp)](../slides/how-to-kill-the-code-review/deep/s46.webp)

*Slide 46: Where do these live?*

[![Slide 47: And we throw these away when the session ends, on a light slide.](../slides/how-to-kill-the-code-review/deep/s47.webp)](../slides/how-to-kill-the-code-review/deep/s47.webp)

*Slide 47: We throw these away*

[![Slide 48: Do this today: capture intent and criteria during the session; publish them on the pull request, so the reviewer reads what you decided.](../slides/how-to-kill-the-code-review/deep/s48.webp)](../slides/how-to-kill-the-code-review/deep/s48.webp)

*Slide 48: Do this today (Capture)*

[![Slide 49: Step 3 of 6, Codify: turn repeated comments into deterministic rules.](../slides/how-to-kill-the-code-review/deep/s49.webp)](../slides/how-to-kill-the-code-review/deep/s49.webp)

*Slide 49: Codify*

[![Slide 50: Two kinds of review comment: Have you considered doing this differently? Use the Money type, not float. Only one of them needs human judgment.](../slides/how-to-kill-the-code-review/deep/s50.webp)](../slides/how-to-kill-the-code-review/deep/s50.webp)

*Slide 50: Two kinds of review comment*

[![Slide 51: What one of my reviews contained: PR \#11318, require /aviator revise at the start of a comment to trigger editing. Fourteen threads, bot and me, tagged NOISE, BUG, NIT, RULE and DECISION, for example: query hardcodes first 100, no pagination (noise); .delay() is duplicated in try and except (bug); use GraphQLRetryableException so Celery retries on it (rule); no comments extracted, tell the user on the PR? (decision).](../slides/how-to-kill-the-code-review/deep/s51.webp)](../slides/how-to-kill-the-code-review/deep/s51.webp)

*Slide 51: What one of my reviews contained*

[![Slide 52: Fourteen threads: 8 bot threads, 1 real bug; 3 rules I'd written on other PRs; 2 actual decisions.](../slides/how-to-kill-the-code-review/deep/s52.webp)](../slides/how-to-kill-the-code-review/deep/s52.webp)

*Slide 52: Fourteen threads*

[![Slide 53: Codify, the AI slop register: the running list of patterns your team keeps correcting.](../slides/how-to-kill-the-code-review/deep/s53.webp)](../slides/how-to-kill-the-code-review/deep/s53.webp)

*Slide 53: The AI slop register*

[![Slide 54: Codified as invariants: standing rules, checked on every change. Not remembered. Enforced.](../slides/how-to-kill-the-code-review/deep/s54.webp)](../slides/how-to-kill-the-code-review/deep/s54.webp)

*Slide 54: Invariants*

[![Slide 55: Codified as invariants: Money type for anything with a currency; no direct writes to the users table; structured logger only, no print; every error path emits a counter.](../slides/how-to-kill-the-code-review/deep/s55.webp)](../slides/how-to-kill-the-code-review/deep/s55.webp)

*Slide 55: Codified as invariants*

[![Slide 56: We mined a year of our comments: 11,400 review comments mined, 212 candidate rules, 64 invariants we kept. Reduce, extract, distill.](../slides/how-to-kill-the-code-review/deep/s56.webp)](../slides/how-to-kill-the-code-review/deep/s56.webp)

*Slide 56: We mined a year of comments*

[![Slide 57: An invariant, defined. Rule: every config change writes an audit-log entry, only when something changed. Scope: mutations and API handlers that write repo or account config. Verified by: save twice, read the audit log. Provenance: mined from 23 review threads across 17 PRs. Owner: platform team.](../slides/how-to-kill-the-code-review/deep/s57.webp)](../slides/how-to-kill-the-code-review/deep/s57.webp)

*Slide 57: An invariant, defined*

[![Slide 58: Every review comment your team repeats is a guardrail you haven't written, on a light slide.](../slides/how-to-kill-the-code-review/deep/s58.webp)](../slides/how-to-kill-the-code-review/deep/s58.webp)

*Slide 58: A guardrail you haven't written*

[![Slide 59: Step 4 of 6, Prove: prove it works, with evidence.](../slides/how-to-kill-the-code-review/deep/s59.webp)](../slides/how-to-kill-the-code-review/deep/s59.webp)

*Slide 59: Prove*

[![Slide 60: A green check might mean no bugs. It says nothing about the behavior.](../slides/how-to-kill-the-code-review/deep/s60.webp)](../slides/how-to-kill-the-code-review/deep/s60.webp)

*Slide 60: A green check*

[![Slide 61: How to prove a criterion: 1 plan, each criterion becomes a scenario; 2 spin up a preview environment from the PR; 3 drive, an agent clicks, calls and watches; 4 capture screenshots, requests, responses, logs.](../slides/how-to-kill-the-code-review/deep/s61.webp)](../slides/how-to-kill-the-code-review/deep/s61.webp)

*Slide 61: How to prove a criterion*

[![Slide 62: Every criterion, its own proof: what the user sees, screenshot and DOM snapshot; an API contract, recorded request and response; side effects, network requests, server logs, DB state; a code rule, ast-grep match or a file:line citation; behavior over time, a test run and its trace.](../slides/how-to-kill-the-code-review/deep/s62.webp)](../slides/how-to-kill-the-code-review/deep/s62.webp)

*Slide 62: Every criterion, its own proof*

[![Slide 63: Verification proves what you asked. Not what you forgot to ask.](../slides/how-to-kill-the-code-review/deep/s63.webp)](../slides/how-to-kill-the-code-review/deep/s63.webp)

*Slide 63: Verification proves what you asked*

[![Slide 64: Step 5 of 6, Debate: humans, on the decisions.](../slides/how-to-kill-the-code-review/deep/s64.webp)](../slides/how-to-kill-the-code-review/deep/s64.webp)

*Slide 64: Debate*

[![Slide 65: No verification layer answers this.](../slides/how-to-kill-the-code-review/deep/s65.webp)](../slides/how-to-kill-the-code-review/deep/s65.webp)

*Slide 65: No verification layer answers this*

[![Slide 66: And here's the part that worries me.](../slides/how-to-kill-the-code-review/deep/s66.webp)](../slides/how-to-kill-the-code-review/deep/s66.webp)

*Slide 66: The part that worries me*

[![Slide 67: Code review is the only scheduled moment engineers talk to each other about the system.](../slides/how-to-kill-the-code-review/deep/s67.webp)](../slides/how-to-kill-the-code-review/deep/s67.webp)

*Slide 67: The only scheduled moment*

[![Slide 68: Automate code review, and you delete shared understanding, on a light slide.](../slides/how-to-kill-the-code-review/deep/s68.webp)](../slides/how-to-kill-the-code-review/deep/s68.webp)

*Slide 68: Delete shared understanding*

[![Slide 69: Quote: The death of a program happens when the programmer team possessing its theory is dissolved. Peter Naur, 1985. Programming as Theory Building, verified verbatim.](../slides/how-to-kill-the-code-review/deep/s69.webp)](../slides/how-to-kill-the-code-review/deep/s69.webp)

*Slide 69: Naur, 1985*

[![Slide 70: Knowledge sharing was never a side effect of review. It was the product.](../slides/how-to-kill-the-code-review/deep/s70.webp)](../slides/how-to-kill-the-code-review/deep/s70.webp)

*Slide 70: It was the product*

[![Slide 71: So keep the conversation. Change what it's about.](../slides/how-to-kill-the-code-review/deep/s71.webp)](../slides/how-to-kill-the-code-review/deep/s71.webp)

*Slide 71: Change what it's about*

[![Slide 72: Debate decisions not diffs: tradeoffs, defaults, rejected options, scope cuts.](../slides/how-to-kill-the-code-review/deep/s72.webp)](../slides/how-to-kill-the-code-review/deep/s72.webp)

*Slide 72: Debate decisions, not diffs*

[![Slide 73: Criteria vs decisions. Acceptance criteria: what it should do, written while you build, pass or fail, for example a 429 is retried after Retry-After. Decisions: the calls made getting there, made by you and the agents along the way, right or wrong for a reason, for example retry 5xx, never 4xx.](../slides/how-to-kill-the-code-review/deep/s73.webp)](../slides/how-to-kill-the-code-review/deep/s73.webp)

*Slide 73: Criteria vs decisions*

[![Slide 74: Where decisions come from, first item only: while you build, the agent asks about some choices and makes others silently. The later items were not photographed.](../slides/how-to-kill-the-code-review/deep/s74.webp)](../slides/how-to-kill-the-code-review/deep/s74.webp)

*Slide 74: Where decisions come from (first build)*

[![Slide 75: Every decision on that PR, with where it came from and the outcome: retry 5xx and timeouts, never 4xx, while building, decided; exponential backoff capped at 10 minutes, while building, decided; honor Retry-After on a 429, verification failed, fixed; deduplicate retried deliveries, agents disagreed, needs a human; give up after 24h and mark the endpoint failing, review, follow-up ticket.](../slides/how-to-kill-the-code-review/deep/s75.webp)](../slides/how-to-kill-the-code-review/deep/s75.webp)

*Slide 75: Every decision on that PR*

[![Slide 76: How you review decisions: 1 skim what's settled, the calls the agents made with their reasons; 2 settle what they couldn't, the disagreements left open; 3 reopen any call you'd make differently, never edited, only reopened; 4 talk it through with the author, that conversation is where understanding gets built.](../slides/how-to-kill-the-code-review/deep/s76.webp)](../slides/how-to-kill-the-code-review/deep/s76.webp)

*Slide 76: How you review decisions*

[![Slide 77: Step 6 of 6, Own: what happens to accountability?](../slides/how-to-kill-the-code-review/deep/s77.webp)](../slides/how-to-kill-the-code-review/deep/s77.webp)

*Slide 77: Own*

[![Slide 78: A model has no reputation. A model has no liability. A model cannot be asked why.](../slides/how-to-kill-the-code-review/deep/s78.webp)](../slides/how-to-kill-the-code-review/deep/s78.webp)

*Slide 78: A model has no reputation*

[![Slide 79: Responsibility moved: the author wrote it and owned it, the reviewer read it and approved it, now the team writes the rules that verify it.](../slides/how-to-kill-the-code-review/deep/s79.webp)](../slides/how-to-kill-the-code-review/deep/s79.webp)

*Slide 79: Responsibility moved*

[![Slide 80: What owning the rules looks like on a bad day.](../slides/how-to-kill-the-code-review/deep/s80.webp)](../slides/how-to-kill-the-code-review/deep/s80.webp)

*Slide 80: On a bad day*

[![Slide 81: Every filter passed it: 1 the author's agent wrote it with an engineer; 2 cross-examination argued ERROR vs FAILED and optional checks; 3 an AI review bot commented, nothing blocking; 4 acceptance criteria, 6 of 7 passed, 1 accepted.](../slides/how-to-kill-the-code-review/deep/s81.webp)](../slides/how-to-kill-the-code-review/deep/s81.webp)

*Slide 81: Every filter passed it*

[![Slide 82: Why it passed: the criteria described behavior, not cost at prod scale; the preview env has none of prod's data; both agents argued semantics and neither read the query plan; one of our own rules, filter in SQL, pushed toward it.](../slides/how-to-kill-the-code-review/deep/s82.webp)](../slides/how-to-kill-the-code-review/deep/s82.webp)

*Slide 82: Why it passed*

[![Slide 83: 18 minutes: 6:27 PM impact starts, 6:30 identified and rollback started, 6:45 rollback complete, 7:02 resolved. status.aviator.co, Oct 26, 2026, Pacific Time.](../slides/how-to-kill-the-code-review/deep/s83.webp)](../slides/how-to-kill-the-code-review/deep/s83.webp)

*Slide 83: 18 minutes*

[![Slide 84: None of this replaces continuous delivery. Small releases. Flags. Fast rollback.](../slides/how-to-kill-the-code-review/deep/s84.webp)](../slides/how-to-kill-the-code-review/deep/s84.webp)

*Slide 84: None of this replaces CD*

[![Slide 85: Nobody asked who approved it. We asked which rule was missing.](../slides/how-to-kill-the-code-review/deep/s85.webp)](../slides/how-to-kill-the-code-review/deep/s85.webp)

*Slide 85: Which rule was missing*

[![Slide 86: Queries on large tables stay bounded by an index: the invariant, two days later. Since then: caught an unbounded subselect on a 2.9M-row table, before merge.](../slides/how-to-kill-the-code-review/deep/s86.webp)](../slides/how-to-kill-the-code-review/deep/s86.webp)

*Slide 86: The invariant, two days later*

[![Slide 87: A year later: 4x PRs merged per week; 3.4h median time to merge, was 2.1 days; 1.3 human threads per PR, was 6.2; -40% reverts. 9 engineers, one team, Nov 2025 to Nov 2026.](../slides/how-to-kill-the-code-review/deep/s87.webp)](../slides/how-to-kill-the-code-review/deep/s87.webp)

*Slide 87: A year later*

[![Slide 88: Fewer reverts, at 4x the volume: 10 reverts a quarter in Nov 2025, 6 in Nov 2026. The slide footer reads: PLACEHOLDER NUMBERS, replace before the talk.](../slides/how-to-kill-the-code-review/deep/s88.webp)](../slides/how-to-kill-the-code-review/deep/s88.webp)

*Slide 88: Fewer reverts*

[![Slide 89: The first 90 days were hard: month 1, double work, reviewing code and writing invariants; month 2, invariants catch enough that reviews shrink; month 3, you read intent and evidence, not code.](../slides/how-to-kill-the-code-review/deep/s89.webp)](../slides/how-to-kill-the-code-review/deep/s89.webp)

*Slide 89: The first 90 days were hard*

[![Slide 90: Where our time goes now: refining invariants, tighten the scope, retire the noisy ones, promote the stable ones to rules; debating decisions, the calls the agents couldn't settle and the ones we'd make differently; improving verification, better scenarios, better evidence, faster preview environments.](../slides/how-to-kill-the-code-review/deep/s90.webp)](../slides/how-to-kill-the-code-review/deep/s90.webp)

*Slide 90: Where our time goes now*

[![Slide 91: Run a 90-day pilot: 1 prerequisites first, CI, continuous delivery, flags, fast rollback; 2 pick one team, high PR volume, mature CI; 3 baseline before day one, reverts, incidents, time to merge, reviewer load; 4 mine, codify, capture, top 20 comments become invariants, intent on every PR; 5 decide at day 90 against kill criteria you wrote down up front.](../slides/how-to-kill-the-code-review/deep/s91.webp)](../slides/how-to-kill-the-code-review/deep/s91.webp)

*Slide 91: Run a 90-day pilot*

[![Slide 92: What changes at scale. Who owns an invariant? A team, named on the rule; it retires the noisy ones. Two teams' rules conflict? The team that owns the code path decides; the rule records why. What still gets line-by-line review? Auth, payments, migrations, infra. What does the approver sign? The intent, the decisions and the evidence, not the diff.](../slides/how-to-kill-the-code-review/deep/s92.webp)](../slides/how-to-kill-the-code-review/deep/s92.webp)

*Slide 92: What changes at scale*

[![Slide 93: Section slide: Here's your homework.](../slides/how-to-kill-the-code-review/deep/s93.webp)](../slides/how-to-kill-the-code-review/deep/s93.webp)

*Slide 93: Homework*

[![Slide 94: Kill the line-by-line review theater.](../slides/how-to-kill-the-code-review/deep/s94.webp)](../slides/how-to-kill-the-code-review/deep/s94.webp)

*Slide 94: Kill the theater*

[![Slide 95: AI is good at finding bugs. Humans are good at judgment.](../slides/how-to-kill-the-code-review/deep/s95.webp)](../slides/how-to-kill-the-code-review/deep/s95.webp)

*Slide 95: Bugs and judgment*

[![Slide 96: Six verbs, six things: 1 run a second reviewer, different model, PR-Agent is MIT and free; 2 write down what they settled, intent and acceptance criteria on the PR; 3 harvest your last 1000 review comments, the top 20 become invariants; 4 ask for evidence, not a green check, a screenshot, a request, a log per criterion; 5 change what the conversation is about, decisions, not the diff; 6 define ownership of rules and what ownership now means.](../slides/how-to-kill-the-code-review/deep/s96.webp)](../slides/how-to-kill-the-code-review/deep/s96.webp)

*Slide 96: Six verbs, six things*

[![Slide 97: Work on the tools and culture together: build tools to push decisions to the same PR; have a conversation with the team to change behavior; define guardrails to build the trust.](../slides/how-to-kill-the-code-review/deep/s97.webp)](../slides/how-to-kill-the-code-review/deep/s97.webp)

*Slide 97: Tools and culture together*

[![Slide 98: Hangar DX, dx.community, with a QR code. Quote: You can outsource your thinking, but you can't outsource your understanding, Andrej Karpathy. @ankitxg. Aviator, aviator.co/verify.](../slides/how-to-kill-the-code-review/deep/s98.webp)](../slides/how-to-kill-the-code-review/deep/s98.webp)

*Slide 98: Close*
