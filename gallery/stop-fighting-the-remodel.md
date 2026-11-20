---
title: "Slides: Stop Fighting the Remodel: API Design for Models That Outgrew Their Boundaries"
---

# Slides: Stop Fighting the Remodel: API Design for Models That Outgrew Their Boundaries

[Back to the notes](../talks/stop-fighting-the-remodel.md)

[![Slide 1: Title card: A software engineer's accidental education in roofing. Roofing Science 101. Track: Modern API Design for Humans and Agents.](../slides/stop-fighting-the-remodel/deep/p01.webp)](../slides/stop-fighting-the-remodel/deep/p01.webp)

*Slide 1: Title card*

[![Slide 2: Episode 1, The Roof. Hi, I'm Aarti Gupta: roofing expert by necessity, software engineer by trade. Staff Engineer at Netflix, team CBP Foundations (Content and Business Products), based in the Bay Area.](../slides/stop-fighting-the-remodel/deep/p02.webp)](../slides/stop-fighting-the-remodel/deep/p02.webp)

*Slide 2: Introduction*

[![Slide 3: October 2024. I was forced to become a roofing expert. 7+ places where the roof was leaking, with photos of the shakes, a ceiling crack and the floor.](../slides/stop-fighting-the-remodel/deep/p03.webp)](../slides/stop-fighting-the-remodel/deep/p03.webp)

*Slide 3: October 2024: 7+ leaks*

[![Slide 4: We learn the science under the hood. Cemwood, installed on her roof in 1998: 2 to 1 cement to wood, pressed to look like cedar shake, fire-safe, 50-year warranty.](../slides/stop-fighting-the-remodel/deep/p04.webp)](../slides/stop-fighting-the-remodel/deep/p04.webp)

*Slide 4: Cemwood*

[![Slide 5: Roof can last another 25 years. The 2020 disclosure said the roof may last another 25 years with proper care; four years later, in 2024, 7+ leaks were found.](../slides/stop-fighting-the-remodel/deep/p05.webp)](../slides/stop-fighting-the-remodel/deep/p05.webp)

*Slide 5: The disclosure vs four years later*

[![Slide 6: Outsource the problem. The roofer took one step onto the roof and it cracked.](../slides/stop-fighting-the-remodel/deep/p06.webp)](../slides/stop-fighting-the-remodel/deep/p06.webp)

*Slide 6: Outsource the problem*

[![Slide 7: Spec vs reality: 50 years warranted at installation, 25 years left according to the disclosure, 1 step to set off a ripple of cracks. Stay off the roof.](../slides/stop-fighting-the-remodel/deep/p07.webp)](../slides/stop-fighting-the-remodel/deep/p07.webp)

*Slide 7: Spec vs reality*

[![Slide 8: So the only way forward: a complete replacement, since patching was ruled out. A lift and shift is how her kid imagined it.](../slides/stop-fighting-the-remodel/deep/p08.webp)](../slides/stop-fighting-the-remodel/deep/p08.webp)

*Slide 8: The only way forward*

[![Slide 9: Why talk about roofs at a software conference? 01 composite failures: small cracks compound. 02 turning a blind eye: someone always saw it coming. 03 remodels are costly: migrations are elaborate and time-intensive.](../slides/stop-fighting-the-remodel/deep/p09.webp)](../slides/stop-fighting-the-remodel/deep/p09.webp)

*Slide 9: Why roofs at a software conference*

[![Slide 10: The roof carries the same load year after year; software faces changing models, ownership moves, workflows that cross, splits, merges and moving boundaries. AI accelerates the change.](../slides/stop-fighting-the-remodel/deep/p10.webp)](../slides/stop-fighting-the-remodel/deep/p10.webp)

*Slide 10: Roofs stay put, software doesn't*

[![Slide 11: Today, three questions. How do you know your roof is leaking (five diagnostic signs). Patch it or replace it, and how to redraw the boundaries. How do you re-roof without moving out: migrating 100+ consumers with zero downtime.](../slides/stop-fighting-the-remodel/deep/p11.webp)](../slides/stop-fighting-the-remodel/deep/p11.webp)

*Slide 11: Three questions*

[![Slide 12: Episode 2, At Netflix. Content and Business Products Foundations. Who are our consumers? 100+ apps consume our data, under Content, Ads, Studio and more, all built on CBP Foundations.](../slides/stop-fighting-the-remodel/deep/p12.webp)](../slides/stop-fighting-the-remodel/deep/p12.webp)

*Slide 12: 100+ consuming apps*

[![Slide 13: Entity Services, the team she works on: foundational entities in a connected knowledge graph. 1.7M person records and 225K vendor records; a users figure is cut off in the photo.](../slides/stop-fighting-the-remodel/deep/p13.webp)](../slides/stop-fighting-the-remodel/deep/p13.webp)

*Slide 13: Entity Services*

[![Slide 14: Chart of requests per second over Sep 25 to 30. Axis values are not readable in the photo.](../slides/stop-fighting-the-remodel/deep/p14.webp)](../slides/stop-fighting-the-remodel/deep/p14.webp)

*Slide 14: Requests per second*

[![Slide 15: Chart of p99 latency over the same week. Axis values are not readable in the photo.](../slides/stop-fighting-the-remodel/deep/p15.webp)](../slides/stop-fighting-the-remodel/deep/p15.webp)

*Slide 15: Latency p99*

[![Slide 16: The API powers the business. APIs are projections, one per use case: GraphQL schema, gRPC service and an internal IPC. A mapping layer sits between them and the domain model, which sits on the data model: vendor tables and RAW Hollow objects.](../slides/stop-fighting-the-remodel/deep/p16.webp)](../slides/stop-fighting-the-remodel/deep/p16.webp)

*Slide 16: The API powers the business*

[![Slide 17: Where the leak actually was: in the domain model layer, one Vendor with five meanings, between the API projections above and the invariants and data model below.](../slides/stop-fighting-the-remodel/deep/p17.webp)](../slides/stop-fighting-the-remodel/deep/p17.webp)

*Slide 17: Where the leak was*

[![Slide 18: The supply chain was drawn as one line with two ends: a content partner makes an asset and a fulfillment partner delivers it. Then Spotify (The Rewatchables, live on Netflix) both produces and delivers: one partner, two roles.](../slides/stop-fighting-the-remodel/deep/p18.webp)](../slides/stop-fighting-the-remodel/deep/p18.webp)

*Slide 18: One line, two ends*

[![Slide 19: Episode 3, The leak at Netflix. Amber Studio is one business with one tax ID, but World of Peppa Pig and Play With Fire each got their own partner key, so the same vendor was copied per title.](../slides/stop-fighting-the-remodel/deep/p19.webp)](../slides/stop-fighting-the-remodel/deep/p19.webp)

*Slide 19: Amber Studio: one business, many keys*

[![Slide 20: Inversions of money and time. Every other vendor is paid by Netflix, but advertisers pay Netflix. For live and sports, the rights window comes before the asset exists.](../slides/stop-fighting-the-remodel/deep/p20.webp)](../slides/stop-fighting-the-remodel/deep/p20.webp)

*Slide 20: Inversions of money and time*

[![Slide 21: Signs your roof is leaking. 01 A polyseme: one word, vendor, means a content or fulfillment partner in Content, a studio with many titles in Games, an advertiser who pays us in Ads and a payee with one tax ID in Finance. Force one model to hold them all and you get the tangle.](../slides/stop-fighting-the-remodel/deep/p21.webp)](../slides/stop-fighting-the-remodel/deep/p21.webp)

*Slide 21: Sign 1: a polyseme*

[![Slide 22: 02 Incorrect data invariants: the business broke core invariants such as a partner has exactly one legal identity and a partner's tax ID is unique. Invariants aren't fields; you can't split them by moving a column.](../slides/stop-fighting-the-remodel/deep/p22.webp)](../slides/stop-fighting-the-remodel/deep/p22.webp)

*Slide 22: Sign 2: broken invariants*

[![Slide 23: 03 Blast radius: how far a single change travels. Internal domain structures leak to every consumer, and one schema change becomes a 100-team refactor.](../slides/stop-fighting-the-remodel/deep/p23.webp)](../slides/stop-fighting-the-remodel/deep/p23.webp)

*Slide 23: Sign 3: blast radius*

[![Slide 24: 04 Stamp coupling: passing a whole composite structure to a module that needs one piece. A vendor object with legal metadata, global licensing rights, tax identity and hierarchy was handed to a module that only mints an API key.](../slides/stop-fighting-the-remodel/deep/p24.webp)](../slides/stop-fighting-the-remodel/deep/p24.webp)

*Slide 24: Sign 4: stamp coupling*

[![Slide 25: 05 Connascence: a change in one module requires a change in another to stay correct. Overloading a string field to say this vendor is really a game title means every downstream service must share the convention or break at runtime.](../slides/stop-fighting-the-remodel/deep/p25.webp)](../slides/stop-fighting-the-remodel/deep/p25.webp)

*Slide 25: Sign 5: connascence*

[![Slide 26: Episode 5, The search for a fix. If you find yourself in a hole, stop digging. Quote from Chris Richardson, Microservices Patterns (2018): don't add new features to the monolith, implement them as services. Steps: stop digging, new features as services, strangle the monolith.](../slides/stop-fighting-the-remodel/deep/p26.webp)](../slides/stop-fighting-the-remodel/deep/p26.webp)

*Slide 26: Stop digging*

[![Slide 27: Different boundaries, same pressures: SOA in the 2000s, DDD from Evans in 2003, microservices around 2014, and now, in the AI era, a modular approach. Each pattern is another move to recognize and reuse.](../slides/stop-fighting-the-remodel/deep/p27.webp)](../slides/stop-fighting-the-remodel/deep/p27.webp)

*Slide 27: Different boundaries, same pressures*

[![Slide 28: SOA, 1996 to 2004: boundaries are explicit. Capabilities sit behind explicit contracts and are crossed only by message. Kept: ask the service, don't read its data. The contract is the wall.](../slides/stop-fighting-the-remodel/deep/p28.webp)](../slides/stop-fighting-the-remodel/deep/p28.webp)

*Slide 28: SOA*

[![Slide 29: Bounded contexts, Domain-Driven Design, 2003: an anti-corruption layer translates between contexts. Split the model: in Ads, vendor means an advertiser; in Finance, a payee we pay; in Games, a studio with many titles.](../slides/stop-fighting-the-remodel/deep/p29.webp)](../slides/stop-fighting-the-remodel/deep/p29.webp)

*Slide 29: Bounded contexts*

[![Slide 30: Microservices, around 2014: own it, ship it alone. One team, one service, one database. Pros: teams ship without waiting, one bug stays in one service. Cons: every call crosses the network; cut too small, one change needs many deploys. Self deployment equals self governance.](../slides/stop-fighting-the-remodel/deep/p30.webp)](../slides/stop-fighting-the-remodel/deep/p30.webp)

*Slide 30: Microservices*

[![Slide 31: Episode 6, Re-roofing at Netflix. Five houses, one roof: one codebase, one build, one deploy, with Content, Games, Ads, Financial and Artwork business entities behind CI-enforced boundaries over a shared Legal Entity core: exactly one legal identity, and a tax ID is unique.](../slides/stop-fighting-the-remodel/deep/p31.webp)](../slides/stop-fighting-the-remodel/deep/p31.webp)

*Slide 31: Five houses, one roof*

[![Slide 32: Quiz: how many cables does this take? 100 apps wired to five houses (Content, Games, Ads, Finance, Access). Options 5, 100, 105, 500; the answer is 500, apps times houses.](../slides/stop-fighting-the-remodel/deep/p32.webp)](../slides/stop-fighting-the-remodel/deep/p32.webp)

*Slide 32: Quiz: how many cables?*

[![Slide 33: Quiz: name the problem we just described. A single point of failure, the N+1 problem, N times M fan-out, or none of the above. The answer is N times M fan-out.](../slides/stop-fighting-the-remodel/deep/p33.webp)](../slides/stop-fighting-the-remodel/deep/p33.webp)

*Slide 33: Quiz: name the problem*

[![Slide 34: Episode 7, The search ends. Unprecedented scale with GraphQL Federation, with a large 4,000 and a link to Netflix's blog post on scaling its API with GraphQL Federation. Callers such as vendor HQ, the ads service and UI clients hit one graph: one query in, batched, no N+1, no fan-out. DGS stitches it all together.](../slides/stop-fighting-the-remodel/deep/p34.webp)](../slides/stop-fighting-the-remodel/deep/p34.webp)

*Slide 34: GraphQL Federation*

[![Slide 35: Federated GraphQL: every team owns its subgraph. Accounts, Catalog and Interactions subgraphs compose through a router to TV, mobile and web. One subgraph per domain; one change, one team; the router composes and clients see one graph.](../slides/stop-fighting-the-remodel/deep/p35.webp)](../slides/stop-fighting-the-remodel/deep/p35.webp)

*Slide 35: Every team owns its subgraph*

[![Slide 36: Ask for exactly what you need: a GraphQL query for ads entities by ID that pulls the entity, its core vendor and its ads organization from three subgraphs plus gateway request details, and nothing more.](../slides/stop-fighting-the-remodel/deep/p36.webp)](../slides/stop-fighting-the-remodel/deep/p36.webp)

*Slide 36: Ask for exactly what you need*

[![Slide 37: One query, then N: the N+1 problem. One query for the list of shows, N queries to an external artwork service, and N database queries behind an inefficient fetcher.](../slides/stop-fighting-the-remodel/deep/p37.webp)](../slides/stop-fighting-the-remodel/deep/p37.webp)

*Slide 37: The N+1 problem*

[![Slide 38: N+1, the restaurant edition: 10 orders, 10 trips. One query for a list, then N sequential queries, one per item, like a waiter who walks to the kitchen ten times instead of writing one ticket.](../slides/stop-fighting-the-remodel/deep/p38.webp)](../slides/stop-fighting-the-remodel/deep/p38.webp)

*Slide 38: N+1, restaurant edition*

[![Slide 39: Batch loading: one ticket to the kitchen. Collect every key, run the loader once, send one request.](../slides/stop-fighting-the-remodel/deep/p39.webp)](../slides/stop-fighting-the-remodel/deep/p39.webp)

*Slide 39: Batch loading*

[![Slide 40: N+1, fixed in prod. Slowest requests: up to about 7 seconds before (p99 peak 7.2s), under 1.4 seconds after. Typical requests at about 0.4 seconds did not change; what disappeared was the multi-second slow tail.](../slides/stop-fighting-the-remodel/deep/p40.webp)](../slides/stop-fighting-the-remodel/deep/p40.webp)

*Slide 40: N+1 fixed in prod*

[![Slide 41: Fewer calls, no slow tail. Before the fix: 396 calls, 66 over 2 seconds (17%), 51% under 0.5 seconds. After: 78 calls, none over 2 seconds, 83% under 0.5 seconds.](../slides/stop-fighting-the-remodel/deep/p41.webp)](../slides/stop-fighting-the-remodel/deep/p41.webp)

*Slide 41: Fewer calls, no slow tail*

[![Slide 42: Walls inside one house: a managed runtime where each domain service writes only its own RAW Hollow namespace (ads, legal, coreVendor), callers use DGS queries and writes, and a proxy forwards writes to the legacy Vendor Service.](../slides/stop-fighting-the-remodel/deep/p42.webp)](../slides/stop-fighting-the-remodel/deep/p42.webp)

*Slide 42: Walls inside one house*

[![Slide 43: Building an ontology: defining a domain class in seven steps. Define the trait, define the direct class, set the primary key, define an enumeration, establish relationships, implement the trait, fuse across domains. Each is defined in Upper.](../slides/stop-fighting-the-remodel/deep/p43.webp)](../slides/stop-fighting-the-remodel/deep/p43.webp)

*Slide 43: Building an ontology*

[![Slide 44: Trait, a shared contract (rdf.netflix.net/onto/v2b#Entity): anything that is an Entity has an id, one core vendor and one or more domains.](../slides/stop-fighting-the-remodel/deep/p44.webp)](../slides/stop-fighting-the-remodel/deep/p44.webp)

*Slide 44: Trait*

[![Slide 45: Direct class, a concept with its own records (v2b#CoreVendor): every Entity points to one CoreVendor; Ads and Games business entities implement the trait.](../slides/stop-fighting-the-remodel/deep/p45.webp)](../slides/stop-fighting-the-remodel/deep/p45.webp)

*Slide 45: Direct class*

[![Slide 46: Relationship, a link with a count: a games business entity has zero or more game production mappings, so a games partner can work on any number of productions.](../slides/stop-fighting-the-remodel/deep/p46.webp)](../slides/stop-fighting-the-remodel/deep/p46.webp)

*Slide 46: Relationship*

[![Slide 47: Fuse edges, another team's concept: links to ADS_Organization and NPP_Partner owned by other teams. One-to-one means the link is mandatory; point by key, never copy.](../slides/stop-fighting-the-remodel/deep/p47.webp)](../slides/stop-fighting-the-remodel/deep/p47.webp)

*Slide 47: Fuse edges*

[![Slide 48: Enumeration, a fixed list of values: BusinessDomain is ADS, GAMES, ARTWORK, PUBLISHING, PRODUCTION or LEGAL, and nothing else.](../slides/stop-fighting-the-remodel/deep/p48.webp)](../slides/stop-fighting-the-remodel/deep/p48.webp)

*Slide 48: Enumeration*

[![Slide 49: One Vendor, 6+ shapes, zero drift. UDA: model once, represent everywhere. A projection turns the domain model into a real container such as a GraphQL type.](../slides/stop-fighting-the-remodel/deep/p49.webp)](../slides/stop-fighting-the-remodel/deep/p49.webp)

*Slide 49: One vendor, 6+ shapes*

[![Slide 50: The same model projected into a GraphQL type, an Avro record for Data Mesh and an Iceberg table. Change the model once and every container follows.](../slides/stop-fighting-the-remodel/deep/p50.webp)](../slides/stop-fighting-the-remodel/deep/p50.webp)

*Slide 50: Every container follows*

[![Slide 51: Self-validation, checked by Upper: the core vendor (the legal entity) with Ads, Games and Artwork business entities. Upper, the model for all models, validates every model including its own: self-describing, self-referencing, self-validating.](../slides/stop-fighting-the-remodel/deep/p51.webp)](../slides/stop-fighting-the-remodel/deep/p51.webp)

*Slide 51: Self-validation by Upper*

[![Slide 52: ROI, context-aware search: the word partners alone matches five concepts (games, ads, artwork, publishing and production partner), all tied to the core vendor, the legal entity.](../slides/stop-fighting-the-remodel/deep/p52.webp)](../slides/stop-fighting-the-remodel/deep/p52.webp)

*Slide 52: Context-aware search*

[![Slide 53: Searching for game partners for Northwind Media resolves to the games partner concept and the core vendor, and finds it in the GraphQL subgraph, search index and Iceberg table. Credited to Sphere and Netflix's UDA post, 2025.](../slides/stop-fighting-the-remodel/deep/p53.webp)](../slides/stop-fighting-the-remodel/deep/p53.webp)

*Slide 53: Game partners for Northwind Media*

[![Slide 54: Weather alert, agentic weathering. Someone else is on the roof, and nobody told it to stay off. Three questions: who's up there and who sent them (identity); where may they step (policies); what did they touch (observability).](../slides/stop-fighting-the-remodel/deep/p54.webp)](../slides/stop-fighting-the-remodel/deep/p54.webp)

*Slide 54: Someone else is on the roof*

[![Slide 55: Agentic identity, know who's asking: the agent carries its own name and principal ID, and the person it acts for carries an end-to-end user token. On behalf of is not optional.](../slides/stop-fighting-the-remodel/deep/p55.webp)](../slides/stop-fighting-the-remodel/deep/p55.webp)

*Slide 55: Agentic identity*

[![Slide 56: Agentic access policies and governance. Before: a check copied into every backend that can't tell an agent from a person. After: can this person see it, and should an agent do it for them? Tag the data once; let the platform say no.](../slides/stop-fighting-the-remodel/deep/p56.webp)](../slides/stop-fighting-the-remodel/deep/p56.webp)

*Slide 56: Agent access policies*

[![Slide 57: Agentic observability from audit logs: 300K agent calls, all reads; 6,000 agent writes, synthetic data in test; and some agents that don't say so and look like a person or an app. Quiet doesn't mean safe; it may mean unlabelled.](../slides/stop-fighting-the-remodel/deep/p57.webp)](../slides/stop-fighting-the-remodel/deep/p57.webp)

*Slide 57: Agent audit logs*

[![Slide 58: Back to the three questions: patch it or replace it, and how do you re-roof without moving out.](../slides/stop-fighting-the-remodel/deep/p58.webp)](../slides/stop-fighting-the-remodel/deep/p58.webp)

*Slide 58: Back to the three questions*

[![Slide 59: Strangler fig, nobody moves out. Six stages: Scaffold, Stop digging, Facade, Lure, Flip the source, Tear off. 100+ consumers, zero downtime.](../slides/stop-fighting-the-remodel/deep/p59.webp)](../slides/stop-fighting-the-remodel/deep/p59.webp)

*Slide 59: Strangler fig: six stages*

[![Slide 60: Stage 4, Lure: the old model drains as consumers move through the API facade when ready. Every read and write on the new service is authorized before it runs.](../slides/stop-fighting-the-remodel/deep/p60.webp)](../slides/stop-fighting-the-remodel/deep/p60.webp)

*Slide 60: Stage 4: Lure*

[![Slide 61: Stage 5, Flip the source: writes stay on the original while a shadow copy is built via the facade; then reads move to the new system while writes go to the old; then the new system becomes the source of truth for legacy entities via the facade.](../slides/stop-fighting-the-remodel/deep/p61.webp)](../slides/stop-fighting-the-remodel/deep/p61.webp)

*Slide 61: Stage 5: Flip the source*

[![Slide 62: Stage 6, Tear off: with 100% of traffic routed, the old model retires and the new UDA model is the sole model, but only after the last consumer leaves.](../slides/stop-fighting-the-remodel/deep/p62.webp)](../slides/stop-fighting-the-remodel/deep/p62.webp)

*Slide 62: Stage 6: Tear off*

[![Slide 63: Takeaway 1, score the leak: count the five signs (polysemy, broken invariants, blast radius, stamp coupling, connascence), keep a scorecard rather than a hunch, and read the score.](../slides/stop-fighting-the-remodel/deep/p63.webp)](../slides/stop-fighting-the-remodel/deep/p63.webp)

*Slide 63: Takeaway 1: score the leak*

[![Slide 64: Takeaway 2, keep change local: split by reason to change (one context, one meaning, one owner), serve it as one graph with federated GraphQL, and write the meaning once in UDA and generate the schema from it.](../slides/stop-fighting-the-remodel/deep/p64.webp)](../slides/stop-fighting-the-remodel/deep/p64.webp)

*Slide 64: Takeaway 2: keep change local*

[![Slide 65: Takeaway 3, migrate without disruption: one facade, one stage at a time; the strangler fig pattern; deprecate, don't break.](../slides/stop-fighting-the-remodel/deep/p65.webp)](../slides/stop-fighting-the-remodel/deep/p65.webp)

*Slide 65: Takeaway 3: migrate without disruption*

[![Slide 66: Expect change. In an agentic world, change is frequent. Get past the mental block, right-size the first bite with a small greenfield use case, and build the muscle with small changes first.](../slides/stop-fighting-the-remodel/deep/p66.webp)](../slides/stop-fighting-the-remodel/deep/p66.webp)

*Slide 66: Expect change*

[![Slide 67: Thank you. Aarti Gupta, Staff Software Engineer, Netflix. Further reading: Patterns of Legacy Displacement; Parallel Change; Microservices Patterns, chapter 13; Principles of Web API Design; Model Once, Represent Everywhere (UDA).](../slides/stop-fighting-the-remodel/deep/p67.webp)](../slides/stop-fighting-the-remodel/deep/p67.webp)

*Slide 67: Thank you and further reading*
