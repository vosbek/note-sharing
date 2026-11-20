---
title: "Use AI to Multiply Your Team as a Staff Engineer"
---

# Use AI to Multiply Your Team as a Staff Engineer

**Speaker:** Jordan Cutler (Senior Staff Engineer and Web Tech Lead, Pinterest)  
QCon SF 2026 · Staff+ Engineering Skills · Tue Nov 17, 11:45 · Ballroom BC  
[Session page](https://qconsf.com/presentation/nov2026/use-ai-multiply-your-team-staff-engineer)

> Pinterest's Jordan Cutler turned the corrections he kept giving AI agents into shared skills, a one-command path to a reviewed PR, and scheduled agents that run whole migrations.

## Key points

- From Q1 2025 to Q3 2026, Pinterest's top 10% went from 6.7 to 11.3 merged PRs per engineer per week, and the bottom half from 1.0 to 1.15.
- His three moves: multiply yourself, multiply your team, and multiply the system.
- He tried new internal agent tools first and steered his team away from the ones that fell short.
- A learn-from-session skill, run by a hook at the end of each session, turns his repeated corrections into skills that sync to Claude Code, Codex and Cursor.
- Telling the team to switch tools didn't work. Fixing the sandbox, four recorded shadow sessions and a one-line setup script did.
- Useful personal skills were promoted to repo-wide or company-wide skills that install themselves; the most-used were opening a PR, Slack updates and diagnosing CI.
- Autoship takes a ticket, Slack thread or a few sentences to a ready-for-review PR, with a skill at each step. 28 teams and 400+ merged PRs since July.
- A scheduled agent system ran a React class-to-function migration 3 to 5 times faster than by hand, in the background.
- One runaway job opened 16 PRs in two minutes and CI job start times went from under 30 seconds to 14 minutes. Rate limits fixed it.
- Against other web teams on the same AI tools, his team's merged PRs per engineer were 4 times higher in 2026, his own PRs excluded.

From the session audio and photos of the whole deck. Almost every figure is Pinterest’s internal data shown on a slide, so I could only check the arithmetic. One correction: the audio says a teammate’s agent found 130 PRs that could skip tests. The slide says 130 end-to-end runs avoided across 82 PRs in one week, and I’ve used the slide.

## The talk in brief

Pinterest’s own data shows the gap between its top 10% of engineers and the bottom half widening fast in 2026: the top tenth now merges about ten times as many PRs a week. Jordan Cutler’s answer to “what is a staff engineer for now” is to close that gap, not to out-ship it. His tools are three moves: multiply yourself, multiply your team, multiply the system.

Each move takes the same judgment one level further out. First he wrote his repeated corrections down as skills, using a hook that reviews each session. Then he got his team onto the same system, promoted the useful skills company-wide, and wrapped them in Autoship, one command from ticket to ready-for-review PR. Finally he built a scheduled agent system that runs whole migrations in the background. That one taught him about guardrails the hard way.

> “A 10x engineer isn’t ten times faster. They’re the reason ten other people are.” (Closing slide)

## In depth

The talk followed the three moves in order. Slide numbers are photo order in the gallery below.

### Why it matters: a 10x gap, and growing (slides 1–5)

A year ago his conference talk was about multiplying himself: one slide from it read “4 hours → 4 minutes”. This year’s question is what a 10x engineer looks like when everyone has AI. His chart of merged PRs per engineer per week shows the top tenth pulling away from the bottom half through 2026, using the same tools.

| Merged PRs per engineer per week | Q1 2025 | Q3 2026 | Change |
|----------------------------------|---------|---------|--------|
| Top 10%                          | 6.7     | 11.3    | +68%   |
| Bottom half                      | 1.0     | 1.15    | +14%   |
| Ratio, top to bottom             | 6.7×    | 9.8×    |        |

His framing: AI didn’t change what a staff engineer is for, which is making the people around them better. It changed where the leverage is. It used to be one code review at a time. Now it’s judgment built into the agents and tools the whole team uses every day.

![Line chart of merged PRs per engineer per week, Q1 2025 to Q3 2026. Top 10% rise from 6.7 to 11.3, plus 68%. Bottom half rise from 1.0 to 1.15, plus 14%. Labelled the opportunity, a 10x gap and growing. Internal Pinterest data.](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p5989.webp)

Slide 3. Everyone has AI. Not everyone uses it the same way.

![Slide: three moves. Multiply yourself: go first, and notice what others will run into too. Multiply your team: make your corrections the default, and let others add. Multiply the system: move up a level, and build for any case, not each one.](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p5991.webp)

Slide 5. The three moves.

The staff engineer’s job is raising the bottom half, not shipping more than the top tenth.

### Move 1: multiply yourself (slides 6–16)

Going first means trying new tools before the team does. A new agent harness, promoted internally, cancelled all running subagents if you steered it mid-task. A new remote agent runner needed too much back and forth for some jobs, where a lighter in-house hack worked better. He reported both and steered his team away. It also means seeing the gap between what you asked for and what you got. His repeat corrections: fix the root cause, not the symptom (“why is it null?”); stop using em dashes; add a Mermaid before-and-after diagram to PR descriptions; keep the PR small; and actually test it like a user before saying it’s done.

Every new session forgot all of it. A teammate showed him a personal skills folder, one skill for each thing they kept repeating, and he copied and extended it into a loop: work, spot a repeat, save it as a skill, and the next agent knows it. Three skills run the loop:

| Skill              | What it does                                                                                                                                                           |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| learn-from-session | Triggered by a hook at the end of a session. Reads the transcript, finds where he applied judgment, and decides what to change.                                        |
| create-skill       | Writes a new skill and runs evals on it.                                                                                                                               |
| ship-skill         | Improves an existing skill, updates global instructions or adds a deterministic hook, then links the skills into every harness he uses: Claude Code, Codex and Cursor. |

Out came 33 skills. Some are judgment: a staff design review (“is this the right problem?”), PR review ranked by correctness, security and risk, and which review comments are worth fixing. Some are workflow: a PR shepherd that takes a change from review to green CI, and one that strips AI writing tells. He calls them slices of himself. His point was that you only find them by staying close to the code.

![Diagram: learn-from-session finds what I keep repeating, then calls create-skill, which writes a new skill, or ship-skill, which improves one I already have, then refreshes my skills in every coding agent I use.](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6002.webp)

Slide 11. Three skills keep it learning.

![Six skill folders: staff-design-review, review-pr-as-ai, annotate-pr-as-ai, pr-shepherd-as-ai, address-pr-review, scrub-ai-slop. Caption: 6 of my 33 skills, each one something I'd repeated.](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6003.webp)

Slide 12. Judgment, written down.

Any correction you type twice is a candidate skill. But a folder only you have makes only you faster.

### Move 2: bringing the team along (slides 17–28)

Two new people joined his team, two more were new to the area, and the team had big goals for build and CI scaling while a surge of agent PRs was knocking CI over. Reviewing their PRs, he found himself giving the same corrections he used to give his own agents. Less experienced engineers had it hardest, because it’s harder to tell when an agent is fooling you. Two problems stood out: judgment wasn’t spreading, and people ran agents in Cursor, approving every command, instead of the team’s sandbox where agents can run free.

Telling people to switch didn’t work, so he asked why they avoided the sandbox and fixed each answer.

| Complaint                             | Fix                                                                                 |
|---------------------------------------|-------------------------------------------------------------------------------------|
| There’s no browser in the sandbox     | Browser access by default; browser tool start went from about 70 seconds to under 2 |
| MCP tools take forever to start       | MCP tools installed by default                                                      |
| pnpm install keeps failing            | Dependencies fixed                                                                  |
| The build tool is broken in the agent | Caching, so builds start fast                                                       |

That still wasn’t enough. What flipped it was four shadow sessions where four teammates watched him do real work. A junior engineer’s reaction was that they hadn’t realised the sandbox was one command to start, though it had been announced several times. He recorded the sessions and turned the transcripts into a reading guide and slides now used in onboarding. Then he made the whole learning system a one-line install, `./setup-fork.sh your-name`. A junior engineer used it to build their own skill that explains the lessons in each PR.

Next came the shared layer. Too many people were building personal skills that never got shared, so the team crowdsourced common workflows and corrections and promoted them to repo-wide or company-wide skills. Those install automatically into every harness an engineer uses. In the talk he put usage at over a thousand people and more than 20 skills. The slide shows which ones spread:

| Skill (2026)                                 | People who used it |
|----------------------------------------------|--------------------|
| Opening a PR (create-pr)                     | 861                |
| Writing a Slack update (write-slack-message) | 610                |
| Why did CI fail? (diagnose-ci)               | 550                |
| Explaining code (explain-code)               | 15                 |

A skill is guidance, and guidance is usually close. Where he could, he added a deterministic check: a lint rule, a CI check, or a script inside the skill the agent must run before moving on. He warned against overdoing it. Their PR description skill enforces the template but leaves room for the agent to go beyond it.

![Slide: what I had to fix. Engineer A: there's no browser in the sandbox. B: MCP tools take forever to start. C: pnpm install keeps failing. D: the build tool is broken in the agent. Fixes: browsers, MCP tools, dependencies, caching. Browser tool start about 70 seconds to under 2.](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6016.webp)

Slide 22. Fix the reasons people avoid the sandbox.

![Bar chart: about half our engineers used our skills this year. People who used each skill in 2026: opening a PR 861, writing a Slack update 610, why did CI fail 550, explaining code 15.](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6023.webp)

Slide 27. The boring ones spread furthest.

Adoption came from removing friction and showing real work, not from announcements.

### Move 2: Autoship, the default path (slides 29–35)

With good skills in place, people were still calling them one by one in the same order: plan, implement, review, address comments, babysit CI. Autoship does it in one command. You feed it a Jira ticket, a Slack thread, a customer report or a few sentences, and it runs research, plan, build, verify, open the PR, review and watch CI, splitting context windows across agents. Each step has a skill attached: is this the right problem, proof it runs, the evidence, correct, secure and tested, and fix what’s mechanical. Anyone on the team can add to a step, and the next PR for everyone gets it.

It launched in July. 28 teams have shipped with it and over 400 PRs have merged. He said most of those PRs get very little review feedback. His story: a teammate saw his review agent’s comments and asked what his prompt was. He pointed them to the review skill. On their next PR, it flagged a design problem before any human looked: a flag that sounded generic but did something specific. Fix the behaviour or rename it. The human review was then close to a stamp.

![Diagram: agents for research, plan, build, verify, open the PR, review and watch CI, with a skill at each step: right problem, proved where it runs, show the evidence, correct secure tested, fix what's mechanical. Anyone on the team can add to a step. A shared knowledge system for shipping.](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6030.webp)

Slide 30. Judgment at every step.

![Slide: teams shipping with Autoship. 28 teams shipped with it, 400+ merged PRs, launched in July. One command. The judgment is already in it.](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6031.webp)

Slide 31. One command, and the judgment is already in it.

Make the right way the easy way, and let the team add to it. But every slice still needs someone to press the button.

### Move 3: multiply the system (slides 36–50)

Before the 1950s, ports got better at loading cargo by hand, one sack at a time. Containerization changed the unit instead. His slide put hand loading at \$5.86 a ton and the box at 16 cents. AI makes it easy to load by hand faster, he said: twenty terminals and a lot of sloppy PRs. The staff move is asking whether you need a box.

His team’s cargo was migrations: one kind of change across hundreds of files and dozens of teams, such as React class components to function components. Before, a staff engineer wrote the plan and engineers prompted their way through it, team by team. Now one system runs any migration. The staff engineer points it at the job with an example, an engineer puts it on a schedule, and an agent in a sandbox splits it into PRs and posts to Slack for human review. A job is a few lines of YAML (name, cron schedule, working directory, prompt file, timeout, notify), registered with one command. Because it’s declarative, he could set up jobs for other teams too.

The class-component migration ran 3 to 5 times faster than by hand, in the background. iOS, Android and backend teams adopted the system. Then the sorcerer’s apprentice part. Early on someone asked what the scheduler would do to CI, and he said not to worry. A few weeks later one job opened 16 PRs in two minutes, and the wait for a CI job to start went from under 30 seconds to 14 minutes. They added rate limits and better docs and haven’t hit it since. His lesson: don’t wait for the perfect guardrail, ship a small one.

| By hand, faster            | Building the box                                                                                           |
|----------------------------|------------------------------------------------------------------------------------------------------------|
| Debug each incident faster | A first responder for any incident, already looking at recent changes, deploys, experiments and dashboards |
| Fix each bug ticket faster | A draft fix for any bug ticket; agents and people post bugs to a channel and another agent ships fixes     |
| Review each design doc     | A platform for any design doc that bakes in company principles                                             |
| Fix each flaky test faster | An agent that triages any flaky test and ships a prevention back into the system                           |

He taught a teammate the scheduler, and the teammate built the flaky-test agent, then a second one of their own. It spotted end-to-end test runs on PRs that couldn’t affect them. In its first week (Sep 29 to Oct 6, 2026) its report showed 82 PRs affected and 130 estimated end-to-end runs avoided. Forty engineers now have scheduler jobs of their own.

![Slide: what a job looks like. A jobs.yaml with name migration, schedule every two hours, working_dir, prompt_file prompts/migration.md, timeout 45m, notify self_dm true, registered with cron-claude register.](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6043.webp)

Slide 42. A whole job in a few lines.

![Slide: one loop, and everyone waited. 16 PRs in two minutes. How long a CI job waited to start: under 30 seconds before, 14 minutes after one loop, about 30 times longer.](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6047.webp)

Slide 45. The broom he couldn’t stop.

Pick work you do one case at a time and ask what it would take to handle any case. Put a limit on it before it runs.

### Results, and the part you can’t write down (slides 51–58)

He compared merged PRs a month for the same five teammates in 2025 and 2026. He said his own output tripled and his teammates’ went up five times. Against other web teams, his team was in line in 2025. In 2026 it was up four times per engineer, with his own PRs left out, while other teams also improved. Same AI tools, different results.

He closed on what a skill can’t fix. One teammate was struggling with expectations, and what helped was an honest one-on-one conversation. His three things for Monday: write down what you repeat, put it where people already work, and build for every case, not one.

![Bar chart: same AI tools, different results. Merged PRs per engineer per month for other web teams and my team, 2025 and 2026. My team is 4x in 2026. My own PRs are not counted. Internal Pinterest data.](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6057.webp)

Slide 52. Against other web teams.

![Slide: on Monday. Multiply yourself: write down what you repeat. Multiply your team: put it where they already work. Multiply the system: build for every case, not one.](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6059.webp)

Slide 54. What to do on Monday.

### From the Q&A

- **Shared skills versus personal taste.** He wrote a skill on writing skills that sets the standard for what goes central, adds checks in review, and keeps taste-specific rules in personal skills.
- **Feedback when the slice is wrong.** Next they plan to compare what agents comment on with what humans comment on, and track how often humans reject agent feedback.
- **Where to start.** Autoship, because it’s one path every engineer funnels through, so the team can agree its standards once.
- **Review fatigue.** Consistent PR descriptions, Autoship’s own review catching most comments first, and risk-based review that they are evaluating.
- **Spreading what works.** Rotate the shadow sessions, and a biweekly learning hour where people who ship the most explain how.
- **Making the case to leadership.** His leadership cares whether goals are hit. Show the gap in data, then argue that a couple of days of training can turn a two-month plan into three weeks.

## Numbers we checked

Checked on Nov 17, 2026. Pinterest’s internal figures can’t be checked from outside; where the arithmetic could be, I reran it.

| Claim                                           | Figure                                                                    | Source                                                                                                                                                                                                         | Status                                       |
|-------------------------------------------------|---------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------|
| Top 10% merged PRs per engineer per week        | 6.7 → 11.3, +68%                                                          | Slide 3; 11.3 ÷ 6.7 = 1.69                                                                                                                                                                                     | Slide only arithmetic checked                |
| Bottom half, same measure                       | 1.0 → 1.15, +14%                                                          | Slide 3; the rounded values give +15%                                                                                                                                                                          | Caveat rounding                              |
| Top 10% ship about 10× the bottom half          | 11.3 ÷ 1.15 = 9.8×                                                        | Arithmetic rerun on slide 3                                                                                                                                                                                    | Checked                                      |
| Cost to load cargo, by hand vs container (1956) | Slide: \$5.86 vs 16¢ a ton                                                | [The Geography of Transport Systems](https://transportgeography.org/contents/chapter1/the-setting-of-global-transportation-systems/idealx-first-containeriship-1956/): McLean’s figure was \$5.83 vs under 16¢ | Caveat source says \$5.83; loading cost only |
| Browser tool start in the sandbox               | About 70 s → under 2 s                                                    | Slide 22                                                                                                                                                                                                       | Slide only                                   |
| People using the shared skills                  | About half of engineers; create-pr 861, Slack update 610, diagnose-ci 550 | Slide 27                                                                                                                                                                                                       | Slide only                                   |
| Shared skill users and count                    | Over 1,000 people, 20+ skills                                             | Spoken in the talk                                                                                                                                                                                             | Talk only                                    |
| Autoship adoption                               | 28 teams, 400+ merged PRs, launched July                                  | Slide 31; 28 teams also in the session abstract                                                                                                                                                                | Slide only                                   |
| Class-component migration speed                 | 3 to 5× faster than by hand                                               | Slide 43                                                                                                                                                                                                       | Slide only                                   |
| Runaway scheduled job                           | 16 PRs in 2 minutes; CI start under 30 s → 14 min, about 30×              | Slide 45; 14 min ÷ 30 s = 28                                                                                                                                                                                   | Slide only arithmetic checked                |
| End-to-end runs skipped in one week             | 130 runs, 82 PRs                                                          | Slide 48 (bot report); the audio said 130 PRs                                                                                                                                                                  | Slide only                                   |
| Engineers with their own scheduler jobs         | 40                                                                        | Slide 50                                                                                                                                                                                                       | Slide only                                   |
| His output vs his teammates’, 2025 to 2026      | 3× vs 5×, same five teammates                                             | Spoken; the chart on slide 51 has no values                                                                                                                                                                    | Talk only                                    |
| His team vs other web teams, 2026               | 4× per engineer per month, his PRs excluded                               | Slide 52                                                                                                                                                                                                       | Slide only                                   |
| Newsletter readership                           | 100,000 subscribers                                                       | [QCon speaker page](https://qconsf.com/speakers/jordancutler)                                                                                                                                                  | Checked as stated there                      |

## About the speaker

Jordan Cutler is a Senior Staff Engineer and Web Tech Lead at Pinterest, where he leads platform work across web infrastructure, developer experience, performance and reliability. Before Pinterest he worked at Qualified, Gusto and Twitter. He writes the High Growth Engineer newsletter on engineering careers, which the QCon page puts at 100,000 subscribers. His 2025 talk at infoShare, “Using AI to 10x Your Productivity as an Engineer”, was the multiply-yourself version of this one.

## Terms and technologies

### Skills and instructions

[Agent Skills (SKILL.md)](https://agentskills.io/specification)  
An open format, started by Anthropic: a folder with a SKILL.md file of instructions an agent loads only when the task calls for it. Every “slice” in this talk is one.

[Hooks](https://code.claude.com/docs/en/hooks)  
Commands Claude Code runs at fixed points in a session. A SessionEnd hook is how his learn-from-session skill reviews each transcript.

[Lint and deterministic checks](https://en.wikipedia.org/wiki/Lint_(software))  
Automated rules that pass or fail the same way every time. He adds them where a skill’s guidance alone isn’t followed reliably.

### Agents and where they run

[Claude Code](https://code.claude.com/docs)  
Anthropic’s coding agent for the terminal and IDE. One of the three harnesses his skills sync into.

[Codex](https://developers.openai.com/codex)  
OpenAI’s coding agent. Also reads the same skills.

[Cursor](https://cursor.com)  
An AI code editor. In Pinterest’s setup it asked engineers to approve each command, which is why he wanted people in the sandbox.

Agent harness  
The program around a model that runs the loop, tools and subagents. He tried a new internal one and found it cancelled subagents when steered.

[Agent sandbox](https://docs.docker.com/ai/sandboxes/)  
An isolated environment where an agent can run commands without approval. Pinterest’s is its own container-based setup; Docker Sandboxes is one public product of this kind.

[Model Context Protocol (MCP)](https://modelcontextprotocol.io)  
A standard way to connect agents to tools and data. Slow-starting MCP tools were one reason people avoided the sandbox.

[pnpm](https://pnpm.io)  
A JavaScript package manager. Failing installs in the sandbox were another complaint he fixed.

### Shipping and review

Autoship  
Pinterest’s internal one-command skill that takes a task to a ready-for-review PR, with a review skill at each step. Not public.

[Mermaid](https://mermaid.js.org)  
Text-defined diagrams that render in Markdown. He wanted a before-and-after diagram in every PR description.

[Jira](https://www.atlassian.com/software/jira)  
Atlassian’s issue tracker. One of the inputs Autoship accepts.

[Flaky test](https://martinfowler.com/articles/nonDeterminism.html)  
A test that passes or fails without any code change. One of his “any \_\_\_” examples.

### Systems

[Containerization](https://en.wikipedia.org/wiki/Containerization)  
Shipping cargo in standard boxes that cranes, ships and trucks all handle the same way. His analogy for changing the unit of work instead of speeding up each case.

[cron](https://en.wikipedia.org/wiki/Cron)  
The Unix job scheduler and its schedule syntax. Pinterest’s internal cron-claude tool registers scheduled agent jobs.

[React class components](https://react.dev/reference/react/Component)  
The older way to write React components. React recommends function components, and its docs show how to migrate. This was the first migration the scheduler ran.

[The Sorcerer’s Apprentice](https://en.wikipedia.org/wiki/The_Sorcerer%27s_Apprentice)  
Goethe’s poem about an apprentice who enchants a broom to carry water and can’t stop it. His label for the job that flooded CI.

[Rate limiting](https://en.wikipedia.org/wiki/Rate_limiting)  
Capping how often something can run. The small guardrail they added after the flood.

## Reading and tools

- Jordan Cutler, [How to Grow From Senior to Staff Engineer in the AI Era](https://newsletter.eng-leadership.com/p/how-to-grow-from-senior-to-staff) (Engineering Leadership newsletter, June 2026).
- Jordan Cutler, [High Growth Engineer](http://read.highgrowthengineer.com/) newsletter.
- [Agent Skills specification](https://agentskills.io/specification) and the Claude Code [hooks reference](https://code.claude.com/docs/en/hooks), for building a learn-from-session loop.
- Docker, [Docker Sandboxes docs](https://docs.docker.com/ai/sandboxes/), for the sandbox side.
- Marc Levinson, [The Box](https://en.wikipedia.org/wiki/The_Box_(Levinson_book)) (Princeton, 2006), the history behind the container analogy.

### Related sessions

- [Skills, Memory, or Fine-Tuning?](skills-memory-or-fine-tuning.md) (Lucidic, this morning). SkillsBench found AI-written skills made agents slightly worse. Jordan’s loop is built from a person’s corrections, which may be the difference.
- [Running a Software Factory Efficiently at Uber Scale](running-software-factory-efficiently-at-uber-scale.md) (Monday). Scheduled migration agents at a much larger scale.
- [Generation Got Cheap, Trust Didn’t](generation-got-cheap-trust-didnt.md) (Roblox, Monday). Mining review history for review rules, the same idea as comparing agent and human comments.

## All slides

[![Slide: Title](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p5986.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p5986.webp)

Slide 1. Title

[![Slide: What does a 10x engineer look like when everyone has AI?](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p5987.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p5987.webp)

Slide 2. What does a 10x engineer look like when everyone has AI?

[![Slide: Everyone has AI. Not everyone uses it the same.](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p5989.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p5989.webp)

Slide 3. Everyone has AI. Not everyone uses it the same.

[![Slide: AI didn’t change what a staff engineer is for](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p5990.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p5990.webp)

Slide 4. AI didn’t change what a staff engineer is for

[![Slide: Three moves](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p5991.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p5991.webp)

Slide 5. Three moves

[![Slide: Some of what I tried was a dead end](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p5994.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p5994.webp)

Slide 6. Some of what I tried was a dead end

[![Slide: Going first, I ran a lot of agents](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p5995.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p5995.webp)

Slide 7. Going first, I ran a lot of agents

[![Slide: I kept repeating myself](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p5997.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p5997.webp)

Slide 8. I kept repeating myself

[![Slide: A teammate’s folder](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p5998.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p5998.webp)

Slide 9. A teammate’s folder

[![Slide: A system that learns from every session](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6001.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6001.webp)

Slide 10. A system that learns from every session

[![Slide: Three skills keep it learning](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6002.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6002.webp)

Slide 11. Three skills keep it learning

[![Slide: Judgment, written down](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6003.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6003.webp)

Slide 12. Judgment, written down

[![Slide: Slices of me](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6004.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6004.webp)

Slide 13. Slices of me

[![Slide: You find these by staying close to the code](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6005.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6005.webp)

Slide 14. You find these by staying close to the code

[![Slide: My folder made me faster. But only I had it](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6006.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6006.webp)

Slide 15. My folder made me faster. But only I had it

[![Slide: New people, a new area, and no time to ramp](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6007.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6007.webp)

Slide 16. New people, a new area, and no time to ramp

[![Slide: Now I was repeating myself in code review](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6008.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6008.webp)

Slide 17. Now I was repeating myself in code review

[![Slide: The math](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6010.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6010.webp)

Slide 18. The math

[![Slide: Move 2: multiply your team](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6011.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6011.webp)

Slide 19. Move 2: multiply your team

[![Slide: Meet people where they are](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6012.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6012.webp)

Slide 20. Meet people where they are

[![Slide: Two problems to solve](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6014.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6014.webp)

Slide 21. Two problems to solve

[![Slide: What I had to fix](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6016.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6016.webp)

Slide 22. What I had to fix

[![Slide: Teaching gets it used](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6018.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6018.webp)

Slide 23. Teaching gets it used

[![Slide: One line to get your own](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6020.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6020.webp)

Slide 24. One line to get your own

[![Slide: We made it a plan](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6021.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6021.webp)

Slide 25. We made it a plan

[![Slide: Make your judgment the default](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6022.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6022.webp)

Slide 26. Make your judgment the default

[![Slide: The boring ones spread furthest](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6023.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6023.webp)

Slide 27. The boring ones spread furthest

[![Slide: Write it down. Then make it a check.](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6025.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6025.webp)

Slide 28. Write it down. Then make it a check.

[![Slide: One command, task to ready-for-review PR](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6027.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6027.webp)

Slide 29. One command, task to ready-for-review PR

[![Slide: Judgment at every step](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6030.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6030.webp)

Slide 30. Judgment at every step

[![Slide: Teams shipping with Autoship](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6031.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6031.webp)

Slide 31. Teams shipping with Autoship

[![Slide: “What’s your prompt for the review?”](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6032.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6032.webp)

Slide 32. “What’s your prompt for the review?”

[![Slide: My review, before anyone else’s](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6033.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6033.webp)

Slide 33. My review, before anyone else’s

[![Slide: The question I’d have asked](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6034.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6034.webp)

Slide 34. The question I’d have asked

[![Slide: A slice still needs someone to press the button](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6035.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6035.webp)

Slide 35. A slice still needs someone to press the button

[![Slide: Move 3: multiply the system](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6036.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6036.webp)

Slide 36. Move 3: multiply the system

[![Slide: Move up a level](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6037.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6037.webp)

Slide 37. Move up a level

[![Slide: Shipping, before the 1950s](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6039.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6039.webp)

Slide 38. Shipping, before the 1950s

[![Slide: Migrations were our cargo](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6040.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6040.webp)

Slide 39. Migrations were our cargo

[![Slide: From each migration to any migration](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6041.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6041.webp)

Slide 40. From each migration to any migration

[![Slide: What runs it](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6042.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6042.webp)

Slide 41. What runs it

[![Slide: What a job looks like](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6043.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6043.webp)

Slide 42. What a job looks like

[![Slide: One job, 3 to 5 times faster than by hand](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6044.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6044.webp)

Slide 43. One job, 3 to 5 times faster than by hand

[![Slide: I made a broom I couldn’t stop](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6045.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6045.webp)

Slide 44. I made a broom I couldn’t stop

[![Slide: One loop, and everyone waited](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6047.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6047.webp)

Slide 45. One loop, and everyone waited

[![Slide: Don’t wait for the perfect guardrail](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6048.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6048.webp)

Slide 46. Don’t wait for the perfect guardrail

[![Slide: Find your any \_\_\_](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6051.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6051.webp)

Slide 47. Find your any \_\_\_

[![Slide: Test runs it skipped](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6052.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6052.webp)

Slide 48. Test runs it skipped

[![Slide: The question](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6053.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6053.webp)

Slide 49. The question

[![Slide: The math, finished](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6054.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6054.webp)

Slide 50. The math, finished

[![Slide: What my team shipped, next to me](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6056.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6056.webp)

Slide 51. What my team shipped, next to me

[![Slide: Same AI tools. Different results.](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6057.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6057.webp)

Slide 52. Same AI tools. Different results.

[![Slide: AI didn’t change what a staff engineer is for (reprise)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6058.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6058.webp)

Slide 53. AI didn’t change what a staff engineer is for (reprise)

[![Slide: On Monday](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6059.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6059.webp)

Slide 54. On Monday

[![Slide: The parts you can’t write down stay yours](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6060.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6060.webp)

Slide 55. The parts you can’t write down stay yours

[![Slide: A 10x engineer isn’t ten times faster](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6062.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6062.webp)

Slide 56. A 10x engineer isn’t ten times faster

[![Slide: Thank you](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6063.webp)](../slides/use-ai-to-multiply-your-team-as-a-staff-engineer/deep/p6063.webp)

Slide 57. Thank you
