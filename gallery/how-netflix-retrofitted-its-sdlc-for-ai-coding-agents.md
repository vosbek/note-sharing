---
title: "Slides: How Netflix Retrofitted Its SDLC for AI Coding Agents"
---

# Slides: How Netflix Retrofitted Its SDLC for AI Coding Agents

[Back to the notes](../talks/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents.md)

[![Slide 1: How Netflix retrofitted its SDLC for AI coding agents. Mark Khuzam, Software Engineer, Commerce at Netflix. QCon San Francisco, Nov 18, 2026.](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s01.webp)](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s01.webp)

*Slide 1: Title*

[![Slide 2: A mock email titled AI is here, to engineering-all at 9:02 AM: We've just purchased Claude Code for all of engineering. You can use AI to write your code now. Let us know how much faster you're shipping.](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s02.webp)](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s02.webp)

*Slide 2: The email*

[![Slide 3: Agents promised speed. But we spent 20 years building for humans.](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s03.webp)](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s03.webp)

*Slide 3: Agents promised speed*

[![Slide 4: Commerce supports every step of the member lifecycle. 300M+ members, 190 countries, \$45B+ revenue a year, beside a Netflix signup page.](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s04.webp)](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s04.webp)

*Slide 4: Commerce at Netflix*

[![Slide 5: Commerce, a dense graph of dozens of connected services.](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s05.webp)](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s05.webp)

*Slide 5: The service graph*

[![Slide 6: Server Driven UI. API Gateway to Screen Composition, which serves iOS, Android, Web and TV.](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s06.webp)](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s06.webp)

*Slide 6: Server-driven UI*

[![Slide 7: One codebase. Screen Composition: context engineering, loops.](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s07.webp)](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s07.webp)

*Slide 7: One codebase*

[![Slide 8: Context Engineering. Getting what engineers know into what agents see.](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s08.webp)](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s08.webp)

*Slide 8: Context engineering*

[![Slide 9: Writing new code to migrate old code to enable more code. As the product grows, we build the foundation that supports it.](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s09.webp)](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s09.webp)

*Slide 9: Migrations*

[![Slide 10: Failing Forward. Attempt 1: migrate this file. Attempt 2: plus instructions. Attempt 3: plus the APIs to use. Attempt 4: plus how to mock data.](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s10.webp)](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s10.webp)

*Slide 10: Failing forward*

[![Slide 11: Our docs were ok. For humans. Written for humans, hard to find, inconsistent. You had to learn how to write tests here.](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s11.webp)](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s11.webp)

*Slide 11: Docs were ok, for humans*

[![Slide 12: -3. Net Promoter Score: how likely someone would recommend building on it.](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s12.webp)](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s12.webp)

*Slide 12: NPS of -3*

[![Slide 13: From one test to a whole feature. Screen, Data, Route, Test. We had to teach the agent how we build here.](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s13.webp)](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s13.webp)

*Slide 13: One test to a whole feature*

[![Slide 14: Entropy. Many ways to do the same thing. What stays? What goes? What confuses agents and humans?](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s14.webp)](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s14.webp)

*Slide 14: Entropy*

[![Slide 15: Architecture Decision Records. Context, Decision, Pattern and anti-pattern, AI usage notes (what an agent should do), Metadata (related docs, ADRs, code).](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s15.webp)](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s15.webp)

*Slide 15: ADR template*

[![Slide 16: Documentation. 45 architecture decision records, each written for people and for agents. 300+ docs: Docs, Tutorials, Server API, Client API, TV, Web, Mobile, Recipes.](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s16.webp)](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s16.webp)

*Slide 16: 45 ADRs, 300+ docs*

