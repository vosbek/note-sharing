---
title: "Stop Fighting the Remodel: API Design for Models That Outgrew Their Boundaries"
---

# Stop Fighting the Remodel: API Design for Models That Outgrew Their Boundaries

**Speaker:** Aarti Gupta (Staff Engineer, Netflix)  
QCon SF 2026 · Modern API Design for Humans and Agents · Mon Nov 16, 13:35 · Ballroom BC  
[Session page](https://qconsf.com/presentation/nov2026/stop-fighting-remodel-api-design-models-outgrew-their-boundaries)

> How Netflix's Entity Services team found its shared vendor model no longer fit the business, and is rebuilding it in stages while agents start calling its APIs.

## Key points

- More than 100 internal apps consume her team's data. Entity Services holds 1.7 million person records and 225,000 vendor records, so a small API decision can become a company-wide migration.
- The leak was not in the API or the data but in the domain model. Vendor came to mean a content or fulfillment partner, a game studio with many titles, an advertiser who pays Netflix, and a payee with one tax ID.
- Games forced a copy of one legal entity per title to keep partner keys working. Ads reversed which way money flows, and live events needed rights before the asset existed. Each was patched with special cases.
- She gave five signs a model is leaking: a polyseme, broken data invariants, blast radius, stamp coupling and connascence. She urged keeping a scorecard rather than a hunch.
- The fix reused older patterns. Stop adding to the old model and split it into bounded contexts with a translation layer. Five domain models now sit behind CI-enforced boundaries in one deployable, over a shared legal-entity core.
- With 100 apps and five domains, direct wiring needs 500 connections. GraphQL Federation on Netflix's open-source DGS framework gives consumers one graph. Each team owns its own subgraph.
- Batch loading fixed an N+1 problem in production. Calls in the sample fell from 396 to 78, calls over 2 seconds from 66 to none, and the p99 peak from 7.2 seconds to under 1.4. She said cost fell about 20%.
- Each domain is modelled once in Netflix's UDA, with a URI for every concept, and GraphQL, Avro and Iceberg schemas are generated from it so they do not drift. She argued people and agents both need that shared meaning.
- Audit logs showed 300,000 agent calls, all reads, and 6,000 agent writes of synthetic test data, plus agents that do not identify themselves. Calls now carry an agent identity and the user's token, and policy asks whether an agent may act for that user.
- The migration runs as a six-stage strangler fig (scaffold, stop digging, facade, lure, flip the source, tear off) with zero downtime. She said 62 consumers had moved and 38 had not.

From an audio recording and 67 slide photos. The deck shows no slide numbers, so slides are numbered here in photo order. Figures come from the slides first, then Netflix’s published posts, then the recording. The recording is badly garbled in places; where it disagrees with a slide, the slide wins.

## The talk in brief

Aarti’s team owns the vendor and entity data that more than 100 internal Netflix apps depend on. As Netflix moved into ads, games and live events, one shared word, *vendor*, came to mean four different things, and the team patched each new meaning into one model until it leaked. Her talk uses the 2024 failure of her own Cemwood roof as the frame: a spec that promised decades, small cracks that compounded, and a full replacement that nobody could do by stepping on the old roof.

She gave five measurable signs that a domain model is leaking (polysemy, broken invariants, blast radius, stamp coupling and connascence). The fix combined old patterns: bounded contexts as five domain “houses” under one deployable “roof”, GraphQL Federation on Netflix’s DGS framework, batch loading to remove N+1 calls, and UDA to define each concept once and generate every schema from it. Agents now call these APIs, so the team added agent identity, per-agent policy and audit logs. The migration runs as a six-stage strangler fig with zero downtime.

> “Tag the data once. Let the platform say no.” (Slide 56, on agent access policies)

## In depth

The talk ran as nine “episodes”; each part below follows that order. Slide numbers are photo order (1 to 67).

### Episode 1: the roof (slides 1–11)

In October 2024 Aarti found more than seven leaks in her house. The roof was Cemwood, installed in 1998: two parts Portland cement to one part wood fiber, pressed to look like cedar shake, fire-safe and sold with a 50-year warranty. Her 2020 disclosure said it could last another 25 years with proper care. When a roofer stepped onto it to quote a repair, it cracked under him. The guidance for inspecting Cemwood is to stay off the roof. No one would take the liability for a patch and no matching material was in stock, so the only option was full replacement.

She drew three lessons for software: small cracks compound, someone usually saw it coming, and remodels are costly. Unlike a roof, software doesn’t carry the same load every year. Models change, ownership moves, workflows cross, businesses split and merge, and AI speeds all of it up. That set up three questions: how do you know the roof is leaking, should you patch or replace it, and how do you re-roof without moving out.

![Slide 7: Spec vs reality. 50 years warranted at installation, 25 years left according to the disclosure, 1 step to set off a ripple of cracks. Stay off the roof.](../slides/stop-fighting-the-remodel/deep/p07.webp)

Slide 7. Spec vs reality: the warranty, the disclosure and one step.

![Slide 11: Three questions. How do you know your roof is leaking; patch it or replace it; how do you re-roof without moving out, migrating 100+ consumers with zero downtime.](../slides/stop-fighting-the-remodel/deep/p11.webp)

Slide 11. The three questions the talk answers.

### Episode 2: the house at Netflix (slides 12–17)

Aarti works in CBP Foundations, the load-bearing layer under Netflix’s internal studio, content and ads apps. More than 100 apps consume its data, so a small API decision can become a company-wide migration. Her team, Entity Services, connects foundational entities into a knowledge graph: 1.7 million person records and 225,000 vendor records, the legal companies Netflix does business with. In the room she said some services handle 10,000 to 20,000 requests per second with 99% of calls under a second; the charts on slides 14 and 15 aren’t readable enough to confirm the numbers.

Slide 16 lays out the stack. APIs are projections, one per use case (a GraphQL schema, a gRPC service, an internal IPC). They derive from the domain model through an explicit mapping layer, and the domain model sits on invariants and a data model. Slide 17 places the leak: not in the API, not in the data, but in the domain model, where one “Vendor” had five meanings.

![Slide 13: Entity Services, foundational entities in a connected knowledge graph. 1.7M person records and 225K vendor records.](../slides/stop-fighting-the-remodel/deep/p13.webp)

Slide 13. Entity Services: 1.7M persons, 225K vendors.

![Slide 17: Where the leak actually was. Layers: API projections, domain model (one Vendor, five meanings), invariants, data model. The leak is in the domain model.](../slides/stop-fighting-the-remodel/deep/p17.webp)

Slide 17. The leak was in the domain model.

### Episode 3: how the leak happened (slides 18–20)

For years the supply chain was one line with two ends: a content partner made an asset and a fulfillment partner delivered it. Then a partner like Spotify (The Rewatchables) both produced and delivered, and the model had no way to show one company doing two jobs. Games added another strain. Amber Studio is one business with one tax ID, but partner API keys were issued per title, so World of Peppa Pig and Play With Fire each needed their own copy of the same vendor. The rule that one legal entity has one record quietly broke.

Ads inverted money: every other vendor is paid by Netflix, but advertisers pay Netflix, and a surprising amount of code assumed money flows one way. Live and sports inverted time: the rights window arrives before the asset exists. Each case was handled with special exceptions.

![Slide 19: Amber Studio, one business with one tax ID, branches into separate partner keys for World of Peppa Pig and Play With Fire.](../slides/stop-fighting-the-remodel/deep/p19.webp)

Slide 19. One studio, one tax ID, a vendor copy per game.

![Slide 20: Inversions of money and time. Netflix pays every other vendor, but advertisers pay Netflix. For live and sports, the rights window comes before the asset exists.](../slides/stop-fighting-the-remodel/deep/p20.webp)

Slide 20. Ads reverse the money; live events reverse the timeline.

### Episode 4: five signs your roof is leaking (slides 21–25)

The core of the talk is a scorecard. Each sign is something you can find in a codebase or an API review, and later slides tick them off one by one as each fix lands.

| Sign                  | What it means                                                | Netflix’s example                                                                                                       |
|-----------------------|--------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|
| 1\. Polyseme          | One word, a different meaning in every domain                | Vendor as content partner, game studio, advertiser and payee                                                            |
| 2\. Broken invariants | The system’s promises are bent to keep up with the business  | “One legal identity per partner” and “unique tax ID” broken by per-game copies                                          |
| 3\. Blast radius      | How far one change travels                                   | Internal structures leak to consumers; one schema change becomes a 100-team refactor                                    |
| 4\. Stamp coupling    | A whole composite object passed to code that needs one piece | Vendor with legal metadata, licensing rights, tax identity and hierarchy, sent to a module that only mints an API key   |
| 5\. Connascence       | A change in one module forces a change in another            | A string field overloaded to mean “this vendor is really a game title”, failing at runtime when a consumer doesn’t know |

She owned the fifth one herself: she added the string convention, and every other system then had to learn it, with no compiler to catch the misses.

![Slide 21: Sign 01, a polyseme. Vendor means a content or fulfillment partner in Content, a studio with many titles in Games, an advertiser who pays us in Ads, and a payee with one tax ID in Finance.](../slides/stop-fighting-the-remodel/deep/p21.webp)

Slide 21. Sign 1: one word, four meanings.

![Slide 24: Sign 04, stamp coupling. A vendor object with vendorId, legal metadata, global licensing rights, tax identity and hierarchy is passed to a module that only mints an API key.](../slides/stop-fighting-the-remodel/deep/p24.webp)

Slide 24. Sign 4: the whole vendor, for one API key.

### Episode 5: the search for a fix (slides 26–30)

The first rule came from Chris Richardson’s *Microservices Patterns*: if you find yourself in a hole, stop digging. Don’t add new features to the old model; build them in the new one, then strangle the old. Netflix was already on microservices, but the principle applied to the model.

She then walked the eras as reusable moves rather than fashions. SOA gave explicit contracts: ask the service, don’t read its data. DDD gave bounded contexts, where each context keeps its own model and an anti-corruption layer translates between them, so “vendor” can mean an advertiser in Ads and a payee in Finance. Microservices gave ownership: one team, one service, one database, and the ability to ship alone, at the cost of network calls and, if cut too small, many deploys per change.

![Slide 27: Different boundaries, same pressures. SOA in the 2000s, DDD from Evans in 2003, microservices around 2014, and a modular approach now in the AI era.](../slides/stop-fighting-the-remodel/deep/p27.webp)

Slide 27. Each era is a move to reuse.

![Slide 29: Bounded contexts, DDD 2003. An anti-corruption layer translates between contexts; Vendor means an advertiser in Ads, a payee in Finance and a studio with many titles in Games.](../slides/stop-fighting-the-remodel/deep/p29.webp)

Slide 29. Split the model by context.

### Episode 6: five houses, one roof (slides 31–33)

The synthesis is a modular monolith. Five business entities (Content, Games, Ads, Financial and Artwork) each have their own domain model and rules, separated by CI-enforced boundaries, but ship as one codebase, one build and one deploy because one team owns them. Underneath is a shared legal-entity core that keeps the two invariants the business must never break: exactly one legal identity per partner, and a unique tax ID.

Then a quiz. With 100 apps and five houses, how many connections? The room answered 500, which is right: 100 × 5. That is the N×M fan-out problem, the same one that pushes teams toward a backend for frontend per client.

Slide 31 names the fifth house Artwork; slide 32 names it Access. Artwork appears in the BusinessDomain enumeration on slide 48, and an AccessBearingEntity appears separately on slide 47, so Artwork is the likelier fifth domain.

![Slide 31: Five houses, one roof. One codebase, one build, one deploy. Content, Games, Ads, Financial and Artwork business entities behind CI-enforced boundaries over a shared Legal Entity core: exactly one legal identity, a tax ID is unique.](../slides/stop-fighting-the-remodel/deep/p31.webp)

Slide 31. Five domain models, one deployable, one legal core.

![Slide 32: Quiz, how many cables does this take? 100 apps wired to five houses; options 5, 100, 105 and 500.](../slides/stop-fighting-the-remodel/deep/p32.webp)

Slide 32. 100 apps × 5 houses = 500 connections.

### Episode 7: one graph, asked precisely (slides 34–36)

Netflix’s answer to fan-out is GraphQL Federation, built on its open-source Domain Graph Service (DGS) framework. Each team owns its subgraph and only its fields; a router composes them into one graph, so consumers make one query with no service-to-service orchestration between them. One change lands in one team’s subgraph, which shrinks the blast radius. Slide 34 shows a large “4,000” with no unit; she said it in the room as microservices. Netflix’s published figures are different (see Numbers we checked).

Because a GraphQL query names exactly the fields it needs, it also addresses stamp coupling. Her example query on slide 36 pulls an ads entity, its core vendor and its ads organization from three subgraphs, plus gateway request details, and nothing else. She contrasted that with large protobuf payloads passed through gRPC services.

![Slide 35: Federated GraphQL, every team owns its subgraph. Accounts, Catalog and Interactions subgraphs compose through a router to TV, mobile and web clients. One subgraph per domain; one change, one team; the router composes.](../slides/stop-fighting-the-remodel/deep/p35.webp)

Slide 35. One subgraph per domain; the router composes.

![Slide 36: Ask for exactly what you need. A GraphQL query for ads entities by ID that joins three subgraphs: entity, core vendor and ads organization, plus gateway request details.](../slides/stop-fighting-the-remodel/deep/p36.webp)

Slide 36. One query joins three subgraphs and asks for nothing more.

### Episode 7: the N+1 fix in production (slides 37–41)

GraphQL resolvers invite the N+1 problem: one query for a list of shows, then one call per show to an artwork service, then one database query per item. Her analogy was a waiter who takes ten orders at one table and walks to the kitchen ten times. Batch loading writes every order on one ticket: collect every key, run the loader once, send one request.

To get real numbers, she had an engineer new to DGS implement a feature that needed a data loader and test it at batch sizes of 5,000 and 10,000. The before-and-after came from production:

| Measure                            | Before      | After         |
|------------------------------------|-------------|---------------|
| Slowest requests (p99), daily peak | up to 7.2 s | 1.4 s or less |
| Typical request (p50)              | ~0.4 s      | unchanged     |
| Calls in the sample                | 396         | 78            |
| Calls over 2 seconds               | 66 (17%)    | 0             |
| Calls under 0.5 seconds            | 51%         | 83%           |

The fix removed the multi-second tail on requests with large batches; typical requests didn’t change. She also claimed about 20% lower cost, which isn’t on the slides. The recording has her saying p99 fell to “24 seconds”, a transcription error; slide 40 says under 1.4 seconds.

![Slide 40: N+1, fixed in prod. Slowest requests up to about 7 seconds before (peak 7.2s), under 1.4 seconds after. Typical requests at about 0.4 seconds didn't change.](../slides/stop-fighting-the-remodel/deep/p40.webp)

Slide 40. p99 peak from 7.2 s to under 1.4 s.

![Slide 41: Fewer calls, no slow tail. Before: 396 calls, 66 over 2 seconds (17%). After: 78 calls, none over 2 seconds; 83% under 0.5 seconds.](../slides/stop-fighting-the-remodel/deep/p41.webp)

Slide 41. 396 calls to 78; none over 2 seconds.

### Walls between the houses, and an ontology (slides 42–48)

The new service runs on a managed runtime backed by RAW Hollow, Netflix’s in-memory, co-located object store with optional strong consistency. The store is split into namespaces (ads, legal, core vendor), and only the owning domain service may write to its namespace; that is what makes the walls real. Writes across namespaces go through asynchronous workflows, and a proxy forwards writes to the legacy Vendor Service while it still exists.

To enforce the boundaries in the model itself, the team uses UDA and its metamodel, Upper. An ontology is a machine-readable graph of what exists, how things relate and with what cardinality. Defining a domain class takes seven steps:

| Step                | Netflix’s example                                                  | What it buys                                                                   |
|---------------------|--------------------------------------------------------------------|--------------------------------------------------------------------------------|
| Trait               | Entity: an id, one core vendor, one or more domains                | One legal entity can carry many business domains; no copy per line of business |
| Direct class        | CoreVendor, with Ads and Games business entities pointing to it    | The unique legal-entity invariant has a home                                   |
| Primary key         | id                                                                 | Every record is addressable                                                    |
| Enumeration         | BusinessDomain: ADS, GAMES, ARTWORK, PUBLISHING, PRODUCTION, LEGAL | Replaces the “this vendor is really a game” string                             |
| Relationship        | Games business entity to zero or more game productions             | Cardinality is explicit, not implied                                           |
| Implement the trait | Ads business entity is an Entity                                   | Questions can be asked across types without knowing them                       |
| Fuse across domains | Links to ADS_Organization and NPP_Partner, owned by other teams    | Point by key, never copy                                                       |

Slide 44 shows the trait’s core vendor as exactly one (1..1); slide 51 shows it as zero or one for Ads and Games and exactly one for Artwork. Worth asking which is current.

![Slide 42: Walls inside one house. Domain services each write only their own RAW Hollow namespace (ads, legal, coreVendor); callers use DGS queries and writes; a proxy forwards writes to the legacy Vendor Service.](../slides/stop-fighting-the-remodel/deep/p42.webp)

Slide 42. Namespaces in RAW Hollow are the walls.

![Slide 44: Trait, a shared contract at rdf.netflix.net/onto/v2b#Entity. Anything that is an Entity has an id, one core vendor and one or more domains.](../slides/stop-fighting-the-remodel/deep/p44.webp)

Slide 44. The Entity trait: one core vendor, many domains.

### UDA: model once, represent everywhere (slides 49–53)

Every concept in UDA has a URI, using the W3C’s RDF, so when a concept crosses team boundaries it is referenced like a web address, and the same URI identifies it in the federated graph. From one model, UDA generates the GraphQL type, an Avro record for Netflix’s Data Mesh platform and an Iceberg table. Change the model and every container follows, so they don’t drift. Upper is self-describing, self-referencing and self-validating: it validates every model, including itself, with SHACL.

Her return-on-investment case was search. A plain search for “partners” matches five different concepts. A context-aware search for “game partners for Northwind Media” resolves to the games-partner concept, finds the core vendor, and knows where it lives in the GraphQL subgraph, search index and Iceberg table, across teams. She argued that semantic meaning matters more now because agents, like people, need to know what a field means to use an API correctly.

![Slide 50: One Vendor, 6+ shapes, zero drift. The domain model is projected by UDA into a GraphQL type, an Avro record for Data Mesh and an Iceberg table. Change the model once and every container follows.](../slides/stop-fighting-the-remodel/deep/p50.webp)

Slide 50. One model projected to GraphQL, Avro and Iceberg.

![Slide 53: Context-aware search for game partners for Northwind Media resolves to the games partner concept and the core vendor, found in the GraphQL subgraph, search index and Iceberg table.](../slides/stop-fighting-the-remodel/deep/p53.webp)

Slide 53. Search that knows what “partner” means.

### Episode 8: someone else is on the roof (slides 54–57)

The roofer who cracked her roof was someone she hired. Agents calling Netflix’s APIs are often hired by a coworker, and nobody told them to stay off the roof. She framed three questions, each with a guardrail the team has built:

| Question                           | Guardrail                  | How it works                                                                                                                                                                                  |
|------------------------------------|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Who’s up there, and who sent them? | Agentic identity           | Each call carries the agent’s own name and principal ID, and separately the end user’s end-to-end token. “On behalf of” is not optional.                                                      |
| Where may they step?               | Declarative agent policies | Authorization asks two questions: can this person see it, and should an agent do it for them? Data is tagged once and the platform enforces it, instead of a check copied into every backend. |
| What did they touch?               | Agent audit logs           | 300K agent calls (all reads) and 6,000 agent writes of synthetic test data, plus calls from agents that don’t identify themselves and look like a person or an app.                           |

In the room she put the 300K calls in the last 180 days and said most came from people using agents to explore Netflix’s systems; the 6,000 writes came from an agent generating synthetic data to reproduce the N+1 problem. Next, the team plans to deny calls that lack an on-behalf-of token. “Quiet doesn’t mean safe,” slide 57 says. “It may mean unlabelled.”

![Slide 55: Agentic identity, know who's asking. The agent's own name and principal ID, and the person it acts for with an end-to-end user token. On behalf of is not optional.](../slides/stop-fighting-the-remodel/deep/p55.webp)

Slide 55. Agent identity plus the end user’s token.

![Slide 57: Agentic observability. 300K agent calls, all reads; 6,000 agent writes, synthetic data in test; some agents don't say so. Quiet doesn't mean safe.](../slides/stop-fighting-the-remodel/deep/p57.webp)

Slide 57. What the audit logs found.

### Episode 8: re-roofing while the family lives there (slides 58–62)

The migration follows the strangler fig pattern, in six stages:

| Stage               | What happens                                     | At Netflix                                                                                    |
|---------------------|--------------------------------------------------|-----------------------------------------------------------------------------------------------|
| 1\. Scaffold        | Build the new beside the old                     | Ads business entities modeled first in the new service, with new consumers on it              |
| 2\. Stop digging    | New features land only in the new model          | No new features on the legacy vendor service                                                  |
| 3\. Facade          | One contract in front of both models             | Legacy consumers keep the old API while work happens behind it                                |
| 4\. Lure            | Make the new house nicer and leave the door open | Agent identity, semantic meaning and fine-grained access only in the new service              |
| 5\. Flip the source | The new model becomes the source of truth        | Shadow writes, then reads from the new system checked against the old, then writes to the new |
| 6\. Tear off        | Retire the old once the last consumer leaves     | Not reached yet; planned for 2027, per the recording                                          |

She said 62 consumers had migrated and 38 had not; that slide wasn’t captured. Her principle: an API change should not mean a forced migration for every other team. Consumers move when they choose. In Q&A she explained that the facade works in both directions: at first it sends unchanged consumers to the legacy system, and after the flip it lets the old API write to the new system. Her team does the translation work, not the consumers. Asked how she sold it to leadership, she pointed to Netflix’s freedom-and-responsibility culture: show the business return, then deliver it.

![Slide 59: Strangler fig, nobody moves out. Six stages: Scaffold, Stop digging, Facade, Lure, Flip the source, Tear off. 100+ consumers, zero downtime.](../slides/stop-fighting-the-remodel/deep/p59.webp)

Slide 59. Six stages, 100+ consumers, zero downtime.

![Slide 61: Stage 5, Flip the source. Writes stay on the original while a shadow copy is built via the facade, then reads move to the new system while writes go to the old, then the new system becomes the source of truth.](../slides/stop-fighting-the-remodel/deep/p61.webp)

Slide 61. Flipping the source of truth in three moves.

### Episode 9: takeaways (slides 63–67)

**Score the leak.** Count the five signs in one part of your system, keep a scorecard rather than a hunch, and measure the same way every time.

**Keep change local.** Split by reason to change (one context, one meaning, one owner), serve it as one federated graph, and write the meaning once in a model that generates the schemas.

**Migrate without disruption.** One facade, one stage at a time; deprecate, don’t break.

Her closing advice was to expect change: get past the mental block, pick a small greenfield use case as the first bite, and build the muscle with small changes. Agents will make code easier to write, she said, but not easier to get right.

![Slide 63: Takeaway 1, score the leak. Count the five signs, keep a scorecard not a hunch, read the score.](../slides/stop-fighting-the-remodel/deep/p63.webp)

Slide 63. Takeaway 1: score the leak.

![Slide 64: Takeaway 2, keep change local. Split by reason to change; serve it as one graph with federated GraphQL; write the meaning once in UDA and generate the schema from it.](../slides/stop-fighting-the-remodel/deep/p64.webp)

Slide 64. Takeaway 2: keep change local.

## Numbers we checked

Every figure in the talk against its source. Checked means we found it in a published source or reran the arithmetic; Caveat means it holds with a condition; Slide only means we took it from the slide; Talk only means we heard it in the room and found it nowhere else.

| Claim                                                           | Figure           | Source                                                                                                                                                                                                                           | Status                                         |
|-----------------------------------------------------------------|------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------|
| Apps consuming CBP Foundations’ data                            | 100+             | Slides 12, 59                                                                                                                                                                                                                    | Slide only                                     |
| Person records in Entity Services                               | 1.7M             | Slide 13 (the recording says 17 million)                                                                                                                                                                                         | Slide only                                     |
| Vendor records                                                  | 225K             | Slide 13                                                                                                                                                                                                                         | Slide only                                     |
| Requests per second; share of calls under 1 s                   | 10K–20K; 99%     | Recording; charts on slides 14–15 unreadable                                                                                                                                                                                     | Talk only                                      |
| Connections for 100 apps × 5 domains                            | 500              | Slide 32; 100 × 5 = 500                                                                                                                                                                                                          | Checked                                        |
| Scale of the federated graph                                    | “4,000”          | Slide 34 gives no unit; said as microservices. [InfoQ, 2022](https://www.infoq.com/news/2022/10/scaling-graphql-netflix/): 10,000+ types and fields, 500+ developers                                                             | Caveat unit unclear; not matched in any source |
| Requests per day through the graph                              | 1B+              | Recording; [InfoQ, 2022](https://www.infoq.com/news/2022/10/scaling-graphql-netflix/)                                                                                                                                            | Checked                                        |
| Federation open-sourced                                         | 2020             | [Netflix TechBlog, Nov 2020](https://netflixtechblog.com/how-netflix-scales-its-api-with-graphql-federation-part-1-ae3557c187e2); DGS open-sourced [early 2021](https://www.infoq.com/news/2021/02/netflix-graphql-spring-boot/) | Caveat the post was 2020; the framework 2021   |
| p99 latency, before and after batch loading                     | 7.2 s → ≤1.4 s   | Slide 40 (the recording says 24 s, an error)                                                                                                                                                                                     | Slide only                                     |
| Drop in tail latency                                            | ~80%             | Recording; (7.2 − 1.4) / 7.2 = 81% from slide 40                                                                                                                                                                                 | Checked arithmetic                             |
| Calls before and after; calls over 2 s                          | 396 → 78; 66 → 0 | Slide 41; 66 / 396 = 16.7%, shown as 17%                                                                                                                                                                                         | Slide only                                     |
| Lower cost after the fix                                        | ~20%             | Recording                                                                                                                                                                                                                        | Talk only                                      |
| RAW Hollow: in-memory, co-located, strong consistency available | n/a              | [Netflix TechBlog on Tudum](https://netflixtechblog.com/netflix-tudum-architecture-from-cqrs-with-kafka-to-cqrs-with-raw-hollow-86d141b72e52)                                                                                    | Checked                                        |
| UDA built on RDF and SHACL; projects to GraphQL, Avro, Iceberg  | n/a              | [Netflix TechBlog, June 2025](https://netflixtechblog.com/uda-unified-data-architecture-6a6aee261d8d)                                                                                                                            | Checked                                        |
| Agent calls, all reads                                          | 300K             | Slide 57; “last 180 days” from the recording                                                                                                                                                                                     | Slide only                                     |
| Agent writes, synthetic test data                               | 6,000            | Slide 57                                                                                                                                                                                                                         | Slide only                                     |
| Consumers migrated vs not yet                                   | 62 / 38          | Recording; slide not captured                                                                                                                                                                                                    | Talk only                                      |
| Roof leaks found; year                                          | 7+; Oct 2024     | Slides 3, 5 (an earlier draft from the recording said 2020)                                                                                                                                                                      | Slide only                                     |
| *Microservices Patterns* publication year                       | 2018             | Slide 26; [O’Reilly listing, Nov 2018](https://www.oreilly.com/library/view/-/9781617294549)                                                                                                                                     | Checked                                        |

## About the speaker

Aarti Gupta is a Staff Engineer at Netflix with more than 16 years of experience building distributed systems and platform architecture, according to her [QCon speaker page](https://qconsf.com/speakers/aartigupta2). She holds a master’s in computer science from the University of Southern California. At Netflix she works on Entity Services in CBP Foundations, the shared data and API layer under Netflix’s studio, content and ads apps. Her closing slide lists linkedin.com/in/aarti-gupta. The track host said hers was the first abstract she wanted for the track.

## Terms and technologies

Everything the talk names, in plain English, with a link to the real thing.

### The five signs

[Polysemy](https://en.wikipedia.org/wiki/Polysemy)  
One word carrying several related meanings. In software it shows up when one shared type, here Vendor, means something different to each team that uses it.

[Data invariant](https://en.wikipedia.org/wiki/Invariant_(computer_science))  
A rule the system promises is always true, such as “a partner has exactly one legal identity”. Breaking one to fit a new business case is her second sign.

[Blast radius](https://en.wikipedia.org/wiki/Connascence)  
How far one change travels before everything is consistent again. No canonical page; linked to connascence, which gives a vocabulary for it. At Netflix, one schema change could reach 100+ consumers.

[Stamp coupling](https://en.wikipedia.org/wiki/Connascence)  
A classic coupling type: passing a whole data structure to code that uses only part of it, so the callee depends on fields it never needed. Listed among the traditional coupling types on this page.

[Connascence](https://en.wikipedia.org/wiki/Connascence)  
Meilir Page-Jones’s measure of coupling: two parts are connascent if changing one forces a change in the other to stay correct. Her example was a string convention that every consumer had to know.

### Architecture patterns

[Service-oriented architecture (SOA)](https://en.wikipedia.org/wiki/Service-oriented_architecture)  
An approach where capabilities sit behind explicit service contracts. The lesson she kept: ask the service, don’t read its database.

[Domain-driven design (DDD)](https://en.wikipedia.org/wiki/Domain-driven_design)  
Eric Evans’s 2003 approach of modeling software on the business domain and its language.

[Bounded context](https://martinfowler.com/bliki/BoundedContext.html)  
DDD’s boundary within which one model and one vocabulary apply. It lets “vendor” mean different things in Ads and Finance without conflict.

[Anti-corruption layer](https://learn.microsoft.com/azure/architecture/patterns/anti-corruption-layer)  
A translation layer between two systems or contexts with different models, so neither has to adopt the other’s.

[Modular monolith](https://microservices.io/post/architecture/2024/09/09/modular-monolith-patterns-for-fast-flow.html)  
One deployable organized as domain modules with enforced boundaries. Her “five houses, one roof” is this shape; the slide’s cut-off fourth era likely reads “Modular”.

N×M fan-out  
When N clients each call M services directly, connections multiply. 100 apps and 5 domains means 500. Federation replaces it with one graph.

[Backend for frontend (BFF)](https://samnewman.io/patterns/architectural/bff/)  
Sam Newman’s pattern of a dedicated backend per client experience; she named it as where teams often meet the fan-out problem.

[Strangler fig](https://martinfowler.com/bliki/StranglerFigApplication.html)  
Martin Fowler’s name for replacing a legacy system gradually, growing the new around the old until the old can be removed. Her six stages are one version of it.

[Parallel change](https://martinfowler.com/bliki/ParallelChange.html)  
Also called expand and contract: change an interface by supporting old and new side by side, migrate callers, then remove the old. On her reading list.

### APIs and GraphQL

[GraphQL](https://graphql.org)  
A query language for APIs where the client names exactly the fields it wants, which is why she presented it as a cure for stamp coupling.

[GraphQL Federation](https://www.apollographql.com/docs/federation/v2/subgraphs/)  
Combining many GraphQL services (subgraphs) into one graph behind a router. Each team owns its subgraph; clients see one API. Netflix adopted the Apollo Federation spec.

[DGS framework](https://netflix.github.io/dgs/)  
Netflix’s open-source Domain Graph Service framework for building GraphQL services on Spring Boot, including federation support and code generation.

[gRPC](https://grpc.io)  
A remote-procedure-call framework. One of the API projections on slide 16; she contrasted its large payloads with GraphQL’s field selection.

[Protocol Buffers](https://protobuf.dev)  
The binary message format gRPC uses.

[N+1 problem](https://www.graphql-js.org/docs/n1-dataloader/)  
One query for a list followed by one more query per item. Common in GraphQL because each field has its own resolver.

[DataLoader (batch loading)](https://github.com/graphql/dataloader)  
A pattern, first released by Facebook, that collects the keys requested during one query and fetches them in a single batch. DGS supports it for Java.

### Data and modeling

[Hollow and RAW Hollow](https://hollow.how)  
Hollow is Netflix’s open-source Java library for distributing in-memory datasets to many consumers. RAW Hollow is its read-after-write version: the whole dataset in each service’s memory, with strong consistency available per request. Netflix described it in its [Tudum post](https://netflixtechblog.com/netflix-tudum-architecture-from-cqrs-with-kafka-to-cqrs-with-raw-hollow-86d141b72e52).

[UDA (Unified Data Architecture)](https://netflixtechblog.com/uda-unified-data-architecture-6a6aee261d8d)  
Netflix’s knowledge graph that connects business concepts to the schemas and data containers that hold them, so a domain is modeled once and projected everywhere.

Upper  
UDA’s metamodel, the model of models in which every domain class, attribute, key and relationship is defined. It describes, references and validates itself. Described in the UDA post.

[Ontology](https://en.wikipedia.org/wiki/Ontology_(information_science))  
A formal, machine-readable description of the concepts in a domain and how they relate. She called it a dictionary that software can read.

[RDF](https://www.w3.org/TR/rdf11-primer/)  
The W3C’s Resource Description Framework, which describes things as linked statements identified by URIs. UDA uses it so every concept has a web-style address.

[SHACL](https://www.w3.org/TR/shacl/)  
The W3C Shapes Constraint Language for validating RDF data against rules such as cardinality. UDA uses it for validation.

[Apache Avro](https://avro.apache.org/)  
A schema-based binary format for records, common in streaming pipelines. One of UDA’s generated projections.

[Data Mesh (Netflix)](https://netflixtechblog.com/data-mesh-a-data-movement-and-processing-platform-netflix-1288bcab2873)  
Netflix’s internal platform for moving and processing data between systems. Not the same thing as Zhamak Dehghani’s [data mesh](https://martinfowler.com/articles/data-mesh-principles.html) principles, though related.

[Apache Iceberg](https://iceberg.apache.org/)  
An open table format for large analytic datasets, created at Netflix. UDA can generate Iceberg tables from the model.

### Agents

[Agentic identity and on-behalf-of tokens](https://www.iana.org/go/rfc8693)  
Giving each agent its own identity and carrying, separately, the identity of the user it acts for. OAuth 2.0 Token Exchange (RFC 8693) is the standard for this kind of delegation; Netflix didn’t say which mechanism it uses.

Declarative agent policies  
Access rules stated once against tagged data and enforced by the platform, rather than checks re-implemented in each backend. Netflix’s version asks whether the person may see the data and whether an agent may act for them.

Agent audit logs  
Logs that record which agent called which API for whom. Netflix uses them to measure agent traffic and spot unlabelled agents.

## Reading and tools

### From her further-reading slide

- [Patterns of Legacy Displacement](https://martinfowler.com/articles/patterns-legacy-displacement), Ian Cartwright, Rob Horn and James Lewis, martinfowler.com.
- [Parallel Change](https://martinfowler.com/bliki/ParallelChange.html), Danilo Sato, martinfowler.com, 2014.
- [Microservices Patterns, chapter 13: Refactoring to microservices](https://livebook.manning.com/book/microservices-patterns/chapter-13), Chris Richardson, Manning, 2018. A second edition is in early access.
- [Principles of Web API Design](https://www.oreilly.com/library/view/principles-of-web/9780137355754/), James Higginbotham, Addison-Wesley, 2021.
- [Model Once, Represent Everywhere: UDA at Netflix](https://netflixtechblog.com/uda-unified-data-architecture-6a6aee261d8d), Netflix TechBlog, June 2025.

### Netflix sources behind the talk

- [How Netflix Scales its API with GraphQL Federation (Part 1)](https://netflixtechblog.com/how-netflix-scales-its-api-with-graphql-federation-part-1-ae3557c187e2), Netflix TechBlog, 2020. Shown on slide 34.
- [Scaling GraphQL at Netflix](https://www.infoq.com/news/2022/10/scaling-graphql-netflix/), InfoQ, 2022. The 1B+ requests a day and 10,000+ types figures.
- [Netflix Tudum Architecture: from CQRS with Kafka to CQRS with RAW Hollow](https://netflixtechblog.com/netflix-tudum-architecture-from-cqrs-with-kafka-to-cqrs-with-raw-hollow-86d141b72e52), Netflix TechBlog, 2025.
- [DGS framework documentation](https://netflix.github.io/dgs/) and [Hollow documentation](https://hollow.how).

### Related sessions at QCon

- **Still ahead** Tue 1:35: [Drawing the Rest of the Owl: A Blueprint for Your Software Factory](https://qconsf.com/presentation/nov2026/drawing-rest-owl-blueprint-your-software-factory) (Harness).
- **Still ahead** Tue 2:45: [Lessons from Building a \$100M Product in Six Weeks at OpenAI](https://qconsf.com/presentation/nov2026/lessons-building-100m-product-six-weeks-openai).
- **Still ahead** Wed 10:35: [How Netflix Retrofitted Its SDLC for AI Coding Agents](https://qconsf.com/presentation/nov2026/how-netflix-retrofitted-its-sdlc-ai-coding-agents), another Netflix view of agents in the SDLC.
- **Still ahead** Wed 11:45: [Making Production Legible to Agents](https://qconsf.com/presentation/nov2026/making-production-legible-agents-lessons-building-observability-mcp) (Honeycomb).
- **Still ahead** Wed 3:55: [How To Kill the Code Review](https://qconsf.com/presentation/nov2026/how-kill-code-review) (Aviator).

## All slides

[![Slide 1: Title card: A software engineer's accidental education in roofing. Roofing Science 101. Track: Modern API Design for Humans and Agents.](../slides/stop-fighting-the-remodel/deep/p01.webp)](../slides/stop-fighting-the-remodel/deep/p01.webp)

Slide 1. Title card

[![Slide 2: Episode 1, The Roof. Hi, I'm Aarti Gupta: roofing expert by necessity, software engineer by trade. Staff Engineer at Netflix, team CBP Foundations (Content and Business Products), based in the Bay Area.](../slides/stop-fighting-the-remodel/deep/p02.webp)](../slides/stop-fighting-the-remodel/deep/p02.webp)

Slide 2. Introduction

[![Slide 3: October 2024. I was forced to become a roofing expert. 7+ places where the roof was leaking, with photos of the shakes, a ceiling crack and the floor.](../slides/stop-fighting-the-remodel/deep/p03.webp)](../slides/stop-fighting-the-remodel/deep/p03.webp)

Slide 3. October 2024: 7+ leaks

[![Slide 4: We learn the science under the hood. Cemwood, installed on her roof in 1998: 2 to 1 cement to wood, pressed to look like cedar shake, fire-safe, 50-year warranty.](../slides/stop-fighting-the-remodel/deep/p04.webp)](../slides/stop-fighting-the-remodel/deep/p04.webp)

Slide 4. Cemwood

[![Slide 5: Roof can last another 25 years. The 2020 disclosure said the roof may last another 25 years with proper care; four years later, in 2024, 7+ leaks were found.](../slides/stop-fighting-the-remodel/deep/p05.webp)](../slides/stop-fighting-the-remodel/deep/p05.webp)

Slide 5. The disclosure vs four years later

[![Slide 6: Outsource the problem. The roofer took one step onto the roof and it cracked.](../slides/stop-fighting-the-remodel/deep/p06.webp)](../slides/stop-fighting-the-remodel/deep/p06.webp)

Slide 6. Outsource the problem

[![Slide 7: Spec vs reality: 50 years warranted at installation, 25 years left according to the disclosure, 1 step to set off a ripple of cracks. Stay off the roof.](../slides/stop-fighting-the-remodel/deep/p07.webp)](../slides/stop-fighting-the-remodel/deep/p07.webp)

Slide 7. Spec vs reality

[![Slide 8: So the only way forward: a complete replacement, since patching was ruled out. A lift and shift is how her kid imagined it.](../slides/stop-fighting-the-remodel/deep/p08.webp)](../slides/stop-fighting-the-remodel/deep/p08.webp)

Slide 8. The only way forward

[![Slide 9: Why talk about roofs at a software conference? 01 composite failures: small cracks compound. 02 turning a blind eye: someone always saw it coming. 03 remodels are costly: migrations are elaborate and time-intensive.](../slides/stop-fighting-the-remodel/deep/p09.webp)](../slides/stop-fighting-the-remodel/deep/p09.webp)

Slide 9. Why roofs at a software conference

[![Slide 10: The roof carries the same load year after year; software faces changing models, ownership moves, workflows that cross, splits, merges and moving boundaries. AI accelerates the change.](../slides/stop-fighting-the-remodel/deep/p10.webp)](../slides/stop-fighting-the-remodel/deep/p10.webp)

Slide 10. Roofs stay put, software doesn't

[![Slide 11: Today, three questions. How do you know your roof is leaking (five diagnostic signs). Patch it or replace it, and how to redraw the boundaries. How do you re-roof without moving out: migrating 100+ consumers with zero downtime.](../slides/stop-fighting-the-remodel/deep/p11.webp)](../slides/stop-fighting-the-remodel/deep/p11.webp)

Slide 11. Three questions

[![Slide 12: Episode 2, At Netflix. Content and Business Products Foundations. Who are our consumers? 100+ apps consume our data, under Content, Ads, Studio and more, all built on CBP Foundations.](../slides/stop-fighting-the-remodel/deep/p12.webp)](../slides/stop-fighting-the-remodel/deep/p12.webp)

Slide 12. 100+ consuming apps

[![Slide 13: Entity Services, the team she works on: foundational entities in a connected knowledge graph. 1.7M person records and 225K vendor records; a users figure is cut off in the photo.](../slides/stop-fighting-the-remodel/deep/p13.webp)](../slides/stop-fighting-the-remodel/deep/p13.webp)

Slide 13. Entity Services

[![Slide 14: Chart of requests per second over Sep 25 to 30. Axis values are not readable in the photo.](../slides/stop-fighting-the-remodel/deep/p14.webp)](../slides/stop-fighting-the-remodel/deep/p14.webp)

Slide 14. Requests per second

[![Slide 15: Chart of p99 latency over the same week. Axis values are not readable in the photo.](../slides/stop-fighting-the-remodel/deep/p15.webp)](../slides/stop-fighting-the-remodel/deep/p15.webp)

Slide 15. Latency p99

[![Slide 16: The API powers the business. APIs are projections, one per use case: GraphQL schema, gRPC service and an internal IPC. A mapping layer sits between them and the domain model, which sits on the data model: vendor tables and RAW Hollow objects.](../slides/stop-fighting-the-remodel/deep/p16.webp)](../slides/stop-fighting-the-remodel/deep/p16.webp)

Slide 16. The API powers the business

[![Slide 17: Where the leak actually was: in the domain model layer, one Vendor with five meanings, between the API projections above and the invariants and data model below.](../slides/stop-fighting-the-remodel/deep/p17.webp)](../slides/stop-fighting-the-remodel/deep/p17.webp)

Slide 17. Where the leak was

[![Slide 18: The supply chain was drawn as one line with two ends: a content partner makes an asset and a fulfillment partner delivers it. Then Spotify (The Rewatchables, live on Netflix) both produces and delivers: one partner, two roles.](../slides/stop-fighting-the-remodel/deep/p18.webp)](../slides/stop-fighting-the-remodel/deep/p18.webp)

Slide 18. One line, two ends

[![Slide 19: Episode 3, The leak at Netflix. Amber Studio is one business with one tax ID, but World of Peppa Pig and Play With Fire each got their own partner key, so the same vendor was copied per title.](../slides/stop-fighting-the-remodel/deep/p19.webp)](../slides/stop-fighting-the-remodel/deep/p19.webp)

Slide 19. Amber Studio: one business, many keys

[![Slide 20: Inversions of money and time. Every other vendor is paid by Netflix, but advertisers pay Netflix. For live and sports, the rights window comes before the asset exists.](../slides/stop-fighting-the-remodel/deep/p20.webp)](../slides/stop-fighting-the-remodel/deep/p20.webp)

Slide 20. Inversions of money and time

[![Slide 21: Signs your roof is leaking. 01 A polyseme: one word, vendor, means a content or fulfillment partner in Content, a studio with many titles in Games, an advertiser who pays us in Ads and a payee with one tax ID in Finance. Force one model to hold them all and you get the tangle.](../slides/stop-fighting-the-remodel/deep/p21.webp)](../slides/stop-fighting-the-remodel/deep/p21.webp)

Slide 21. Sign 1: a polyseme

[![Slide 22: 02 Incorrect data invariants: the business broke core invariants such as a partner has exactly one legal identity and a partner's tax ID is unique. Invariants aren't fields; you can't split them by moving a column.](../slides/stop-fighting-the-remodel/deep/p22.webp)](../slides/stop-fighting-the-remodel/deep/p22.webp)

Slide 22. Sign 2: broken invariants

[![Slide 23: 03 Blast radius: how far a single change travels. Internal domain structures leak to every consumer, and one schema change becomes a 100-team refactor.](../slides/stop-fighting-the-remodel/deep/p23.webp)](../slides/stop-fighting-the-remodel/deep/p23.webp)

Slide 23. Sign 3: blast radius

[![Slide 24: 04 Stamp coupling: passing a whole composite structure to a module that needs one piece. A vendor object with legal metadata, global licensing rights, tax identity and hierarchy was handed to a module that only mints an API key.](../slides/stop-fighting-the-remodel/deep/p24.webp)](../slides/stop-fighting-the-remodel/deep/p24.webp)

Slide 24. Sign 4: stamp coupling

[![Slide 25: 05 Connascence: a change in one module requires a change in another to stay correct. Overloading a string field to say this vendor is really a game title means every downstream service must share the convention or break at runtime.](../slides/stop-fighting-the-remodel/deep/p25.webp)](../slides/stop-fighting-the-remodel/deep/p25.webp)

Slide 25. Sign 5: connascence

[![Slide 26: Episode 5, The search for a fix. If you find yourself in a hole, stop digging. Quote from Chris Richardson, Microservices Patterns (2018): don't add new features to the monolith, implement them as services. Steps: stop digging, new features as services, strangle the monolith.](../slides/stop-fighting-the-remodel/deep/p26.webp)](../slides/stop-fighting-the-remodel/deep/p26.webp)

Slide 26. Stop digging

[![Slide 27: Different boundaries, same pressures: SOA in the 2000s, DDD from Evans in 2003, microservices around 2014, and now, in the AI era, a modular approach. Each pattern is another move to recognize and reuse.](../slides/stop-fighting-the-remodel/deep/p27.webp)](../slides/stop-fighting-the-remodel/deep/p27.webp)

Slide 27. Different boundaries, same pressures

[![Slide 28: SOA, 1996 to 2004: boundaries are explicit. Capabilities sit behind explicit contracts and are crossed only by message. Kept: ask the service, don't read its data. The contract is the wall.](../slides/stop-fighting-the-remodel/deep/p28.webp)](../slides/stop-fighting-the-remodel/deep/p28.webp)

Slide 28. SOA

[![Slide 29: Bounded contexts, Domain-Driven Design, 2003: an anti-corruption layer translates between contexts. Split the model: in Ads, vendor means an advertiser; in Finance, a payee we pay; in Games, a studio with many titles.](../slides/stop-fighting-the-remodel/deep/p29.webp)](../slides/stop-fighting-the-remodel/deep/p29.webp)

Slide 29. Bounded contexts

[![Slide 30: Microservices, around 2014: own it, ship it alone. One team, one service, one database. Pros: teams ship without waiting, one bug stays in one service. Cons: every call crosses the network; cut too small, one change needs many deploys. Self deployment equals self governance.](../slides/stop-fighting-the-remodel/deep/p30.webp)](../slides/stop-fighting-the-remodel/deep/p30.webp)

Slide 30. Microservices

[![Slide 31: Episode 6, Re-roofing at Netflix. Five houses, one roof: one codebase, one build, one deploy, with Content, Games, Ads, Financial and Artwork business entities behind CI-enforced boundaries over a shared Legal Entity core: exactly one legal identity, and a tax ID is unique.](../slides/stop-fighting-the-remodel/deep/p31.webp)](../slides/stop-fighting-the-remodel/deep/p31.webp)

Slide 31. Five houses, one roof

[![Slide 32: Quiz: how many cables does this take? 100 apps wired to five houses (Content, Games, Ads, Finance, Access). Options 5, 100, 105, 500; the answer is 500, apps times houses.](../slides/stop-fighting-the-remodel/deep/p32.webp)](../slides/stop-fighting-the-remodel/deep/p32.webp)

Slide 32. Quiz: how many cables?

[![Slide 33: Quiz: name the problem we just described. A single point of failure, the N+1 problem, N times M fan-out, or none of the above. The answer is N times M fan-out.](../slides/stop-fighting-the-remodel/deep/p33.webp)](../slides/stop-fighting-the-remodel/deep/p33.webp)

Slide 33. Quiz: name the problem

[![Slide 34: Episode 7, The search ends. Unprecedented scale with GraphQL Federation, with a large 4,000 and a link to Netflix's blog post on scaling its API with GraphQL Federation. Callers such as vendor HQ, the ads service and UI clients hit one graph: one query in, batched, no N+1, no fan-out. DGS stitches it all together.](../slides/stop-fighting-the-remodel/deep/p34.webp)](../slides/stop-fighting-the-remodel/deep/p34.webp)

Slide 34. GraphQL Federation

[![Slide 35: Federated GraphQL: every team owns its subgraph. Accounts, Catalog and Interactions subgraphs compose through a router to TV, mobile and web. One subgraph per domain; one change, one team; the router composes and clients see one graph.](../slides/stop-fighting-the-remodel/deep/p35.webp)](../slides/stop-fighting-the-remodel/deep/p35.webp)

Slide 35. Every team owns its subgraph

[![Slide 36: Ask for exactly what you need: a GraphQL query for ads entities by ID that pulls the entity, its core vendor and its ads organization from three subgraphs plus gateway request details, and nothing more.](../slides/stop-fighting-the-remodel/deep/p36.webp)](../slides/stop-fighting-the-remodel/deep/p36.webp)

Slide 36. Ask for exactly what you need

[![Slide 37: One query, then N: the N+1 problem. One query for the list of shows, N queries to an external artwork service, and N database queries behind an inefficient fetcher.](../slides/stop-fighting-the-remodel/deep/p37.webp)](../slides/stop-fighting-the-remodel/deep/p37.webp)

Slide 37. The N+1 problem

[![Slide 38: N+1, the restaurant edition: 10 orders, 10 trips. One query for a list, then N sequential queries, one per item, like a waiter who walks to the kitchen ten times instead of writing one ticket.](../slides/stop-fighting-the-remodel/deep/p38.webp)](../slides/stop-fighting-the-remodel/deep/p38.webp)

Slide 38. N+1, restaurant edition

[![Slide 39: Batch loading: one ticket to the kitchen. Collect every key, run the loader once, send one request.](../slides/stop-fighting-the-remodel/deep/p39.webp)](../slides/stop-fighting-the-remodel/deep/p39.webp)

Slide 39. Batch loading

[![Slide 40: N+1, fixed in prod. Slowest requests: up to about 7 seconds before (p99 peak 7.2s), under 1.4 seconds after. Typical requests at about 0.4 seconds did not change; what disappeared was the multi-second slow tail.](../slides/stop-fighting-the-remodel/deep/p40.webp)](../slides/stop-fighting-the-remodel/deep/p40.webp)

Slide 40. N+1 fixed in prod

[![Slide 41: Fewer calls, no slow tail. Before the fix: 396 calls, 66 over 2 seconds (17%), 51% under 0.5 seconds. After: 78 calls, none over 2 seconds, 83% under 0.5 seconds.](../slides/stop-fighting-the-remodel/deep/p41.webp)](../slides/stop-fighting-the-remodel/deep/p41.webp)

Slide 41. Fewer calls, no slow tail

[![Slide 42: Walls inside one house: a managed runtime where each domain service writes only its own RAW Hollow namespace (ads, legal, coreVendor), callers use DGS queries and writes, and a proxy forwards writes to the legacy Vendor Service.](../slides/stop-fighting-the-remodel/deep/p42.webp)](../slides/stop-fighting-the-remodel/deep/p42.webp)

Slide 42. Walls inside one house

[![Slide 43: Building an ontology: defining a domain class in seven steps. Define the trait, define the direct class, set the primary key, define an enumeration, establish relationships, implement the trait, fuse across domains. Each is defined in Upper.](../slides/stop-fighting-the-remodel/deep/p43.webp)](../slides/stop-fighting-the-remodel/deep/p43.webp)

Slide 43. Building an ontology

[![Slide 44: Trait, a shared contract (rdf.netflix.net/onto/v2b#Entity): anything that is an Entity has an id, one core vendor and one or more domains.](../slides/stop-fighting-the-remodel/deep/p44.webp)](../slides/stop-fighting-the-remodel/deep/p44.webp)

Slide 44. Trait

[![Slide 45: Direct class, a concept with its own records (v2b#CoreVendor): every Entity points to one CoreVendor; Ads and Games business entities implement the trait.](../slides/stop-fighting-the-remodel/deep/p45.webp)](../slides/stop-fighting-the-remodel/deep/p45.webp)

Slide 45. Direct class

[![Slide 46: Relationship, a link with a count: a games business entity has zero or more game production mappings, so a games partner can work on any number of productions.](../slides/stop-fighting-the-remodel/deep/p46.webp)](../slides/stop-fighting-the-remodel/deep/p46.webp)

Slide 46. Relationship

[![Slide 47: Fuse edges, another team's concept: links to ADS_Organization and NPP_Partner owned by other teams. One-to-one means the link is mandatory; point by key, never copy.](../slides/stop-fighting-the-remodel/deep/p47.webp)](../slides/stop-fighting-the-remodel/deep/p47.webp)

Slide 47. Fuse edges

[![Slide 48: Enumeration, a fixed list of values: BusinessDomain is ADS, GAMES, ARTWORK, PUBLISHING, PRODUCTION or LEGAL, and nothing else.](../slides/stop-fighting-the-remodel/deep/p48.webp)](../slides/stop-fighting-the-remodel/deep/p48.webp)

Slide 48. Enumeration

[![Slide 49: One Vendor, 6+ shapes, zero drift. UDA: model once, represent everywhere. A projection turns the domain model into a real container such as a GraphQL type.](../slides/stop-fighting-the-remodel/deep/p49.webp)](../slides/stop-fighting-the-remodel/deep/p49.webp)

Slide 49. One vendor, 6+ shapes

[![Slide 50: The same model projected into a GraphQL type, an Avro record for Data Mesh and an Iceberg table. Change the model once and every container follows.](../slides/stop-fighting-the-remodel/deep/p50.webp)](../slides/stop-fighting-the-remodel/deep/p50.webp)

Slide 50. Every container follows

[![Slide 51: Self-validation, checked by Upper: the core vendor (the legal entity) with Ads, Games and Artwork business entities. Upper, the model for all models, validates every model including its own: self-describing, self-referencing, self-validating.](../slides/stop-fighting-the-remodel/deep/p51.webp)](../slides/stop-fighting-the-remodel/deep/p51.webp)

Slide 51. Self-validation by Upper

[![Slide 52: ROI, context-aware search: the word partners alone matches five concepts (games, ads, artwork, publishing and production partner), all tied to the core vendor, the legal entity.](../slides/stop-fighting-the-remodel/deep/p52.webp)](../slides/stop-fighting-the-remodel/deep/p52.webp)

Slide 52. Context-aware search

[![Slide 53: Searching for game partners for Northwind Media resolves to the games partner concept and the core vendor, and finds it in the GraphQL subgraph, search index and Iceberg table. Credited to Sphere and Netflix's UDA post, 2025.](../slides/stop-fighting-the-remodel/deep/p53.webp)](../slides/stop-fighting-the-remodel/deep/p53.webp)

Slide 53. Game partners for Northwind Media

[![Slide 54: Weather alert, agentic weathering. Someone else is on the roof, and nobody told it to stay off. Three questions: who's up there and who sent them (identity); where may they step (policies); what did they touch (observability).](../slides/stop-fighting-the-remodel/deep/p54.webp)](../slides/stop-fighting-the-remodel/deep/p54.webp)

Slide 54. Someone else is on the roof

[![Slide 55: Agentic identity, know who's asking: the agent carries its own name and principal ID, and the person it acts for carries an end-to-end user token. On behalf of is not optional.](../slides/stop-fighting-the-remodel/deep/p55.webp)](../slides/stop-fighting-the-remodel/deep/p55.webp)

Slide 55. Agentic identity

[![Slide 56: Agentic access policies and governance. Before: a check copied into every backend that can't tell an agent from a person. After: can this person see it, and should an agent do it for them? Tag the data once; let the platform say no.](../slides/stop-fighting-the-remodel/deep/p56.webp)](../slides/stop-fighting-the-remodel/deep/p56.webp)

Slide 56. Agent access policies

[![Slide 57: Agentic observability from audit logs: 300K agent calls, all reads; 6,000 agent writes, synthetic data in test; and some agents that don't say so and look like a person or an app. Quiet doesn't mean safe; it may mean unlabelled.](../slides/stop-fighting-the-remodel/deep/p57.webp)](../slides/stop-fighting-the-remodel/deep/p57.webp)

Slide 57. Agent audit logs

[![Slide 58: Back to the three questions: patch it or replace it, and how do you re-roof without moving out.](../slides/stop-fighting-the-remodel/deep/p58.webp)](../slides/stop-fighting-the-remodel/deep/p58.webp)

Slide 58. Back to the three questions

[![Slide 59: Strangler fig, nobody moves out. Six stages: Scaffold, Stop digging, Facade, Lure, Flip the source, Tear off. 100+ consumers, zero downtime.](../slides/stop-fighting-the-remodel/deep/p59.webp)](../slides/stop-fighting-the-remodel/deep/p59.webp)

Slide 59. Strangler fig: six stages

[![Slide 60: Stage 4, Lure: the old model drains as consumers move through the API facade when ready. Every read and write on the new service is authorized before it runs.](../slides/stop-fighting-the-remodel/deep/p60.webp)](../slides/stop-fighting-the-remodel/deep/p60.webp)

Slide 60. Stage 4: Lure

[![Slide 61: Stage 5, Flip the source: writes stay on the original while a shadow copy is built via the facade; then reads move to the new system while writes go to the old; then the new system becomes the source of truth for legacy entities via the facade.](../slides/stop-fighting-the-remodel/deep/p61.webp)](../slides/stop-fighting-the-remodel/deep/p61.webp)

Slide 61. Stage 5: Flip the source

[![Slide 62: Stage 6, Tear off: with 100% of traffic routed, the old model retires and the new UDA model is the sole model, but only after the last consumer leaves.](../slides/stop-fighting-the-remodel/deep/p62.webp)](../slides/stop-fighting-the-remodel/deep/p62.webp)

Slide 62. Stage 6: Tear off

[![Slide 63: Takeaway 1, score the leak: count the five signs (polysemy, broken invariants, blast radius, stamp coupling, connascence), keep a scorecard rather than a hunch, and read the score.](../slides/stop-fighting-the-remodel/deep/p63.webp)](../slides/stop-fighting-the-remodel/deep/p63.webp)

Slide 63. Takeaway 1: score the leak

[![Slide 64: Takeaway 2, keep change local: split by reason to change (one context, one meaning, one owner), serve it as one graph with federated GraphQL, and write the meaning once in UDA and generate the schema from it.](../slides/stop-fighting-the-remodel/deep/p64.webp)](../slides/stop-fighting-the-remodel/deep/p64.webp)

Slide 64. Takeaway 2: keep change local

[![Slide 65: Takeaway 3, migrate without disruption: one facade, one stage at a time; the strangler fig pattern; deprecate, don't break.](../slides/stop-fighting-the-remodel/deep/p65.webp)](../slides/stop-fighting-the-remodel/deep/p65.webp)

Slide 65. Takeaway 3: migrate without disruption

[![Slide 66: Expect change. In an agentic world, change is frequent. Get past the mental block, right-size the first bite with a small greenfield use case, and build the muscle with small changes first.](../slides/stop-fighting-the-remodel/deep/p66.webp)](../slides/stop-fighting-the-remodel/deep/p66.webp)

Slide 66. Expect change

[![Slide 67: Thank you. Aarti Gupta, Staff Software Engineer, Netflix. Further reading: Patterns of Legacy Displacement; Parallel Change; Microservices Patterns, chapter 13; Principles of Web API Design; Model Once, Represent Everywhere (UDA).](../slides/stop-fighting-the-remodel/deep/p67.webp)](../slides/stop-fighting-the-remodel/deep/p67.webp)

Slide 67. Thank you and further reading
