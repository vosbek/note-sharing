---
title: "Slides: Observability: The Missing Control Plane for Agentic Engineering"
---

# Slides: Observability: The Missing Control Plane for Agentic Engineering

[Back to the notes](../talks/observability-the-missing-control-plane-for-agentic-engineering.md)

[![Slide 1: Title: the missing control plane for agentic engineering](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s01.webp)](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s01.webp)

*Slide 1: Title: the missing control plane for agentic engineering*

[![Slide 2: What we'll cover today](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s02.webp)](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s02.webp)

*Slide 2: What we'll cover today*

[![Slide: Monitoring is not observability. Known-unknowns: monitoring answers the questions we knew to ask, through dashboards and alerts set up in advance. Unknown-unknowns: observability provides the evidence to investigate questions we didn't know we would have.](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s03.webp)](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s03.webp)

*Slide 3: Known-unknowns versus unknown-unknowns.*

[![Slide: Instrumentation is not capability. Tools can provide the instrumentation (query, traces, metrics, logs). Capability is being able to ask questions when something unexpected happens. Rule of thumb: if answering a new question means adding a new field and redeploying, you have monitoring, not observability.](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s04.webp)](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s04.webp)

*Slide 4: Instrumentation alone doesn't give you the capability.*

[![Slide 5: Why isn't this a solved problem?](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s05.webp)](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s05.webp)

*Slide 5: Why isn't this a solved problem?*

[![Slide: Adoption isn't maturity. 60% self-describe their observability as mature or expert; only 15% have demonstrably reduced MTTR; 51% are still in the early stages. Most teams say they are mature. Few can show it in their results.](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s06.webp)](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s06.webp)

*Slide 6: Self-rating versus outcomes.*

[![Slide: Why is it so hard to get right? Observability is fundamentally a data problem, often handed to teams not specialised for data. It takes data collection, data quality, query-ready storage, exploratory analysis. We ask platform engineers (infrastructure backgrounds) and app developers (web apps, APIs). Whole companies sell this. It's hard, and it's outside our skill sets.](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s07.webp)](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s07.webp)

*Slide 7: A data problem handed to non-data teams.*

[![Slide 8: Who owns observability?](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s08.webp)](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s08.webp)

*Slide 8: Who owns observability?*

[![Slide: Three teams, one capability. App team instruments and investigates; platform team owns the platform and admin; observability team often monitoring, renamed. Where it breaks down: confusion, least privilege, operational risk. Embed the specialists. Upskill the app teams.](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s09.webp)](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s09.webp)

*Slide 9: Three teams with a stake in one capability.*

[![Slide: How much to collect? Curated: cheap, predictable, sees only what you predicted. Everything: costly, disconnected, volume without context. Wide events: rich context per event, sampling controls volume. Curate the shape of the data, not the questions. Telemetry is lossy: drops peak under load, measure them. Cost comes from verbose logs, not wide events.](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s10.webp)](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s10.webp)

*Slide 10: Curate the shape of the data, not the questions.*

[![Slide: Deterministic tests, probabilistic systems. Deterministic code: predefined tests and gates build confidence before release; they catch the failures someone anticipated. Non-deterministic agents: agents change the code, the tests and the deployment process itself; the same input can give different results.](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s11.webp)](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s11.webp)

*Slide 11: Deterministic tests guarding probabilistic systems.*

[![Slide 12: Non-deterministic systems need more rigour](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s12.webp)](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s12.webp)

*Slide 12: Non-deterministic systems need more rigour*

[![Slide: Testing in production. What it looks like: canary releases; feature flags and dark launches; blue-green deploys with fast rollback; chaos engineering and game days; SLOs and error budgets. We know what to do, but few report doing it: while 30% use microservices, only 7-8% have adopted advanced practices like chaos engineering or immutable infrastructure. All of it depends on observability to see what actually happened.](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s13.webp)](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s13.webp)

*Slide 13: We know what to do; few do it.*

[![Slide 14: Maturity of the individual (Shapiro)](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s14.webp)](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s14.webp)

*Slide 14: Maturity of the individual (Shapiro)*

[![Slide 15: Maturity of the system (Eledath)](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s15.webp)](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s15.webp)

*Slide 15: Maturity of the system (Eledath)*

[![Slide: Maturity is the individual and the system. Shapiro levels L0 to L5 mapped to Eledath levels L1 to L8. Shapiro scales the human; Eledath scales what is built around the agent.](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s16.webp)](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s16.webp)

*Slide 16: Shapiro and Eledath side by side.*

[![Slide: Both models stop at the platform edge. Covered by Shapiro and Eledath, how the software gets built: rung 1 AI-assisted not agentic, rung 2 local agents AI-written tests, rung 3 beginner software factory, rung 4 autonomous software factory. Covered by neither model, the agent meets the platform: rung 5 reads the platform, rung 6 makes write requests human reviewed, rung 7 platform changes policy-approved, rung 8 earned autonomy (outlook).](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s17.webp)](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s17.webp)

*Slide 17: Her ladder, with the platform edge.*

[![Slide: Agent first, trace the scenario. Trace the whole scenario: intent, plan, tool calls, approval, artifacts, change, rollback. On every span: user, agent, tool, model, versions, scope, cost, latency, error, policy decision. More autonomy needs more evidence: rung 5 reads the platform worth tracking, rung 6 a reviewer sees the proposal, rung 7 a policy judges it, rung 8 autonomy granted on traces.](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s18.webp)](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s18.webp)

*Slide 18: Trace the whole scenario; more autonomy needs more evidence.*

[![Slide: Agent first, version changes are releases. Prompt: owned by the app team, same code new behaviour. Tools: owned by the platform, changed responses shift plans. Model: moved behind the gateway, hits every agent at once. A version change is a release. Ship it like one. Canary, compare, roll back per version on a slice of traffic. Drift revokes autonomy per capability, as on rung 8.](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s19.webp)](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s19.webp)

*Slide 19: Prompt, tool and model changes ship like releases.*

[![Slide 20: Agent first: sample the behaviour](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s20.webp)](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s20.webp)

*Slide 20: Agent first: sample the behaviour*

[![Slide 21: Agent first: measure the scenario](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s21.webp)](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s21.webp)

*Slide 21: Agent first: measure the scenario*

[![Slide: Agent first, one scenario end to end. On-call engineer asks: does search-api in prod still match its spec? Intent recognised as a drift check; contract: one drift-check tool not ten API calls; identity: read-only for the engineer; state: spec versus live telemetry; evals: golden tasks for known drift verified against ground truth; answer: each gap is fix or update the spec. One trace: user, agent, tool, scope, session, cost.](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s22.webp)](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s22.webp)

*Slide 22: A drift check as a governed, traceable chain.*

[![Slide: No bottleneck, composability through tiers. The platform supplies the plumbing; no approval is needed per metric. Tier 1 automatic defaults, instant. Tier 2 self-service, hours. Tier 3 bespoke work with the platform team by request, case by case.](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s23.webp)](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s23.webp)

*Slide 23: Three tiers; no ticket per metric.*

[![Slide 24: Monitoring is part of the contract](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s24.webp)](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s24.webp)

*Slide 24: Monitoring is part of the contract*

[![Slide: Three parts, one gap. Capabilities: functions to invoke, such as provision infrastructure, deploy applications, retrieve operational data. Context: what should exist, application metadata, architecture, configuration and change records. Controls: rules that hold, approvals, role-based access, non-human identity and delegated permissions. What's missing: every model of context describes the as-designed state. None tells the agent what is actually running. Production telemetry is the as-built half, and observability reconciles the two.](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s25.webp)](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s25.webp)

*Slide 25: Capabilities, context, controls, and the missing half.*

[![Slide: As-designed versus as-built. From industrial automation: the as-designed drawing says what should exist; the as-built record shows what was actually installed. In a non-deterministic space we only really know this through observability.](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s26.webp)](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s26.webp)

*Slide 26: The drawing and the building never quite match.*

[![Slide 27: Closing the loop](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s27.webp)](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s27.webp)

*Slide 27: Closing the loop*

[![Slide: Ambient, not dark. 1 failure: meets a failure no test anticipated. 2 investigate: queries production telemetry, not the test suite. 3 resolve: fixes the defect, or updates the spec when production is right. 4 escalate: hands over to a human with what it found and couldn't confirm. Autonomy is set per decision. The goal isn't a dark factory that operates without people. It's an ambient factory: it acts when the evidence supports it, and knows when to ask for help.](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s30.webp)](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s30.webp)

*Slide 30: Failure, investigate, resolve, escalate.*

[![Slide: Monday morning. 01 put versions and scenario IDs on every span. 02 give teams a self-service path to new signals. 03 set autonomy per capability, based on evals. 04 teach your teams data skills.](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s31.webp)](../slides/observability-the-missing-control-plane-for-agentic-engineering/deep/s31.webp)

*Slide 31: Four things to start on Monday.*
