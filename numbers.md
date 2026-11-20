---
title: "Numbers I checked"
---

# Numbers I checked

Every figure quoted in the 21 talks, 318 in all, with the source I checked it against and what I found. Speakers' numbers lose their conditions as they get repeated; this page keeps them.

**Status:** *Checked* means the same figure is in the source. *Caveat* means it holds with a condition, stated in the row. *Slide only* and *Talk only* mean it came from the slide or the room and I could not confirm it. *Vendor's own* means the company measured itself.

Checked: 118 · Slide only: 93 · Caveat: 64 · Talk only: 35 · Vendor's own: 8

## [The Harness Is the New Operating System](talks/the-harness-is-the-new-operating-system.md)

| Claim | Figure | Source | Status |
|---|---|---|---|
| Same model across 8 harnesses, DeepSWE v1.1 | 65.5–74.2% | [DeepSeek V4.1-Flash model card](https://deepinfra.com/deepseek-ai/DeepSeek-V4.1-Flash), [summary](https://datanorth.ai/news/deepseek-releases-deepseek-v4-1-flash) | Caveat vendor-run, one model |
| Manager-worker scaffold, Qwen3.8-27B | 66.8 → 92.4% | [GVS5H, arXiv 2608.26480](https://arxiv.org/abs/2608.26480) | Caveat 10 rounds vs one call |
| Agents edit or delete tests to pass | n/a | [ImpossibleBench, arXiv 2510.20270](https://arxiv.org/abs/2510.20270) | Checked |
| OpenAI eval agents reached Hugging Face production | Jul 2026 | [BleepingComputer](https://www.bleepingcomputer.com/news/security/openai-says-its-ai-models-hacked-hugging-face-during-testing/), [CSA research note](https://labs.cloudsecurityalliance.org/wp-content/uploads/2026/08/CSA_research_note_agentic_ai_self_attack_systemic_risk_20260816-csa-styled.pdf) | Checked |
| Claude Code permission prompts approved | 97% | [Anthropic, auto mode post](https://claude.com/blog/auto-mode-default-in-claude-code) | Checked |
| Interactive sessions started with checks off (June 2026) | 25% | [Implicator, citing Anthropic](https://www.implicator.ai/anthropic-claude-code-auto-mode-default/) | Checked |
| Dangerous commands caught: people vs classifier | 13.6% vs 89% | [InfoWorld, citing Anthropic (1,053 testers)](https://www.infoworld.com/article/4207959/anthropic-makes-claude-codes-auto-mode-default-for-paid-users.html) | Caveat controlled study |
| Fewer permission prompts after sandboxing | 84% | [Anthropic, Beyond permission prompts](https://www.anthropic.com/engineering/claude-code-sandboxing) | Checked |
| Plain shell vs agent-designed interface | 11.0 → 18.0% | [SWE-agent, arXiv 2405.15793](https://arxiv.org/abs/2405.15793) | Slide only 2024 models |
| Multi-agent vs single agent | +80.8% / −70% | [Kim et al., arXiv 2512.08296](https://arxiv.org/abs/2512.08296) | Checked |
| 20 steps at 95% each; with 80% of errors caught | 36% → 82% | Arithmetic | Checked 35.8%, 81.8% |
| Context anxiety in Sonnet 4.5, gone in Opus 4.5 | n/a | [Anthropic, Harness design for long-running apps](https://www.anthropic.com/engineering/harness-design-long-running-apps) | Checked |
| Harness-only gains, GPT-5.2-Codex, Terminal-Bench 2.0 | 52.8 → 66.5% | [LangChain](https://blog.langchain.com/improving-deep-agents-with-harness-engineering) | Checked |

## [Running Software Factory Efficiently at Uber Scale: Holding Agent Spend Steady While Requests Grew 9X](talks/running-software-factory-efficiently-at-uber-scale.md)

| Claim | Figure | Source | Status |
|---|---|---|---|
| PRs attributed to local or cloud agents | 70%+ | Slide 2; [Uber blog](https://www.uber.com/blog/efficient-software-factory/) | Checked |
| PRs written end to end by autonomous agents | ~20% | Recording | Talk only |
| Agent skills built | 5,000+ | Slide 2; [session page](https://qconsf.com/presentation/nov2026/running-software-factory-efficiently-uber-scale-holding-agent-spend-steady) | Checked |
| Skill executions per day | 33K+ | Slide 2; [Uber blog](https://www.uber.com/blog/efficient-software-factory/), Aug: 30K+ | Checked |
| MCP servers behind one gateway | 1,000+ | Slide 2; [Uber blog](https://www.uber.com/blog/efficient-software-factory/) | Checked |
| Weekly active users, Feb 2 to Oct 19 | +7x | Slide 4; [Uber blog](https://www.uber.com/blog/efficient-software-factory/) (7x to Aug) | Checked |
| Weekly agent requests, Feb 2 to Oct 19 | +15x | Slide 4; blog gives 9.4x to Aug | Caveat longer window; schedule title says 9X |
| Weekly spend | Levelled off ~May | Slide 4 chart; blog says April, session page May | Caveat dips in Jul, new high in Sep |
| Cost per 1,000 requests; cost per session | −34%; −52% | [Uber blog](https://www.uber.com/blog/efficient-software-factory/) | Caveat to Aug, model held constant; not on captured slides |
| Graded benchmark tasks | 1,075 | Slide 11 (Go 363, Java 416, Python 296; sums to 1,075); session page | Checked |
| Time to run one model on the benchmark | 3 days → ~1 h | Slide 12 | Slide only |
| Cost of the top score vs the 1x setting | 7x for +0.019 | Slide 29 | Slide only |
| Context cap on 1M-token models | 400K | Slide 16; [Uber blog](https://www.uber.com/blog/efficient-software-factory/) | Checked |
| Input tokens per request after the defaults | ~−15% | Slides 16, 29 | Slide only |
| Default reasoning effort | Medium (was High) | Slide 16; [Uber blog](https://www.uber.com/blog/efficient-software-factory/) | Checked |
| Output price vs input on frontier models | 5x | Slide 16; [Claude models](https://platform.claude.com/docs/en/about-claude/models/overview) (\$5 in, \$25 out per MTok on Opus) | Checked for Claude |
| Main-thread cache cost with a 1-hour TTL | −39% | Slide 16 | Slide only |
| Cache write 5 min / 1 h; read | 1.25x / 2x; 0.1x | Slide 16; [Anthropic prompt caching](https://platform.claude.com/docs/en/build-with-claude/prompt-caching) | Caveat reads 0.05x on Opus 5.5 and Sonnet 5.5 |
| Subagents finish within | 90 s | Slide 16 | Slide only |
| Tool schemas with 100+ tools | 50–70K tokens | Slide on tool schemas; [Uber blog](https://www.uber.com/blog/efficient-software-factory/) | Checked |
| Startup context after tool search | −60% | Slides on tool schemas and 29 | Slide only |
| Workspace server: tools, schema tokens | 49; ~22K | Slide 18; [Uber blog](https://www.uber.com/blog/efficient-software-factory/) | Checked |
| Five SaaS servers: schemas, tokens kept out | 173; ~57K | Slide 18 (49+46+34+28+16 = 173) | Slide only |
| Code mode: model turns; tokens | 3–7 → 1; ~400 | Code-mode slide | Slide only |
| Code mode token reduction | 55–71% | Slide 29; [Uber blog](https://www.uber.com/blog/efficient-software-factory/) table (4 of 5 queries) | Checked |
| Context graph nodes; edges | 55M+; 195M+ | Graph slide; blog in Aug: 24M; 80M | Caveat grown since Aug; slide only |
| One question, without vs with the graph | 20m 09s → 38s | Graph slide; [Uber blog](https://www.uber.com/blog/efficient-software-factory/) | Checked |
| 68 questions: judge, cost, time | +8.3%, −31%, −49% | Graph slide | Caveat Uber-run, same model; slide only |
| Session analysis checks | 18 | Slides 27–29 (2+2+9+5); blog in Aug: 16 | Slide only |
| Spend nudges | 50, 80, 100% | Slide 26; [Uber blog](https://www.uber.com/blog/efficient-software-factory/) | Checked |
| Cache-miss warning example | +\$4.19 | Recording | Talk only |
| First MCP gateway | Apr–May 2025 | Recording | Talk only |
| Automated migrations; lines | 200–250; ~12M | Recording; [AI Engineer talk](https://ai.engineer/talks/17-YSUHo6Lk-agentic-sdlc-at-uber-building-blocks-ubers), Aug: 250+; 9M | Caveat newer, unpublished |
| Years at Uber | 11 | [Pragmatic Engineer](https://newsletter.pragmaticengineer.com/p/ubers-ai-infra-from-the-inside): joined 2015 | Checked |

## [Beyond the Model: Engineering the Agent Harness for Autonomous Software Delivery](talks/beyond-the-model-engineering-the-agent-harness.md)

| Claim | Figure | Source | Status |
|---|---|---|---|
| Bob users inside IBM; average productivity gain | 80,000+; 45% | [IBM newsroom, Apr 28, 2026](https://newsroom.ibm.com/2026-04-28-introducing-ibm-bob-ai-development-partner-that-takes-enterprises-from-ai-assisted-coding-to-production-ready-software) | Caveat Self-reported by surveyed IBM users. IBM’s blog footnotes it only as “IBM Internal Data”, with no baseline or sample size. |
| Reported productivity range across SDLC tasks | 20–80% | Slide 17 | Slide only Range not found in IBM’s public material. |
| Faster complex delivery; efficiency in structured workflows | 20–40%; 50–80% | Slide 17 | Slide only |
| Lower AI compute cost than calling a model directly | ~40% | Slide 17 (“source claims”) | Slide only [IBM’s blog](https://www.ibm.com/new/announcements/shifting-from-ai-assisted-coding-to-ai-assisted-delivery-with-ibm-bob) gives no cost figures. |
| Security outcomes | none | Slide 17 | Slide only The slide itself says “no quantified rate supplied”. |
| Context window per conversation | 270,000 tokens | Slide 11; [Multishoring on Bob V2](https://multishoring.com/blog/from-hackathon-demo-to-enterprise-use-case-ibm-dev-day/) | Caveat Third-party write-up describes 270K isolated context per subagent. |
| Generally available; internal start | Apr 28, 2026; Jun 2025 (100 devs) | [IBM UK newsroom](https://uk.newsroom.ibm.com/Introducing-IBM-Bob-AI-Development-Partner) | Checked |
| List prices (not shown in the talk) | Pro \$20 / 50 coins; Pro+ \$60 / 180; Ultra \$200 / 1,000 | [bob.ibm.com/pricing](https://bob.ibm.com/pricing) | Caveat Indicative and per month. Enterprise pricing is by quote. At launch it was \$20 for 40 coins and \$200 for 500, about \$0.50 a coin ([The Register](https://www.theregister.com/2026/04/28/ibms_ai_coding_partner_bob/)). |
| Premium packages | DevSecOps \$20, Java \$20, IBM i \$40, Z enterprise only | [bob.ibm.com/pricing](https://bob.ibm.com/pricing) | Checked Per month, indicative. |
| Demo account budget | 250 coins; 52.33 used (21%) | Slide 26 | Slide only An IBM internal account. |
| Time to generate diagrams; to run the audit | ~7–10 min; 10–13 min | Spoken during recorded demos | Speaker only Not timed live. |
| Controls checked by the audit skill | 7 (ASVS Level 1) | Slide 23 | Slide only Control IDs match ASVS 4.0.3 numbering. |

## [Stop Fighting the Remodel: API Design for Models That Outgrew Their Boundaries](talks/stop-fighting-the-remodel.md)

| Claim | Figure | Source | Status |
|---|---|---|---|
| Apps consuming CBP Foundations’ data | 100+ | Slides 12, 59 | Slide only |
| Person records in Entity Services | 1.7M | Slide 13 (the recording says 17 million) | Slide only |
| Vendor records | 225K | Slide 13 | Slide only |
| Requests per second; share of calls under 1 s | 10K–20K; 99% | Recording; charts on slides 14–15 unreadable | Talk only |
| Connections for 100 apps × 5 domains | 500 | Slide 32; 100 × 5 = 500 | Checked |
| Scale of the federated graph | “4,000” | Slide 34 gives no unit; said as microservices. [InfoQ, 2022](https://www.infoq.com/news/2022/10/scaling-graphql-netflix/): 10,000+ types and fields, 500+ developers | Caveat unit unclear; not matched in any source |
| Requests per day through the graph | 1B+ | Recording; [InfoQ, 2022](https://www.infoq.com/news/2022/10/scaling-graphql-netflix/) | Checked |
| Federation open-sourced | 2020 | [Netflix TechBlog, Nov 2020](https://netflixtechblog.com/how-netflix-scales-its-api-with-graphql-federation-part-1-ae3557c187e2); DGS open-sourced [early 2021](https://www.infoq.com/news/2021/02/netflix-graphql-spring-boot/) | Caveat the post was 2020; the framework 2021 |
| p99 latency, before and after batch loading | 7.2 s → ≤1.4 s | Slide 40 (the recording says 24 s, an error) | Slide only |
| Drop in tail latency | ~80% | Recording; (7.2 − 1.4) / 7.2 = 81% from slide 40 | Checked arithmetic |
| Calls before and after; calls over 2 s | 396 → 78; 66 → 0 | Slide 41; 66 / 396 = 16.7%, shown as 17% | Slide only |
| Lower cost after the fix | ~20% | Recording | Talk only |
| RAW Hollow: in-memory, co-located, strong consistency available | n/a | [Netflix TechBlog on Tudum](https://netflixtechblog.com/netflix-tudum-architecture-from-cqrs-with-kafka-to-cqrs-with-raw-hollow-86d141b72e52) | Checked |
| UDA built on RDF and SHACL; projects to GraphQL, Avro, Iceberg | n/a | [Netflix TechBlog, June 2025](https://netflixtechblog.com/uda-unified-data-architecture-6a6aee261d8d) | Checked |
| Agent calls, all reads | 300K | Slide 57; “last 180 days” from the recording | Slide only |
| Agent writes, synthetic test data | 6,000 | Slide 57 | Slide only |
| Consumers migrated vs not yet | 62 / 38 | Recording; slide not captured | Talk only |
| Roof leaks found; year | 7+; Oct 2024 | Slides 3, 5 (an earlier draft from the recording said 2020) | Slide only |
| *Microservices Patterns* publication year | 2018 | Slide 26; [O’Reilly listing, Nov 2018](https://www.oreilly.com/library/view/-/9781617294549) | Checked |

## [Generation Got Cheap, Trust Didn't: Scaling Agentic Changes from Prompt to Prod at Roblox](talks/generation-got-cheap-trust-didnt.md)

| Claim | Figure | Source | Status |
|---|---|---|---|
| AI review precision (flag led to a code change) | 72% | Slide 11+. Roblox has published other acceptance figures on different measures: about 30% to over 60% for AI PR suggestions across 10,000 PRs ([Roblox blog, Jan 12, 2026](https://about.roblox.com/newsroom/2026/01/doubled-ai-code-acceptance-teaching-models-think-like-roblox-engineers)) and about 20% at first, nearly 70% later, for AI review comments ([DX podcast with Andrew Swerdlow](https://getdx.com/podcast/robloxs-approach-to-tripling-ai-code-review-acceptance-rates/)). | Caveat |
| Precision roughly tripled since launch | ≈3x | Talk; starting figure garbled in the transcript. 20% to 72% would be 3.6x. Consistent with the DX podcast title. | Caveat |
| AI review recall (clean sign-off held up) | 88% | Slide 11+ | On slide |
| PRs reviewed by the agent | 400,000+ | Recording. The DX podcast says “many thousands of PRs per day” and about 5% auto-merged. | Talk only |
| Review history mined | 700K PRs, 1.7M comments | [Roblox blog](https://about.roblox.com/newsroom/2026/01/doubled-ai-code-acceptance-teaching-models-think-like-roblox-engineers): PRs merged over three years; comments from experienced reviewers | Checked |
| Curated eval set | 600+ PRs: ~500 catch, 100+ silent | Slide 11+ | On slide |
| Review harness efficiency | 38x reviews/host, ~97% less memory | Slide 11+ | On slide |
| Review cost reduction from harness and caching | ~86% | Recording; the slide’s figure is cut off and starts with “8”. 86% is about 7x cheaper. The DX podcast cites a 90% cut in the cost of each exemplar evaluation through caching. | Caveat |
| Prompt cache pricing behind the pre-warm trick | write 1.25x · read 0.1x | [Anthropic pricing](https://platform.claude.com/docs/en/about-claude/pricing) (5-minute writes; 1-hour writes 2x; some newer models read cheaper). Kushan didn’t name a provider. Our arithmetic in section 03. | Checked |
| AI line edits fleet-wide, 14 days | ~10⁸ | Slide 18 | On slide |
| Merged lines per day | 500K+ | Slide 18 | On slide |
| Weekly AI traffic | ~250M calls · 3T+ tokens · 1M+ conversations | Slide 24. The transcript’s token figure is garbled; the slide wins. | On slide |
| Agents and models | 100+ production agents (2x in 3 months) · 12 coding agents · 50 models | Slide 24 | On slide |
| Existing OTel pipeline throughput | 10M+ msgs/sec | Slide 25 | On slide |
| Cost per token | halved, usage \>2x | Slide 26 | On slide |
| One workload switched to a cheaper model | \$2M/yr | Slide 26 | On slide |
| Disabling MCP eager loading | 15% of coding-agent spend | Slide 26. Claude Code’s own docs say tool search, which defers MCP tool definitions, is [on by default](https://code.claude.com/docs/en/agent-sdk/tool-search), with exceptions. Which agent Roblox changed wasn’t named on the slide. | Caveat |
| Prompts judged a day | ~9M | Recording | Talk only |
| Judge pipeline | 12–28x less data · ~15 min · 19 judges · 50x cheaper | Slide 28. 50x is smallest model versus frontier on everything. | On slide |
| Offline eval cases | 900+ in 7 weeks (52, 87, ~800) | Slide 29 | On slide |
| Team size | 15–20 people, several months | Recording, Q&A estimate | Talk only |

## [Into the Labyrinth: What Distributed Systems Have Taught Us About Guardrails](talks/into-the-labyrinth.md)

| Claim | Figure | Source | Status |
|---|---|---|---|
| Issues Jepsen found in ParticleDB | 96 | [Jepsen](https://jepsen.io/), Oct 31, 2026 | Caveat single node; Orkes-funded |
| Issues outside healthy single-node runs | 3 | Jepsen report, slide 8 | Checked |
| Typical Jepsen findings and duration | 10–30 / 2.5–4 wk | Speaker | Speaker only |
| Failures studied / catastrophic | 198 / 48 | [Yuan et al., OSDI 2014](https://www.usenix.org/conference/osdi14/technical-sessions/presentation/yuan) | Checked |
| Failures reproducible by a unit test | 77% | Yuan et al., Finding 9 | Checked |
| Catastrophic failures from mishandled flagged errors | 92% | Yuan et al. | Checked not on a slide |
| DST invented independently at AWS and FoundationDB | 2000s | Slide 35 | Slide only |

## [Wait, You're Still Doing PRs?](talks/wait-you-re-still-doing-prs.md)

| Claim | Figure | Source | Status |
|---|---|---|---|
| Anthropic replaced Git with Scion as merges grew | 2,500 → 30,000+ a day | [Anthropic engineering, Oct 13, 2026](https://anthropic.com/engineering/redesigning-source-control); coverage reports 7 engineers in 5 months. Lee said “six weeks ago”; it was about five. | Checked |
| OpenAI acquired Pierre “last week” | announced Nov 4 | [Axios via Yahoo Finance](https://finance.yahoo.com/technology/ai/articles/exclusive-openai-targets-microsofts-github-112906674.html); [DevOps.com](https://devops.com/openai-acquires-pierre-computer-to-expand-codex-challenge-github). About 12 days before the talk; deal subject to closing. | Checked |
| OpenAI built a new Git system, heard as “Panda” | Pando | [OpenAI, Scaling Git at OpenAI, Nov 2](https://openai.com/index/scaling-git-at-openai/): median push latency down nearly 80%, close to 1 PB of Git data a day. Name corrected; Pando is a Git backend, not a Git replacement. | Caveat |
| A former GitHub CTO now heads source control at OpenAI | n/a | Not found. Reports name Taylor Blau, a long-time Git contributor formerly of GitHub, among the Pando authors ([Startup Fortune](https://startupfortune.com/openai-built-its-own-git-backend-called-pando-to-survive-a-commit-surge/)). Unverified as stated. | Caveat |
| First pull request, late 2008 or early 2009 | Feb 2008 | [GitHub blog, Feb 23, 2008](https://github.blog/2008-02-23-oh-yeah-there-s-pull-requests-now/). Earlier than he said. | Caveat |
| PR search covers titles and descriptions; code search the default branch only | n/a | Recording | Talk only |
| PRs in a large customer’s org | 150,000 | Recording | Talk only |
| Disk for ten agents in Git worktrees, Rust builds | 500–600 GB | Recording, Atomic’s own demos. Vendor-run. | Talk only |
| GitHub Enterprise in 2015: hot/warm HA, one writable server | n/a | Recording | Talk only |
| Demo: build the CLI | 1m 3s · 14.3K tokens · \$0.08 | Photo 7 | On screen |
| Demo: cost of one change | \$0.076934 | Photo 14 | On screen |
| Demo: review session | 88.9K tokens · \$0.43 | Photo 17. Review did not complete. | On screen |
| Reviewer grant scope | read, record · 1 hour | Photo 16 | On screen |
| Intents one customer created | 30,000 in 2 weeks | Recording | Talk only |
| Atomic is open source, based on patch theory | Apache-2.0 | [github.com/atomicdotdev/atomic](https://github.com/atomicdotdev/atomic). Outposts is commercial. | Checked |
| Agents Atomic integrates with | Claude Code, Copilot, Devin and more | [Atomic docs, agent command](https://docs.atomic.dev/commands/agent). Vendor docs; depth of each integration unknown. | Checked |
| Atomic’s funding | \$2.5M pre-seed | [Vermilion Cliffs Ventures](https://vermilioncliffs.substack.com/p/hello-atomic-goodbye-git-rebuilding). Investor’s own post. | Checked |

## [Learning Out Loud (Under Near-Existential Pressure)](talks/learning-out-loud-under-near-existential-pressure.md)

| Claim | Figure | Source | Status |
|---|---|---|---|
| Heart patients in deep denial did better short term and worse long term | High deniers had fewer days in intensive care and fewer signs of cardiac dysfunction in hospital; denial was maladaptive after discharge | [Levine et al., 1987](https://experts.arizona.edu/en/publications/the-role-of-denial-in-recovery-from-coronary-heart-disease/) | Checked |
| Citation slide gives the journal as Biopsychosocial Science and Medicine | The paper ran in *Psychosomatic Medicine* 49(2); the journal took its new name in 2025 | [SBSM](https://thesbsm.org/?p=478) | Caveat |
| AI doesn’t reduce work, it intensifies it | An eight-month study of about 200 employees at a US tech company: people took on more tasks and longer hours, often unasked | [HBR, Feb 9, 2026](https://hbr.org/2026/02/ai-doesnt-reduce-work-it-intensifies-it) | Checked |
| People told a skill was innate avoided a public-failure learning task | Closest match: incremental theorists were more likely to take remedial action after poor performance. I could not confirm the public-versus-private task design she described | [Hong, Chiu, Dweck et al., 1999](https://rims.cityu-dg.edu.cn/en/publications/implicit-theories-attributions-and-coping-a-meaning-system-approa/) | Caveat |
| The boiling-frog story is debunked | Frogs heated gradually try to escape; moving to regulate temperature is how ectotherms survive | [Wikipedia](https://en.wikipedia.org/wiki/Boiling_frog) | Checked |
| Racehorses share an official birthday | January 1 in the Northern Hemisphere, August 1 in most of the Southern | [Kentucky Derby](https://www.kentuckyderby.com/horses/news/thoroughbred-birthdays-along-the-road-to-the-kentucky-derby/) | Checked |
| She posted her learning session to a 600-person Photoshop channel | Her own account | Recording | Talk only |

## [Skills, Memory, or Fine-Tuning? The Engineering Loop Behind Production Agents](talks/skills-memory-or-fine-tuning.md)

| Claim | Figure | Source | Status |
|---|---|---|---|
| Answer position changes accuracy (GPT-3.5-Turbo, 20 documents) | 75.8% first, 53.8% middle, 56.1% closed-book, 88.3% answer only | [Liu et al., Lost in the Middle](https://arxiv.org/abs/2307.03172) | Checked |
| Performance falls as input grows | Curve values on slide 16 | [Chroma, Context Rot, July 2025](https://research.trychroma.com/context-rot) | Caveat trend checked, slide values not |
| Sub-agents beat one agent | 90.2% better, about 15× the tokens of a chat | [Anthropic, June 2025](https://www.anthropic.com/engineering/multi-agent-research-system) | Caveat Anthropic’s internal research eval |
| Human-written vs AI-written skills | +16.2 vs −1.3 points, 84 tasks | [SkillsBench, Li et al., 2026](https://arxiv.org/abs/2602.12670) | Checked |
| 2 or 3 skills vs 4 or more | +18.6 vs +5.9 points | Slide 33; the paper reports focused 2–3 module skills doing best | Slide only |
| LLM judge agreement with experts | Kappa 0.02 to 0.61; experts 0.69 | [Shopify Engineering](https://shopify.engineering/building-production-ready-agentic-systems) | Checked |
| Models computing tax returns | Fewer than 1 in 3 correct, mid-2025 | [TaxCalcBench, Bock et al.](https://arxiv.org/abs/2507.16126) | Checked |
| Small eval set stands in for a large one | 100 curated vs 14,000 MMLU questions | [tinyBenchmarks, ICML 2024](https://arxiv.org/abs/2402.14992) | Checked |
| A 90% agent at k=3 | 73% (0.9³ = 0.729) | [τ-bench pass^k](https://arxiv.org/abs/2406.12045); arithmetic rerun | Checked |
| 300k tokens is a 25-hour meeting | 300k × 0.75 words ÷ 150 words a minute = 25 hours | Arithmetic rerun on the slide’s assumptions | Checked |
| Agent deleted a production database | 9 seconds, backups included; data later restored | [Decrypt](https://decrypt.co/365897/ai-agent-deletes-startup-database-9-seconds-founder-says), April 2026 | Checked |
| Support bot invented a policy | “One device per subscription”, April 2025 | [CX Today](https://www.cxtoday.com/conversational-ai/a-contact-center-chatbot-invents-company-policies-now-customers-want-out/) | Checked |
| Failure mix, new vs mature agents | Context 37% → 17%; reasoning 7% → 39% | Lucidic deployments | Vendor |
| ServiceNow ticket agent after split and verify | +20 points, 2.0× closed, +15% tokens | Lucidic, slide 27 | Vendor |
| Legal curriculum | 11% to 21%, 24% with post-training | Lucidic, slide 61 | Vendor |

## [Use AI to Multiply Your Team as a Staff Engineer](talks/use-ai-to-multiply-your-team-as-a-staff-engineer.md)

| Claim | Figure | Source | Status |
|---|---|---|---|
| Top 10% merged PRs per engineer per week | 6.7 → 11.3, +68% | Slide 3; 11.3 ÷ 6.7 = 1.69 | Slide only arithmetic checked |
| Bottom half, same measure | 1.0 → 1.15, +14% | Slide 3; the rounded values give +15% | Caveat rounding |
| Top 10% ship about 10× the bottom half | 11.3 ÷ 1.15 = 9.8× | Arithmetic rerun on slide 3 | Checked |
| Cost to load cargo, by hand vs container (1956) | Slide: \$5.86 vs 16¢ a ton | [The Geography of Transport Systems](https://transportgeography.org/contents/chapter1/the-setting-of-global-transportation-systems/idealx-first-containeriship-1956/): McLean’s figure was \$5.83 vs under 16¢ | Caveat source says \$5.83; loading cost only |
| Browser tool start in the sandbox | About 70 s → under 2 s | Slide 22 | Slide only |
| People using the shared skills | About half of engineers; create-pr 861, Slack update 610, diagnose-ci 550 | Slide 27 | Slide only |
| Shared skill users and count | Over 1,000 people, 20+ skills | Spoken in the talk | Talk only |
| Autoship adoption | 28 teams, 400+ merged PRs, launched July | Slide 31; 28 teams also in the session abstract | Slide only |
| Class-component migration speed | 3 to 5× faster than by hand | Slide 43 | Slide only |
| Runaway scheduled job | 16 PRs in 2 minutes; CI start under 30 s → 14 min, about 30× | Slide 45; 14 min ÷ 30 s = 28 | Slide only arithmetic checked |
| End-to-end runs skipped in one week | 130 runs, 82 PRs | Slide 48 (bot report); the audio said 130 PRs | Slide only |
| Engineers with their own scheduler jobs | 40 | Slide 50 | Slide only |
| His output vs his teammates’, 2025 to 2026 | 3× vs 5×, same five teammates | Spoken; the chart on slide 51 has no values | Talk only |
| His team vs other web teams, 2026 | 4× per engineer per month, his PRs excluded | Slide 52 | Slide only |
| Newsletter readership | 100,000 subscribers | [QCon speaker page](https://qconsf.com/speakers/jordancutler) | Checked as stated there |

## [Drawing the Rest of the Owl: A Blueprint for Your Software Factory](talks/drawing-the-rest-of-the-owl.md)

| Claim | Figure | Source | Status |
|---|---|---|---|
| Harness bought Cosmos, Auggie CLI and the Code Context Engine | Announced Oct 8, 2026; terms not disclosed | [Harness blog](https://www.harness.io/blog/harness-acquires-augment-code-cosmos), [Augment blog](https://augmentcode.com/blog/augment-code-next-chapter) | Checked |
| Two reviewers per PR is not a SOC 2 requirement | SOC 2 doesn’t name code review; auditors test the controls you wrote | [Probo](https://www.probo.com/blog/2025-11-09-do-you-need-code-reviews), [Scrums.com](https://www.scrums.com/blog/soc2-engineering-teams) | Caveat your own policy and other regulations still apply |
| Augment’s own factory, Nov 2025 to Jul 2026 | 17,200 merged PRs; size-adjusted output per developer 4.5×; median time to merge 11.2 h → 3.1 h; 14-day revert rate 1.9% → 0.4% | [Augment blog](https://augmentcode.com/blog/beyond-ai-coding-agents-how-we-built-augments-software-factory) | Vendor no control group; model upgrades in the same period |
| Share of Augment’s code reviews run through Cosmos | 97% | [Cosmos product page](https://augmentcode.com/product/cosmos) | Vendor |
| Context Engine MCP improves agent output | 70%+ across Claude Code, Cursor and Codex; 300 Elasticsearch PRs, 900 attempts | [Augment changelog](https://www.augmentcode.com/changelog/context-engine-mcp-in-ga) | Vendor Augment’s own benchmark |
| Auggie CLI cost | Matches Claude Code’s SWE-bench Pro pass rate at 53% lower cost per task | [Harness blog](https://www.harness.io/blog/inside-a-governed-software-factory-with-harness-cosmos) | Vendor |
| Knowledge Graph query cost | About 12K tokens vs 250K+ through raw APIs | [Harness blog](https://www.harness.io/blog/inside-a-governed-software-factory-with-harness-cosmos) | Vendor |
| Augment default model in Cosmos | GPT-5.6 Sol, from July 29, 2026 | [Augment blog](https://www.augmentcode.com/blog/eight-models-in-eight-weeks-gpt-5-6-sol-is-now-our-default) | Checked the talk named a Sol model for review; versions garbled |
| Budget cap example | “Don’t spend more than \$1,000” on one problem, or \$100 | Spoken in Q&A | Talk only illustrative |

## [Lessons from Building a $100M Product in Six Weeks at OpenAI](talks/building-a-100m-product-at-openai.md)

| Claim | Figure | Source | Status |
|---|---|---|---|
| U.S. ads pilot launch | February 9, 2026 | [OpenAI, Testing ads in ChatGPT](https://openai.com/index/testing-ads-in-chatgpt/) | Checked |
| Annualized run rate six weeks after launch | \$100M+ | OpenAI statement in April, [reported by Reuters](https://www.dealstreetasia.com/?p=493737) | Caveat run rate, not collected revenue |
| Annualized run rate under 200 days after launch | \$1B | OpenAI, Aug 31, 2026, [reported by CNBC](https://ppc.land/openais-david-dugan-says-chatgpt-ads-passed-a-1bn-run-rate/) | Caveat run rate, not collected revenue |
| Production code written by people | None | Slide 5; he scoped it to authorship of Ads production code | Talk only |
| Effort split before and with agents | 70/20/10 → 45/35/20 (product, system, maintenance) | Slide 12; his rough estimate | Talk only |
| Routine PR auto-approval target | ≥90% | Slide 17 | Slide only a target, not a measured rate |
| PRs bundled per batch | 30 to 40 | Spoken | Talk only |
| Downtime at 90% uptime | About 17 hours a week | 0.10 × 168 h = 16.8 h; 99.99% is about 1 minute a week | Checked arithmetic |
| Share of his system he understands | 80–90% before, 40–50% on Ads | Q&A | Talk only |
| GPT-6.2 Astra and Sol in Codex | Released Nov 17, 2026 | Slide 5; I couldn’t load OpenAI’s announcement, and reports through Nov 10 said unreleased | Slide only |

## [Bridging Retrieval and Ranking: From LLM Embeddings and Graph Features to a GPU-Served DLRM](talks/bridging-retrieval-and-ranking.md)

| Claim | Figure | Source | Status |
|---|---|---|---|
| Content time spent, online A/B | +2.5% | Slide 5; [preprint abstract](https://arxiv.org/abs/2609.22441); session page | Checked self-reported |
| Recall@10 drop without edge features | −7.86% | Slide 25; preprint abstract | Checked |
| Recall@10 drop without content or item features | −3.05%, −2.5% | Slide 25; preprint ablation | Checked |
| Throughput per GPU | 75 → 700 QPS (9.3x) | Slides 20, 23; the preprint reports relative gains of the same order | Caveat same hardware and model, their workload |
| Batching alone | 75 → 120 QPS (1.6x) | Slide 20; 120 ÷ 75 = 1.6 | Checked arithmetic |
| Scoring budget | p99 ≤ 120 ms | Slides 20, 23; preprint abstract | Checked |
| Index size | 1.3B documents; 400M per H200 | Slides 5, 23; preprint says over one billion, a few hundred million per shard | Checked |
| Doc ID lookup, batch of 8 | 47 ms → 1 ms | Slide 15; preprint | Checked |
| Batch insert speedup | 52x | Slide 15; preprint | Checked |
| Edge join | Up to 200x fewer operations | Slide 17; preprint | Checked |
| Ingestion | ~10⁴ upserts/s, lag under 1 minute | Slides 14, 16; preprint | Checked |
| Ten experiments on one index | 600 → 550 QPS, about 8% | Slide 23; 50 ÷ 600 = 8.3% | Slide only |
| Bigger model trade-off | 75x parameters: +0.20% recall, 0.56x QPS | Slide 24; 1 − 0.56 = 44% less throughput | Checked arithmetic |
| Deployed model size | O(10⁷) parameters | Slide 24; the preprint frames it as a 50x scale-up over the previous model | Slide only exact count not confirmed |
| Lift by connection cohort | +0.58% (under 30) to +3.07% (500–999) | Slide 27 | Slide only |
| End-to-end Feed latency | About 500 ms, retrieval about half | Spoken | Talk only |
| LiNR, the GPU retrieval it builds on | +3% relative professional daily active users | [LiNR, CIKM 2024](https://arxiv.org/abs/2407.13218) | Checked self-reported |
| H200 memory | 141 GB HBM3e at 4.8 TB/s | [NVIDIA](https://www.nvidia.com/h200) | Checked vendor spec |

## [The Execution Muscle: Why Great Teams Are Built, Not Hired](talks/the-execution-muscle-why-great-teams-are-built-not-hired.md)

| Claim | Figure | Source | Status |
|---|---|---|---|
| Organizational performance with a generative culture | +30% | [DORA, Accelerate State of DevOps 2023](https://dora.dev/report/2023) | Caveat survey-based correlation, not a controlled study |
| DORA respondents | 36,000+ | DORA 2023 materials. This is DORA’s total across nine years of research, not the 2023 survey alone | Caveat |
| Project Aristotle teams | 180 (115 engineering) | [Google re:Work](https://rework.withgoogle.com/en/guides/understanding-team-effectiveness); the other 65 were sales pods | Checked |
| Psychological safety as the top dynamic, underpinning the other four | \#1 of 5 | Google re:Work, Julia Rozovsky, 2015 | Caveat Google’s internal teams only; not a peer-reviewed paper |
| Speaker’s experience | 16+ years, 50+ companies | [QCon speaker page](https://qconsf.com/speakers/charlottemestwerdt) | Checked |
| Owning mistakes makes leaders look more respected | n/a | Said in the talk, no study named | Talk only |

## [How Netflix Retrofitted Its SDLC for AI Coding Agents](talks/how-netflix-retrofitted-its-sdlc-for-ai-coding-agents.md)

| Claim | Figure | Source | Status |
|---|---|---|---|
| Netflix members | 300M+ | Slide 4. Netflix passed 300M paid memberships in Q4 2024 and reported [325M+ at the end of 2025](https://www.techloy.com/netflix-hits-325-million-subscribers-beats-earnings-as-ad-revenue-tops-1-5-billion/) | Checked |
| Countries | 190 | Slide 4 | Slide only |
| Revenue a year | \$45B+ | Slide 4. [FY2025 revenue \$45.2B](https://thedesk.net/2026/01/netflix-q4-2025-earnings-report/) | Checked |
| Context window when they started | 200K tokens | Recording, “pre Opus 4.5” | Talk only |
| Framework developer NPS, before | -3 | Slide 12 | Slide only |
| ADRs; docs | 45; 300+ | Slides 16, 17 (the recording says 345) | Slide only |
| Comments from the first review agent, one PR | 23 | Slide 24, an example | Slide only |
| Merged PRs that needed a docs update | ~9% | Slide 26 (the recording says changes to the API) | Slide only |
| Deploys a day | ~3 | Recording, “I think” | Talk only |
| Canary share of traffic | 10% | Slides 21, 27 | Slide only |
| Sev 1 incidents in 2026, one core service | 0 | Slide 28 | Caveat one service, not all of commerce |
| Pull requests, year over year | +32% | Slide 28 | Caveat no control for headcount or other changes given |
| Developer NPS, after | -3 → +25 | Slide 28, “three quarters apart” (the recording sounded like “about 3/4” of the work done) | Slide only |

## [Legacy as Leverage: How Brownfield Work Builds Technical Judgment](talks/legacy-as-leverage-how-brownfield-work-builds-technical-judgment.md)

| Claim | Figure | Source | Status |
|---|---|---|---|
| Messages per day on the SNS + SQS platform | 740M+ | Slide 15; repeated in the [session abstract](https://qconsf.com/presentation/nov2026/legacy-leverage-how-brownfield-work-builds-technical-judgment) | Caveat; Self-reported; employer not named |
| Engineers relying on the platform | 400+ | Slide 15; [speaker bio](https://qconsf.com/speakers/shinegarg) | Caveat; Self-reported |
| Time from platform launch to that state | 3.5 years | Slide 15 | Slide only |
| Schemas within two years | 2,000+ | Slide 16 | Slide only |
| Domains covered by schemas | 100+ | Transcript | Transcript only |
| Deployment automation scope | 150+ servers, 5 envs | Slide 6 | Slide only |
| Magic phone in production | 3+ years | Transcript; "over three years" in the session interview | Caveat; Speaker's own account in both |
| Partner's quoted cost to add a timestamp | \$1M+ | Transcript | Transcript only |
| Email service growth | 2M → 65M members | Transcript | Transcript only |
| Email daily run time | ~2h → ~24h | Transcript | Transcript only |
| Years on legacy systems | ~5 | Slide 2; abstract says "about five years" | Checked |
| Patents from the platform work | 3 | [Speaker bio](https://qconsf.com/speakers/shinegarg); she said in the talk she was lead inventor | Bio only; Patent numbers not given; not verified |
| SNS fanout to SQS is a supported AWS pattern | n/a | [AWS SNS docs](https://docs.aws.amazon.com/sns/latest/dg/sns-sqs-as-subscriber.html) | Checked |

## [Observability: The Missing Control Plane for Agentic Engineering](talks/observability-the-missing-control-plane-for-agentic-engineering.md)

| Claim | Figure | Source | Status |
|---|---|---|---|
| OpenTelemetry running in production | 49% | CNCF Annual Cloud Native Survey (Jan 2026), as reported by [o11y.news](https://buttondown.com/o11y.news/archive/2026-01-26/) and [Dash0](https://www.dash0.com/blog/moving-beyond-supports-opentelemetry-why-there-s-a-need-for-a-shared-maturity-model); another 26% evaluating | Checked |
| Self-describe as mature or expert | 60% | [Dimensional Research for Elastic](https://www.elastic.co/pdf/dimensional-research-2026-landscape-observability-white-paper.pdf): 49% mature + 11% expert, up from 41% in 2025; 500+ IT decision makers | Caveat vendor-sponsored, self-rated |
| Mature by outcomes | 15% | [ManageEngine State of Observability 2025](https://download.manageengine.com/it-operations-management/pdf/State-of-observability-2025-report.pdf): 15.8% mature, maturity set by benefits and outcomes | Caveat vendor survey; MTTR is one of several outcomes, not the sole test |
| Still in early stages | 51% | Same report: 50.2% early stage | Checked |
| Survey size | 1,240 | Same report: 1,240 IT professionals surveyed. She said "organizations" aloud; the slide and source say professionals. | Checked corrected |
| Chaos engineering / immutable infrastructure | 6% / 7% | [CNCF State of Cloud Native Development, Q3 2025](https://www.cncf.io/wp-content/uploads/2025/11/cncf_report_stateofcloud_111025a.pdf), share of backend developers | Checked |
| Use microservices | 30% | Slide 13 cites the CNCF report pp. 6, 23. The Q3 2025 report says 46% of backend developers operate microservices; [coverage of Q1 2026](https://cloudnativenow.com/features/cncf-report-global-cloud-native-developer-community-nears-20-million/) says 39%. I couldn't find 30%. | Slide only |
| Observability defined in control theory | 1960 | Rudolf Kálmán; see [Observability (Wikipedia)](https://en.wikipedia.org/wiki/Observability) | Checked |
| Shapiro five levels / Eledath eight levels | Jan / Mar 2026 | [Shapiro via Simon Willison](https://simonwillison.net/2026/Jan/28/the-five-levels/) (published Jan 23); [Eledath](https://www.bassimeledath.com/blog/levels-of-agentic-engineering) | Checked |
| Scenario metrics list | 8 metrics | [PlatformEngineering.org, Agent-first IDP](https://platformengineering.org/blog/agent-first-idp-how-big-tech-and-the-clouds-are-preparing-platforms-for-agents), Eugene Sergueev, Oct 16 2026, practice 9. Slide shows 7; she added approval cycle time aloud, which is in the source. | Checked |
| OTel GenAI conventions cover agents | Development | [OTel semantic conventions](https://opentelemetry.io/docs/specs/semconv/gen-ai/): `invoke_agent`, `execute_tool`, `plan` spans exist; all `gen_ai.*` items still Development status | Checked |
| Nomura and Equifax engineers code less than a quarter of the time | \<25% | Slides 28–29 not captured. I found no public source for either case study; the closest is an [Equifax job posting](https://careers.equifax.com/en/jobs/j00175843/principal-engineer-agentic-engineering/) describing an MCP toolset to ServiceNow, Atlassian, Datadog and GCP. | Transcript only |

## [You Can't Read the Code Anymore - Verifying Software in the Age of AI](talks/you-cant-read-the-code-anymore.md)

| Claim | Figure | Source | Status |
|---|---|---|---|
| Gate suite size and run time | 24,740 in 58.4 s | Slide 31 terminal output, one laptop. The [blog](https://blog.forter.dev/telem-teaching-systems-to-keep-promises/) says 24,000+ scenarios in under a minute on a personal MacBook; the [session page](https://qconsf.com/presentation/nov2026/you-cant-read-code-anymore-verifying-software-age-ai) says about 25K. | Checked |
| Gate business flows backfilled | ≈8,000 (Σ \> 24,000) | Slide 27. Does not reconcile with “1 to 2 hours in Claude Code per flow” (slide 39): 8,000 flows would be 8,000+ agent hours. “Business flow” on slide 27 probably means a distinct behavior, not the backfill unit. To ask. | Caveat |
| Behaviors not broken, past 60 days | 10,000+ | Slide 30; the dashboard on slide 40 shows 10,776. Omer said some might have been caught later by manual testing, so this counts regressions the suite flagged, not incidents prevented. | Caveat |
| Agent-guarded use cases, all services | 29,179 | Slide 40 dashboard tile | On slide |
| Token cost of a backfill | \$100s–\$1,000s per system | Slide 39. The blog and session page say “a few hundred dollars” for the gateway. The talk widened the range; complexity drives it. | Caveat |
| Agent time per flow | 1–2 h | Slide 39, in Claude Code | On slide |
| Human review, billing case study | ≈4 net eng. months | Slide 39, parallelized across the team | On slide |
| Billing repo fully covered | One quarter | Slide 29 quote from a billing senior engineer, after three senior engineers had failed | On slide |
| Flag combinations avoided | ≈2^40 | Blog: Telem permutes only the flags each test reads | Checked |
| Telem in development | 7 months | Transcript | Talk only |
| Cucumber’s age | ≈20 years | Slide 11. The blog dates Cucumber to 2008, which makes it about 18. | Caveat |
| telem-seed history | 53 commits, 9–12 Nov 2026 | Our clone at `4995a9d` | Checked |
| Sample app: test code to production code | 8,265 : 686 lines | Our count of `sample/test/telem` and `sample/src` | Checked |

## [How To Kill the Code Review](talks/how-to-kill-the-code-review.md)

| Claim | Figure | Source | Status |
|---|---|---|---|
| Developers ranking finding defects as the top reason for review | 44% | [Bacchelli and Bird 2013](https://doi.org/10.1109/ICSE.2013.6606617): 383 of 873 programmers | Checked |
| Classified review comments about defects | 14% | Same paper: 78 of 570 comments | Checked |
| Reviewed changes in Google’s study | 9 million | [Sadowski et al. 2018](https://research.google/pubs/modern-code-review-a-case-study-at-google/) | Checked |
| “We made writing cheap, and understanding stayed exactly as expensive…” | Quote | [Addy Osmani, Agentic Code Review](https://addyosmani.com/blog/agentic-code-review/), Jun 15, 2026 | Checked |
| PRs merged with no review | +76% | [Faros, The Speed Trap](https://www.faros.ai/blog/ai-speed-trap-takeaways): 76.3%, up from a 31.3% rise six months earlier. Vendor telemetry; a relative increase, not a share of PRs, though Ankit said “over 75% of PRs” on stage | Caveat |
| Average PR size | +72% | Faros: 71.8% | Checked |
| Work restarts | +67% | Faros: 66.7% | Checked |
| Incidents per month | +125% | Faros: 125.4%; incidents per PR rose 14.5% in the same report | Checked |
| AI raises throughput and instability | Finding | [DORA 2025](https://dora.dev/insights/balancing-ai-tensions/); survey of nearly 5,000 professionals | Checked |
| Devs “overloaded by AI slop PRs” | Quote | [The Pragmatic Engineer, The Pulse](https://blog.pragmaticengineer.com/the-pulse-new-trend-concern-about-massive-increase-in-code-review-load/); wording matches, Jul 23 date from the slide | Checked |
| r/ExperiencedDevs “won’t be reviewing AI generated PRs” post | 1.9K upvotes, 442 comments | Slide screenshot; post not found | Slide only |
| Defect detection limits | 400 lines, 60 min | [SmartBear / Cisco, 2006](https://smartbear.com/learn/code-review/best-practices-for-peer-code-review/), 2,500 reviews. SmartBear’s guidance is 200 to 400 lines and 60 to 90 minutes | Caveat |
| Aviator’s median AI-generated PR | 640 lines | Aviator’s own data | Slide only |
| AI review noise | 15 findings, 12 noise | Illustrative, no source given | Slide only |
| Wealthfront has no interest in removing review as a bottleneck | Quote | [Wealthfront, Experiments with AI Code Review](https://eng.wealthfront.com/2026/08/03/experiments-with-ai-code-review/), Aug 3, 2026; post confirmed, exact wording not found in my read | Caveat |
| Aviator team, a year apart | 4x PRs/week, 9 engineers | Aviator’s own data | Slide only |
| PR \#11318 threads | 14: 8 bot (1 real bug), 3 rules, 1 nit, 2 decisions | Aviator’s own PR. Our count of slide 51 rows: 8 bot plus 6 by Ankit = 14 | Slide only |
| Comment mining | 11,400 → 212 → 64 | Aviator’s own data; the recording said “over 11,000” and “200 plus” | Slide only |
| Incident timeline | 18 minutes | Slide citing status.aviator.co, Oct 26, 2026. Our arithmetic: 6:27 to 6:45 rollback complete is 18 minutes; resolved at 7:02, 35 minutes after impact | Caveat |
| Median time to merge | 3.4 h, was 2.1 days | Aviator’s own data. 2.1 days is 50.4 hours, so about 15x faster | Slide only |
| Human threads per PR | 1.3, was 6.2 | Aviator’s own data; a 79% drop | Slide only |
| Reverts | −40% (10 → 6 a quarter) | Arithmetic holds, but the slide footer reads “placeholder numbers: replace before the talk”. The recording also said 10 down to 6 | Caveat |
| Naur: “The death of a program happens when…” | Quote | Programming as Theory Building, 1985; matches the published text | Checked |
| “You can outsource your thinking, but you can’t outsource your understanding” | Quote | [Karpathy, Apr 30, 2026](https://x.com/karpathy/status/2049907410303865030), quoting an earlier post by @yacineMTB; Karpathy cites it, he did not coin it | Caveat |
| PR-Agent is MIT and free | License | GitHub showed MIT on Nov 18; Qodo’s April 2026 post said Apache 2.0 | Caveat |

## [Game Time: How to (Unsuccessfully) 10x in a Week & (Successfully) 10x in a Year](talks/game-time-10x-in-a-week-and-in-a-year.md)

| Claim | Figure | Source | Status |
|---|---|---|---|
| Super Bowls among the 20 most-watched US telecasts | 19 of 20 | [Wikipedia’s Nielsen list](https://en.wikipedia.org/wiki/List_of_most-watched_television_broadcasts_in_the_United_States): the M\*A\*S\*H finale is the only non-Super Bowl in the top 20 (11th) | Checked |
| Super Bowl audience | Over 100 million | [Fox](https://www.foxcorporation.com/?p=6207): Super Bowl LIX averaged 127.7 million viewers | Checked |
| Last-minute streaming ad, late January 2025 | About a week’s notice | [Tubefilter](https://www.tubefilter.com/2025/02/07/tubi-free-ad-supported-tv-fast-super-bowl-ads/): Fox sold Super Bowl LIX spots on its free Tubi stream, some offered as late as Jan 31. The talk didn’t name the platform | Caveat |
| Load-testing estimate vs build time | 6 weeks → 1.5 days | Slides 12-13 | Slide only |
| k6 browser tests “still in beta” in January 2025 | Stable in k6 1.0 | [k6 1.0 release notes](https://grafana.com/docs/k6/latest/release-notes/v1.0.0/) (May 2025) list k6/browser among modules now production-ready | Checked |
| Member UUID logic | 7+ years of rules | Recording | Slide only |
| Load times at the choke point, 2025 | 15-22 seconds | Recording only | Slide only |
| Monthly D&D sessions | 3 (March, April, May 2025) | Slide 38 | Slide only |
| D&D first published | 1974 | [Wikipedia](https://en.wikipedia.org/wiki/Dungeons_%26_Dragons) | Checked |
| ARPANET’s “first outage” in 1980, with a misconfigured monitor | Oct 27, 1980 | [RFC 789](https://www.rfc-editor.org/info/rfc789) (Eric Rosen, BBN) documents a network-wide outage of several hours that day. It says no such disturbance had happened “in several years”, so it was not the first. I did not check the monitor detail | Caveat |
| Preparation time for 2026 | Just over 5 months | Recording | Slide only |
| Pathological load held for | 5 minutes | Slides 39-40 and recording | Slide only |
| API calls the intake needs | 2 of about 60 | “2 \< 60” on slide 64 and the recording | Slide only |
| Worker steps after cleanup | About 25 | Recording | Slide only |
| Final D&D session size | About 18 people | Recording | Slide only |
| Cost of the 2026 ad | About \$7 million | [Ro co-founder Saman Rahmanian](https://ro.co/perspectives/making-of-super-bowl-ad/): at least \$233,000 per second; [Campaign](https://campaignlive.com/article/ro-makes-super-bowl-debut-serena-williams-shift-glp-1-narrative-vanity-vitals/1946604): a 30-second spot. 30 × \$233,000 = \$6.99 million | Checked |
| The 2026 ad | Ro’s first Super Bowl ad, Feb 8, 2026 | [Ro press release](https://ro.co/press/super-bowl-2026/), Jan 28, 2026: Serena Williams, “Healthier on Ro”, Super Bowl LX on NBC | Checked |
| Ro’s history | Seven years | [Front Office Sports](https://frontofficesports.com/?p=238525): Ro was founded in 2017 | Checked |
| Record minute of traffic and record hour of onboarding | No figures given | Recording; slide 63 shows business up, system flat | Slide only |
| Lady Gaga as a surprise halftime guest | Super Bowl LX | [Billboard](https://ca.billboard.com/music/pop/lady-gaga-bad-bunny-super-bowl): she joined Bad Bunny’s halftime show unannounced | Checked |

## [AI-Assisted Coding Master Class: Build Your Mission Control](talks/ai-assisted-coding-master-class-build-your-mission-control.md)

| Claim | Figure | Source | Status |
|---|---|---|---|
| Last year's QCon SF poll: share of daily coding assisted by AI | 45% at 0–25%; 14% at 75–100% | Sepehr's own poll, slide 2 | Slide only |
| Last year's poll: advanced or expert | 24% (12% + 12%) | Slide 3; 59% intermediate | Slide only |
| This year's room at the top of the range | About 70% at 100% | Show of hands, from my notes in the room; the audio transcript is garbled here | Caveat |
| Copilot the top tool in last year's poll | \#1 | Spoken only, no slide; the recording is unclear at that point | Caveat |
| Tokens a \$500,000 engineer should use | \$250,000 | [Jensen Huang on the All-In podcast at GTC 2026](https://www.tomshardware.com/tech-industry/artificial-intelligence/jensen-huang-says-nvidia-engineers-should-use-ai-tokens-worth-half-their-annual-salary-every-year-to-be-fully-productive-compares-not-using-ai-to-using-paper-and-pencil-for-designing-chips) | Checked |
| Claude Code system prompt cut for Claude 5 models | Over 80% | [Anthropic, the new rules of context engineering](https://claude.com/blog/the-new-rules-of-context-engineering-for-claude-5-generation-models): “no measurable loss on our coding evaluations”. Anthropic's own evals, not published | Caveat |
| Claude Code adopts AGENTS.md | Sept 2026 | Claude Code 2.1.277, Sep 18, 2026, reads AGENTS.md when no CLAUDE.md exists ([Thariq Shihipar, quoted](https://simonwillison.net/2026/Sep/18/thariq-shihipar/)) | Checked |
| Token cost: MCP schema vs CLI vs skill | 32k–82k vs ~200 vs ~30 idle | Slide 11; no source given | Slide only |
| Sepehr's last month | 2,396 PRs, 120B tokens | Slide 5, his own figures | Slide only |
| Room poll: tools used | AI review 45%, E2E 25%, contracts 10%, mutation 8%, formal 5%, PBT, fuzzing and symbolic 3% each, concolic 0% | Slide 18. The poll hit its response cap, and shares sum to about 100%, so they are shares of answers, not of people | Caveat |
| Ordinary code review catching a seeded security flaw | 3% and 21% | [Semgrep, Oct 9, 2026](https://semgrep.dev/blog/2026/end-is-nigh-for-code-review), citing [Braz et al., ICSE 2022](https://arxiv.org/abs/2202.04586); two seeded flaws, at best 61% with a tailored checklist | Checked |
| Commits that add mocks, agents vs others | 36% vs 26% | [Hora and Robbes, MSR 2026](https://arxiv.org/abs/2602.00409); 1.2M commits in 2,168 TypeScript, JavaScript and Python repos | Checked |
| Bug-catching tests that added no line coverage | 277 of 571 | [Meta ACH, FSE 2025](https://arxiv.org/abs/2501.12862): 49% of tests that killed a mutant added no line coverage. Kotlin Android classes, privacy hardening | Caveat |
| Tokens for TDD inside the agent loop | 3–8.5x | [Böckeler, martinfowler.com, Aug 2026](https://martinfowler.com/articles/exploring-gen-ai/tdd-in-the-agent-loop.html). An exploratory, small study; cache reads overstate the cost | Caveat |
| AI agents' use of `any` vs humans | 9x | [Lee, Hassan and Hindle, MSR 2026](https://arxiv.org/abs/2602.17955), TypeScript projects | Checked |
| LLM-written fuzz harnesses that work within three tries | 87% C, 81% C++; 15 new vulnerabilities in 11 projects | [Yang et al., HarnessAgent, arXiv 2512.03420](https://arxiv.org/abs/2512.03420); 243 OSS-Fuzz projects. The authors' own evaluation | Caveat |
| Paths vs tests in the boundaries example | 625 vs 20 | Slide 29; 5⁴ = 625 and 4 × 5 = 20, rerun | Checked |
| AI will make formal verification mainstream | Dec 2025 | [Kleppmann, Dec 8, 2025](https://martin.kleppmann.com/2025/12/08/ai-formal-verification.html) | Checked |
| Opus 5.5 verifying the Claude Agent SDK in Lean | 16 PRs | Boris Cherny's post of Sep 22, 2026, as shown on slide 36 and [reported](https://explainx.ai/blog/boris-cherny-opus-5-5-lean-tla-formal-verification-sdk-2026). A social post, not a write-up | Caveat |
