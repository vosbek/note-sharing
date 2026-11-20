---
title: "Slides: Wait, You're Still Doing PRs?"
---

# Slides: Wait, You're Still Doing PRs?

[Back to the notes](../talks/wait-you-re-still-doing-prs.md)

[![Slide 1: Photo 1: Title slide: QCon vendor presentation, AI agents and software delivery. Wait, You're Still Doing PRs? A 50-minute argument for giving autonomous work a workflow of its own. Lee Faus, Atomic Software. 50 minutes, 6 acts, Q&A.](../slides/wait-you-re-still-doing-prs/deep/p01.webp)](../slides/wait-you-re-still-doing-prs/deep/p01.webp)

*Slide 1: Title slide*

[![Slide 2: Photo 2: Act 01, The Dark Ages, slide 2 of 12. The patch was ready. Steve was not. A Rube Goldberg machine feeds a bug report through Bugzilla, an SVN diff and a mailing list to a sleeping reviewer.](../slides/wait-you-re-still-doing-prs/deep/p02.webp)](../slides/wait-you-re-still-doing-prs/deep/p02.webp)

*Slide 2: Act 01: the dark ages*

[![Slide 3: Photo 3: Atomic's loop in five steps: 01 Intent, a Feature WorkIntent, the authored spec the work is held to. 02 Capture, a Change; each change comes from a planned SessionTurn. 03 Subject, a ReviewSubject, one content-addressed scope, pinned. 04 Conclusion, a PublicationReview, a signed judgment criterion by criterion. 05 Gate, a PublicationGate, a signed judgment criterion by criterion. Arrows loop back to the intent.](../slides/wait-you-re-still-doing-prs/deep/p03.webp)](../slides/wait-you-re-still-doing-prs/deep/p03.webp)

*Slide 3: The five-step loop*

[![Slide 4: Photo 4: Anatomy of a Feature WorkIntent, the authored spec the work is held to: frontmatter, why, acceptance criteria (one or more), tasks (one or more), files (one or more), scope in, scope out, constraints.](../slides/wait-you-re-still-doing-prs/deep/p04.webp)](../slides/wait-you-re-still-doing-prs/deep/p04.webp)

*Slide 4: Anatomy of an intent*

[![Slide 5: Photo 5: Demo setup: a VS Code workspace named demo-10 with only .atomic, .vault and .atomicignore, and OpenCode running the Atomic agent on GPT-6.1 Sol through OpenRouter.](../slides/wait-you-re-still-doing-prs/deep/p05.webp)](../slides/wait-you-re-still-doing-prs/deep/p05.webp)

*Slide 5: Demo: empty project*

[![Slide 6: Photo 6: Demo prompt typed into OpenCode: let's build a typescript hello world cli. Atomic agent, GPT-6.1 Sol via OpenRouter.](../slides/wait-you-re-still-doing-prs/deep/p06.webp)](../slides/wait-you-re-still-doing-prs/deep/p06.webp)

*Slide 6: Demo: the prompt*

[![Slide 7: Photo 7: Agent result: an attested.jsonld sidecar signed by a did:atomic author; the intent DEMO::continuouslee::1 is a feature, needs review, attested fresh and verified. Built a minimal TypeScript CLI; verified a clean install, a successful build and all 3 tests passing. 1 minute 3 seconds, 14.3K tokens, \$0.08.](../slides/wait-you-re-still-doing-prs/deep/p07.webp)](../slides/wait-you-re-still-doing-prs/deep/p07.webp)

*Slide 7: Demo: built, verified, needs review*

[![Slide 8: Photo 8: The intent rendered like an issue: Build a TypeScript hello world CLI, needs review, priority medium. Description: provide a runnable, minimal TypeScript command-line starting point in an otherwise empty repository. Acceptance criteria 1 of 1, met; tasks 1 of 1. The vault holds attestations, goals, intents, memory, prompts, scratch and skills.](../slides/wait-you-re-still-doing-prs/deep/p08.webp)](../slides/wait-you-re-still-doing-prs/deep/p08.webp)

*Slide 8: Demo: the intent page*

[![Slide 9: Photo 9: Verification evidence for criterion 1: verified by GPT-6.1 Sol via local shell. npm install and npm ci succeeded with zero vulnerabilities, npm test passed all 3 tests after each install, and npm start printed Hello, world. Task 1 done: the files to create and how to verify them.](../slides/wait-you-re-still-doing-prs/deep/p09.webp)](../slides/wait-you-re-still-doing-prs/deep/p09.webp)

*Slide 9: Demo: verification evidence*

[![Slide 10: Photo 10: The same intent as raw Markdown: an acceptance-criterion directive with an ID, status=met, verifiedBy and evidence attributes, and a task directive with status=done and criteria pointing at the criterion ID.](../slides/wait-you-re-still-doing-prs/deep/p10.webp)](../slides/wait-you-re-still-doing-prs/deep/p10.webp)

*Slide 10: Demo: Markdown directives*

[![Slide 11: Photo 11: Output of atomic intent graph 1: a tree of the intent's tasks, acceptance criteria, scope items, constraints, 12 files, two findings (MissingAttestation, MissingPlanId), identities and a provenance graph.](../slides/wait-you-re-still-doing-prs/deep/p11.webp)](../slides/wait-you-re-still-doing-prs/deep/p11.webp)

*Slide 11: Demo: intent graph tree*

[![Slide 12: Photo 12: Output of atomic intent graph 1 --details: URN identifiers and types for Identity, ProvenanceGraph (blake3-256), Session and SessionTurn, with predicates hasTurn, generatedChange and turnExplainedBy, and views dev and late-morning-ba24 linked by childViewOf.](../slides/wait-you-re-still-doing-prs/deep/p12.webp)](../slides/wait-you-re-still-doing-prs/deep/p12.webp)

*Slide 12: Demo: graph details*

[![Slide 13: Photo 13: HTML graph of the change record: Intent 1, 0 implementing, 1 intent-artifact recording, 1 dependency-only change. Legend of node types: AcceptanceCriterion, Change, Constraint, FeatureIntent, File, Finding, Identity, ProvenanceGraph, ScopeItem, Session, SessionTurn, Task, View.](../slides/wait-you-re-still-doing-prs/deep/p13.webp)](../slides/wait-you-re-still-doing-prs/deep/p13.webp)

*Slide 13: Demo: graph view*

[![Slide 14: Photo 14: Node details for one change: a BLAKE3-256 content address, type atomic.dev/ns/workflow#Change, source vcs, 1 of 1 unique changes with AI provenance, and a cost of \$0.076934 with input, output, reasoning and cache breakdowns.](../slides/wait-you-re-still-doing-prs/deep/p14.webp)](../slides/wait-you-re-still-doing-prs/deep/p14.webp)

*Slide 14: Demo: a change's cost*

[![Slide 15: Photo 15: A new OpenCode session asks for a reviewer grant for the current view.](../slides/wait-you-re-still-doing-prs/deep/p15.webp)](../slides/wait-you-re-still-doing-prs/deep/p15.webp)

*Slide 15: Demo: asking for a reviewer*

[![Slide 16: Photo 16: Reviewer grant for the current view: read and record only, 1-hour lifetime, no existing agents or delegation certificates. The agent asks to confirm the target view, a non-author reviewer with a separately provisioned directory, a change budget, and approval including revocation and retirement of the disposable reviewer key. The grant will not authorize insertion into the target.](../slides/wait-you-re-still-doing-prs/deep/p16.webp)](../slides/wait-you-re-still-doing-prs/deep/p16.webp)

*Slide 16: Demo: reviewer grant terms*

[![Slide 17: Photo 17: The review stops: both author sessions are still active and lack the completion signatures Atomic requires. The agent did not delete anything, bypass the gate or create a VM or production grant. Still outstanding: connect the CLI's changed files to the original intent and complete an independent review. No repository files changed; nothing was inserted into dev. 88.9K tokens, \$0.43.](../slides/wait-you-re-still-doing-prs/deep/p17.webp)](../slides/wait-you-re-still-doing-prs/deep/p17.webp)

*Slide 17: Demo: the gate holds*
