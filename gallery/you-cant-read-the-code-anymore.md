---
title: "Slides: You Can't Read the Code Anymore - Verifying Software in the Age of AI"
---

# Slides: You Can't Read the Code Anymore - Verifying Software in the Age of AI

[Back to the notes](../talks/you-cant-read-the-code-anymore.md)

[![Slide 1: Title: You Can't Read the Code Anymore, Verifying Software in the Age of AI. Omer van Kloeten, Principal Engineer, Forter.](../slides/you-cant-read-the-code-anymore/deep/s01.webp)](../slides/you-cant-read-the-code-anymore/deep/s01.webp)

*Slide 1: Title*

[![Slide 2: Meet Gate, our API orchestrator: hand-drawn GATE box with HTTP in and downstream arrows, clouds, databases, queues and question marks, captioned simplified.](../slides/you-cant-read-the-code-anymore/deep/s02.webp)](../slides/you-cant-read-the-code-anymore/deep/s02.webp)

*Slide 2: Meet Gate*

[![Slide 3: Existing codebases are scary: we never read the code, unknown is scary, still adding stuff. Change plus fear equals bigger change. Cartoon of a pilot in a patched plane labelled brownfield development.](../slides/you-cant-read-the-code-anymore/deep/s03.webp)](../slides/you-cant-read-the-code-anymore/deep/s03.webp)

*Slide 3: Existing codebases are scary*

[![Slide 4: Enter coding AI agents: reading code is much harder than writing it; more code we didn't write.](../slides/you-cant-read-the-code-anymore/deep/s04.webp)](../slides/you-cant-read-the-code-anymore/deep/s04.webp)

*Slide 4: Enter coding AI agents*

[![Slide 5: Expectations: “Everyone else is shipping 10x as fast!” your manager? Is being scared the new normal? Cartoon of a plane labelled AI coding.](../slides/you-cant-read-the-code-anymore/deep/s05.webp)](../slides/you-cant-read-the-code-anymore/deep/s05.webp)

*Slide 5: Expectations*

[![Slide 6: Hi, I'm Omer: over 25 years of experience, Principal Engineer at Forter, focus: systemic concerns in engineering. Photo and Forter logo.](../slides/you-cant-read-the-code-anymore/deep/s06.webp)](../slides/you-cant-read-the-code-anymore/deep/s06.webp)

*Slide 6: Hi, I’m Omer*

[![Slide 7: This talk: what's fundamentally changed, verify what you build, verify what you didn't, DIY.](../slides/you-cant-read-the-code-anymore/deep/s07.webp)](../slides/you-cant-read-the-code-anymore/deep/s07.webp)

*Slide 7: This talk*

[![Slide 8: Verifying agentic output: AI writes code and tests (+5391 −1457), I ain't reading all that, spot check / trust it / vibe, ship slop. Tests overfit and fragile; AI marking its own homework; we've reinvented manual QA, poorly.](../slides/you-cant-read-the-code-anymore/deep/s08.webp)](../slides/you-cant-read-the-code-anymore/deep/s08.webp)

*Slide 8: Verifying agentic output*

[![Slide 9: Section slide: Why, What, How.](../slides/you-cant-read-the-code-anymore/deep/s09.webp)](../slides/you-cant-read-the-code-anymore/deep/s09.webp)

*Slide 9: Why, What, How*

[![Slide 10: Understanding the What: easy, write the code; hard, read code and tests. A long test file on screen.](../slides/you-cant-read-the-code-anymore/deep/s10.webp)](../slides/you-cant-read-the-code-anymore/deep/s10.webp)

*Slide 10: Understanding the What*

[![Slide 11: So don't read code: Cucumber, about 20 years ago, costly to write and maintain, let agents do it. Gherkin example about webhook delivery for a Kafka message.](../slides/you-cant-read-the-code-anymore/deep/s11.webp)](../slides/you-cant-read-the-code-anymore/deep/s11.webp)

*Slide 11: So don’t read code*

[![Slide 12: Reframed workflow for agents. Our goal: aligning on the What. Human thinks and reconsiders, agent grills, loop. What plus-equals readable tests.](../slides/you-cant-read-the-code-anymore/deep/s12.webp)](../slides/you-cant-read-the-code-anymore/deep/s12.webp)

*Slide 12: Aligning on the What*

[![Slide 13: Reframed workflow: human writes agent spec, human aligns with agent on What, agent writes implementation with tests as feedback loop, agent refactors and simplifies. Solved!](../slides/you-cant-read-the-code-anymore/deep/s13.webp)](../slides/you-cant-read-the-code-anymore/deep/s13.webp)

*Slide 13: Reframed workflow*

[![Slide 14: Section slide: I Don't Trust the Tests.](../slides/you-cant-read-the-code-anymore/deep/s14.webp)](../slides/you-cant-read-the-code-anymore/deep/s14.webp)

*Slide 14: I don’t trust the tests*

[![Slide 15: Properties to increase trust: What equals behaviors, effects on users (PM cap) and on other parts of the system (architect cap); blackbox behavior. Given merchant A is configured as async, then I get a 202 response, the fraud decision is made and the audit log written.](../slides/you-cant-read-the-code-anymore/deep/s15.webp)](../slides/you-cant-read-the-code-anymore/deep/s15.webp)

*Slide 15: Blackbox*

[![Slide 16: Properties to increase trust: behavior exposed is behavior used (Hyrum's Law); missing test means assumptions and hallucinations; therefore comprehensive. Same scenario with flag A off and on.](../slides/you-cant-read-the-code-anymore/deep/s16.webp)](../slides/you-cant-read-the-code-anymore/deep/s16.webp)

*Slide 16: Comprehensive*

[![Slide 17: Properties to increase trust: tests with implicit behavior plus assumptions, therefore explicit. Flag A on: we should write to S3; flag A off: we shouldn't write to S3.](../slides/you-cant-read-the-code-anymore/deep/s17.webp)](../slides/you-cant-read-the-code-anymore/deep/s17.webp)

*Slide 17: Explicit*

[![Slide 18: Blackbox, Comprehensive, Explicit, Plain-English Tests.](../slides/you-cant-read-the-code-anymore/deep/s18.webp)](../slides/you-cant-read-the-code-anymore/deep/s18.webp)

*Slide 18: The first four properties*

[![Slide 19: Sidebar, not just you and the agent: teammate reviews a PR; plain-English tests give a readable What. 100 line items of \$5 with 1% tax: should the tax be \$0 or \$5? Code floors per-item tax.](../slides/you-cant-read-the-code-anymore/deep/s19.webp)](../slides/you-cant-read-the-code-anymore/deep/s19.webp)

*Slide 19: Sidebar: the reviewer*

[![Slide 20: Implementation erodes comprehensiveness: can't think of everything, implementation will introduce behaviors. Given one \$500 line item and 1% tax, tax \$5, beside code with per-item floor.](../slides/you-cant-read-the-code-anymore/deep/s20.webp)](../slides/you-cant-read-the-code-anymore/deep/s20.webp)

*Slide 20: Implementation erodes comprehensiveness*

[![Slide 21: Make incidental behaviors explicit. Whitebox: comprehensive green tests from whitebox inspection. Disagreement means alignment. Given 100 line items of \$5 each and 1% tax, the tax should be \$0.](../slides/you-cant-read-the-code-anymore/deep/s21.webp)](../slides/you-cant-read-the-code-anymore/deep/s21.webp)

*Slide 21: Make incidental behaviors explicit*

[![Slide 22: Four circles: Red\* achieve mutual understanding, Green minimum implementation, Refactor clean implementation, Whitebox make incidental behaviors explicit.](../slides/you-cant-read-the-code-anymore/deep/s22.webp)](../slides/you-cant-read-the-code-anymore/deep/s22.webp)

*Slide 22: Red, Green, Refactor, Whitebox*

[![Slide 23: This won't work in brownfield: new interacts with existing, missing feedback loop, the usual move is writing tests to pin current behavior. Quote: we've had three senior engineers attempt and fail to backfill tests to our team's codebase. Sr. Engineer, Billing.](../slides/you-cant-read-the-code-anymore/deep/s23.webp)](../slides/you-cant-read-the-code-anymore/deep/s23.webp)

*Slide 23: This won’t work in brownfield*

[![Slide 24: Telem logo with a star, pronounced like tell 'em.](../slides/you-cant-read-the-code-anymore/deep/s24.webp)](../slides/you-cant-read-the-code-anymore/deep/s24.webp)

*Slide 24: Telem*

[![Slide 25: Telem skills plus deterministic tooling: skill invocation graph; tools like only reference entry point means blackbox, comprehensive decision tables, new feature flag must be declared explicitly or fail, linters for tests and implementation.](../slides/you-cant-read-the-code-anymore/deep/s25.webp)](../slides/you-cant-read-the-code-anymore/deep/s25.webp)

*Slide 25: Skills and deterministic tooling*

[![Slide 26: Close-up of the skill invocation graph for telem-bdd, from bootstrap and create-fakes through the backfill steps.](../slides/you-cant-read-the-code-anymore/deep/s26.webp)](../slides/you-cant-read-the-code-anymore/deep/s26.webp)

*Slide 26: Skill invocation graph, close-up*

[![Slide 27: Engineer's role: Gate, about 8,000 business flows (sum over 24,000). Gherkin scenarios in the background.](../slides/you-cant-read-the-code-anymore/deep/s27.webp)](../slides/you-cant-read-the-code-anymore/deep/s27.webp)

*Slide 27: Engineer’s role*

[![Slide 28: Explain it back to me: /walkthrough, conversation with agent using crit, surprises are successes, alignment: see forest before trees. Screenshot of a Create Billing Snapshots explainer.](../slides/you-cant-read-the-code-anymore/deep/s28.webp)](../slides/you-cant-read-the-code-anymore/deep/s28.webp)

*Slide 28: Explain it back to me*

[![Slide 29: We did it: “With Telem, we achieved comprehensive test coverage across the entire repo within a single quarter.” Sr. Engineer, Billing.](../slides/you-cant-read-the-code-anymore/deep/s29.webp)](../slides/you-cant-read-the-code-anymore/deep/s29.webp)

*Slide 29: We did it*

[![Slide 30: Over 10,000: user-invokable behaviors not broken at Forter, past 60 days.](../slides/you-cant-read-the-code-anymore/deep/s30.webp)](../slides/you-cant-read-the-code-anymore/deep/s30.webp)

*Slide 30: Over 10,000*

[![Slide 31: Making this sustainable: blackbox-only, comprehensive, explicit; generated a lot of tests; long feedback loop is bad; blazingly fast. 24,740 passed, 0 failed; 58.4s wall time.](../slides/you-cant-read-the-code-anymore/deep/s31.webp)](../slides/you-cant-read-the-code-anymore/deep/s31.webp)

*Slide 31: 58.4 seconds*

[![Slide 32: Behind the curtain: blackbox plus fast? Doubt. Fakes: test doubles, rudimentary, in-memory, no IO; drift? parity tested; whole other talk. Tests don't leave their runtime, so blazingly fast.](../slides/you-cant-read-the-code-anymore/deep/s32.webp)](../slides/you-cant-read-the-code-anymore/deep/s32.webp)

*Slide 32: Behind the curtain: fakes*

[![Slide 33: Bonus properties: flaky tests suck, flakiness from nondeterminism, fake everything gives determinism; we control the world around tests, forbid the outside world gives hermetic. Error: unexpected write to table Foo.](../slides/you-cant-read-the-code-anymore/deep/s33.webp)](../slides/you-cant-read-the-code-anymore/deep/s33.webp)

*Slide 33: Deterministic and hermetic*

[![Slide 34: Blackbox, Comprehensive, Explicit, Blazingly Fast, Deterministic, Hermetic, Plain-English Tests.](../slides/you-cant-read-the-code-anymore/deep/s34.webp)](../slides/you-cant-read-the-code-anymore/deep/s34.webp)

*Slide 34: All seven properties*

[![Slide 35: Started from a small and risky change: “Telem gave me the confidence that it behaves as I expected.” Principal Engineer, working on Gate. No unexpected behaviors, no incidents.](../slides/you-cant-read-the-code-anymore/deep/s35.webp)](../slides/you-cant-read-the-code-anymore/deep/s35.webp)

*Slide 35: The small risky change*

[![Slide 36: Compounding value, Telem as a translator: your ticket agent triages behavior, interrogates code, costly and error-prone; system behaviors now in plain English, validated, living documentation; ticket agent no longer guesses.](../slides/you-cant-read-the-code-anymore/deep/s36.webp)](../slides/you-cant-read-the-code-anymore/deep/s36.webp)

*Slide 36: Telem as a translator*

[![Slide 37: Compounding value: and context for more agents. “The agents come back with implementations that make sense.” Engineering Manager.](../slides/you-cant-read-the-code-anymore/deep/s37.webp)](../slides/you-cant-read-the-code-anymore/deep/s37.webp)

*Slide 37: Context for more agents*

[![Slide 38: Telem is specialized: not blackbox to blackbox integration, agentic system evals, architecture constraints and tradeoffs, your system in production.](../slides/you-cant-read-the-code-anymore/deep/s38.webp)](../slides/you-cant-read-the-code-anymore/deep/s38.webp)

*Slide 38: Telem is specialized*

[![Slide 39: Costs: AI backfills tests, \$100s to \$1000s in tokens per system, 1 to 2 hours in Claude Code per flow. Human attention: simple systems days, complex systems high variance; billing case study about 4 net engineering months, parallelized.](../slides/you-cant-read-the-code-anymore/deep/s39.webp)](../slides/you-cant-read-the-code-anymore/deep/s39.webp)

*Slide 39: Costs*

[![Slide 40: Convincing our own engineering managers: understand impact (internal dashboard, global and per-service metrics, speedup case studies) and quick time to value (flow backfilled then CI, incremental value). Dashboard shows 10,776 and 29,179.](../slides/you-cant-read-the-code-anymore/deep/s40.webp)](../slides/you-cant-read-the-code-anymore/deep/s40.webp)

*Slide 40: Convincing engineering managers*

[![Slide 41: DIY: seed; agent grows your Telem (skills, tools, methodology); sample: webhooks delivery; work in progress, feedback welcome; blog link; QR code for forter/telem-seed.](../slides/you-cant-read-the-code-anymore/deep/s41.webp)](../slides/you-cant-read-the-code-anymore/deep/s41.webp)

*Slide 41: DIY*

[![Slide 42: Thank you: @omervk, omervk@forter.com, QR code for forter/telem-seed.](../slides/you-cant-read-the-code-anymore/deep/s42.webp)](../slides/you-cant-read-the-code-anymore/deep/s42.webp)

*Slide 42: Thank you*
