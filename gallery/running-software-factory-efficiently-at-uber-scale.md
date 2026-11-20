---
title: "Slides: Running Software Factory Efficiently at Uber Scale: Holding Agent Spend Steady While Requests Grew 9X"
---

# Slides: Running Software Factory Efficiently at Uber Scale: Holding Agent Spend Steady While Requests Grew 9X

[Back to the notes](../talks/running-software-factory-efficiently-at-uber-scale.md)

[![Slide 1: Running Software Factory Efficiently at Uber Scale, holding agent spend steady while requests grew 15X. Uday Kiran Medisetty, VP, Distinguished Engineer, Uber.](../slides/running-software-factory-efficiently-at-uber-scale/deep/s01.webp)](../slides/running-software-factory-efficiently-at-uber-scale/deep/s01.webp)

*Slide 1: Title*

[![Slide 2: 70%+ of pull requests attributed to agents, 5,000+ skills, 33K+ skill executions per day, 1,000+ MCP servers behind one gateway.](../slides/running-software-factory-efficiently-at-uber-scale/deep/s02.webp)](../slides/running-software-factory-efficiently-at-uber-scale/deep/s02.webp)

*Slide 2: Agents do a large share of the work*

[![Slide 3: four layers where agent sessions run, with five specialized agents and their cost-per-outcome units.](../slides/running-software-factory-efficiently-at-uber-scale/deep/s03.webp)](../slides/running-software-factory-efficiently-at-uber-scale/deep/s03.webp)

*Slide 3: Four layers where sessions run*

[![Slide 4: weekly active users +7x, weekly agent requests +15x, and weekly cost, Feb 2 to the week of Oct 19, 2026.](../slides/running-software-factory-efficiently-at-uber-scale/deep/s04.webp)](../slides/running-software-factory-efficiently-at-uber-scale/deep/s04.webp)

*Slide 4: Requests +15x, spend stabilized*

[![Slide 8: what we changed by term, with token price multipliers and changes for each term.](../slides/running-software-factory-efficiently-at-uber-scale/deep/s08.webp)](../slides/running-software-factory-efficiently-at-uber-scale/deep/s08.webp)

*Slide 8: What we changed, by term*

[![Slide 9 or 10: specialized agents are measured by cost per outcome.](../slides/running-software-factory-efficiently-at-uber-scale/deep/s09.webp)](../slides/running-software-factory-efficiently-at-uber-scale/deep/s09.webp)

*Slide 9: Cost per outcome*

[![Slide 11: a merged PR becomes a graded task in six steps; 1,075 graded tasks.](../slides/running-software-factory-efficiently-at-uber-scale/deep/s11.webp)](../slides/running-software-factory-efficiently-at-uber-scale/deep/s11.webp)

*Slide 11: Merged PR to graded task*

[![Slide 11, earlier build with the first two steps highlighted.](../slides/running-software-factory-efficiently-at-uber-scale/deep/s11a.webp)](../slides/running-software-factory-efficiently-at-uber-scale/deep/s11a.webp)

*Slide 11: Earlier build*

[![Slide 12: each run is an isolated agent job on Kubernetes, built by Michelangelo; time to run one model from 3 days to about 1 hour.](../slides/running-software-factory-efficiently-at-uber-scale/deep/s12.webp)](../slides/running-software-factory-efficiently-at-uber-scale/deep/s12.webp)

*Slide 12: Isolated agent jobs*

[![Slide 13: score against cost for each model and effort level, with the Pareto frontier.](../slides/running-software-factory-efficiently-at-uber-scale/deep/s13.webp)](../slides/running-software-factory-efficiently-at-uber-scale/deep/s13.webp)

*Slide 13: Score against cost*

[![Slide 14 to 17: aifx applies the same defaults to every engineer.](../slides/running-software-factory-efficiently-at-uber-scale/deep/s15.webp)](../slides/running-software-factory-efficiently-at-uber-scale/deep/s15.webp)

*Slide 15: aifx defaults*

[![Slide 14 to 17: three fleet-wide defaults set through aifx, with results.](../slides/running-software-factory-efficiently-at-uber-scale/deep/s16.webp)](../slides/running-software-factory-efficiently-at-uber-scale/deep/s16.webp)

*Slide 16: Three fleet-wide defaults*

[![Slide 14 to 17: tool schemas in context, from every installed tool to one CLI.](../slides/running-software-factory-efficiently-at-uber-scale/deep/s17.webp)](../slides/running-software-factory-efficiently-at-uber-scale/deep/s17.webp)

*Slide 17: Tool schemas to one CLI*

[![Slide 18: SaaS MCP servers go through the same gateway; 173 tool schemas kept out of context.](../slides/running-software-factory-efficiently-at-uber-scale/deep/s18.webp)](../slides/running-software-factory-efficiently-at-uber-scale/deep/s18.webp)

*Slide 18: SaaS MCPs via the gateway*

[![Slide 19 to 25: code mode runs the tool loop outside the model.](../slides/running-software-factory-efficiently-at-uber-scale/deep/s19.webp)](../slides/running-software-factory-efficiently-at-uber-scale/deep/s19.webp)

*Slide 19: Code mode*

[![Slide 19 to 25: a capable model still needs company context to answer.](../slides/running-software-factory-efficiently-at-uber-scale/deep/s20.webp)](../slides/running-software-factory-efficiently-at-uber-scale/deep/s20.webp)

*Slide 20: Company context*

[![Slide 19 to 25: agents query the AI Context Graph before they search; 55M+ nodes, 195M+ edges.](../slides/running-software-factory-efficiently-at-uber-scale/deep/s21.webp)](../slides/running-software-factory-efficiently-at-uber-scale/deep/s21.webp)

*Slide 21: AI Context Graph*

[![Slide 19 to 25: same prompt, same model, 20 minutes without the graph and 38 seconds with it.](../slides/running-software-factory-efficiently-at-uber-scale/deep/s22.webp)](../slides/running-software-factory-efficiently-at-uber-scale/deep/s22.webp)

*Slide 22: 20m vs 38s*

[![Slide 19 to 25: a live cost counter in every engineer's status line.](../slides/running-software-factory-efficiently-at-uber-scale/deep/s24.webp)](../slides/running-software-factory-efficiently-at-uber-scale/deep/s24.webp)

*Slide 24: Live cost counter*

[![Slide 26: visibility and nudges instead of hard caps.](../slides/running-software-factory-efficiently-at-uber-scale/deep/s26.webp)](../slides/running-software-factory-efficiently-at-uber-scale/deep/s26.webp)

*Slide 26: Nudges, not hard caps*

[![Slide 27 or 28: session analysis, 18 checks grouped by the term they reduce.](../slides/running-software-factory-efficiently-at-uber-scale/deep/s27.webp)](../slides/running-software-factory-efficiently-at-uber-scale/deep/s27.webp)

*Slide 27: Session analysis*

[![Slide 29: summary of what was changed in each term, with results.](../slides/running-software-factory-efficiently-at-uber-scale/deep/s29.webp)](../slides/running-software-factory-efficiently-at-uber-scale/deep/s29.webp)

*Slide 29: Summary*

[![Slide 30: questions; read more at uber.com/blog/efficient-software-factory.](../slides/running-software-factory-efficiently-at-uber-scale/deep/s30.webp)](../slides/running-software-factory-efficiently-at-uber-scale/deep/s30.webp)

*Slide 30: Questions*