[![Slide 17: Finding the context, 45 ADRs and 300+ docs. AGENTS.md read first (robots.txt), the index of what's where (sitemap.xml), the one doc read in full (the page), then the code. Make it easy to find how to do it.](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s17.webp)](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s17.webp)

*Slide 17: Finding the context*

[![Slide 18: Simplifying. Before: five ways to do one thing. Goal: one way. Agents migrate, people review. Decide what you want agents to do. Then tell them.](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s18.webp)](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s18.webp)

*Slide 18: Simplifying*

[![Slide 19: ADRs now ship inside almost every repo.](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s19.webp)](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s19.webp)

*Slide 19: ADRs in every repo*

[![Slide 20: Loops. An agent writes code. What does it do with it?](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s20.webp)](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s20.webp)

*Slide 20: Loops*

[![Slide 21: Loops inside loops. Release: canary on 10% of traffic, the RCA agent reports. After merge: docs follow. Fix: a comment or the revise label. Review: the CI agent pre-reviews. Every PR: build, lint and tests. Local: write, test, repeat.](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s21.webp)](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s21.webp)

*Slide 21: Loops inside loops*

[![Slide 22: Our CI loop is still deterministic. 1 Build and lint, 2 Unit tests, 3 Integration tests, 4 Screenshot diffing, 5 Merge queues, 6 Canaries.](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s22.webp)](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s22.webp)

*Slide 22: CI is deterministic*

[![Slide 23: Agentic Review. 1 Check the diff against our docs and ADRs. 2 Flag blockers: code that uses an anti-pattern. 3 Look downstream: what depends on this change?](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s23.webp)](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s23.webp)

*Slide 23: Agentic review*

[![Slide 24: Verified blockers only. First version: 23 comments of suggestions and nits. Now: one blocking finding with evidence (the confirm screen drops the local currency format), a fix (use the formatted price the service sends) and the rule (Pricing ADR).](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s24.webp)](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s24.webp)

*Slide 24: Verified blockers only*

[![Slide 25: The agent fixes it. The engineer owns it. The agent reads the PR description, diff, review and comments; the revise label triggers it; it pushes to the same PR; the engineer reviews it. Never auto-merged.](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s25.webp)](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s25.webp)

*Slide 25: The revise label*

[![Slide 26: Docs follow the merge. Review checks whether a doc is now stale; merge is labelled if stale; a docs PR follows in the same PR or after merge. About 9% of merged PRs needed a docs update. ADRs stay human-owned.](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s26.webp)](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s26.webp)

*Slide 26: Docs follow the merge*

[![Slide 27: The agent reports. The engineer ships. Release, canary on 10% of traffic, RCA agent studies the results, the engineer decides if it ships. It compares historical error rates with new errors from this release.](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s27.webp)](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s27.webp)

*Slide 27: The engineer ships*

[![Slide 28: More changes, zero Sev 1s. 0 Sev 1 incidents in 2026 on a core service, +32% pull requests year over year, developer NPS -3 to +25 three quarters apart. A person decided at every step.](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s28.webp)](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s28.webp)

*Slide 28: Results*

[![Slide 29: Ownership. Who owns this context?](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s29.webp)](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s29.webp)

*Slide 29: Ownership*

[![Slide 30: Product engineer. One feature crosses many services, shown as a large service graph.](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s30.webp)](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s30.webp)

*Slide 30: Many services*

[![Slide 31: Portability. How does context follow the work?](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s31.webp)](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s31.webp)

*Slide 31: Portability*

[![Slide 32: Where does context go? Load every repo: dozens of repos, doesn't fit. Git submodules: brittle, extra setup for everyone. A Git MCP server: sees one file, not the system. A shared repo plus copies: goes stale, many copies, many truths.](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s32.webp)](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s32.webp)

*Slide 32: What failed*

[![Slide 33: What we needed. More than anything, accurate: the right context, and it's correct. Portable: any agent, in any environment. Per domain: the team decides what's in it. Fresh: keeps up with the code.](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s33.webp)](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s33.webp)

*Slide 33: What they needed*

[![Slide 34: GraphRAG per domain. Parse (AST: symbols, calls, imports), Extract (semantic extraction from docs and ADRs), Group (community labels, one namespace per domain), Serve (one MCP tool, ask; each build pins commits). Structure from the code. Meaning from the docs.](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s34.webp)](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s34.webp)

*Slide 34: GraphRAG per domain*

[![Slide 35: Any agent can ask. Payments repos feed the payments graph at one MCP address, queried by local agents (Claude Code, Cursor, Codex), a Slack bot and CI review. Every answer cites a file and a line.](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s35.webp)](../slides/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents/deep/s35.webp)

*Slide 35: Any agent can ask*
