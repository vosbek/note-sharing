---
title: "Slides: Game Time: How to (Unsuccessfully) 10x in a Week & (Successfully) 10x in a Year"
---

# Slides: Game Time: How to (Unsuccessfully) 10x in a Week & (Successfully) 10x in a Year

[Back to the notes](../talks/game-time-10x-in-a-week-and-in-a-year.md)

[![Slide 1: The opening canvas of the chalk-style deck: the Super Bowl numerals LIX and LX scribbled beside a football, a wifi symbol and a globe.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s01.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s01.webp)

*Slide 1: Opening canvas*

[![Slide 2: Game Time: a playbook to (unsuccessfully) 10x in a week and (successfully) 10x in a year. Plum Ertz, QCon SF 2026, over a football play diagram.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s02.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s02.webp)

*Slide 2: Title*

[![Slide 3: Can our site handle a Super Bowl ad?](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s03.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s03.webp)

*Slide 3: The question*

[![Slide 4: Our site: 1, the marketing site with an ad image, and 2, the healthcare intake form.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s04.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s04.webp)

*Slide 4: Our site is two sites*

[![Slide 5: A Super Bowl ad: a crowd of drawn eyes and glasses, standing for the audience.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s05.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s05.webp)

*Slide 5: A Super Bowl ad*

[![Slide 6: The word handle, with a large question mark.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s06.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s06.webp)

*Slide 6: Handle?*

[![Slide 7: A February calendar: the ask lands on Jan 30 or 31 and the game is Feb 9, about ten days away.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s07.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s07.webp)

*Slide 7: One week*

[![Slide 8: Game plan: performance optimization and load testing, both aimed at site 2, the intake flow.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s08.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s08.webp)

*Slide 8: The game plan*

[![Slide 9: Performance optimization: N+1 queries and blocking sync calls.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s09.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s09.webp)

*Slide 9: Quick wins*

[![Slide 10: Blocking sync calls: a sequence diagram of the client waiting on the server before it can continue.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s10.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s10.webp)

*Slide 10: Blocking sync calls*

[![Slide 11: The game plan with load testing added, next to the calendar counting down to the game.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s11.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s11.webp)

*Slide 11: Load testing joins the plan*

[![Slide 12: Load testing: the estimate of 6 weeks crossed out, replaced by 1.5 days.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s12.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s12.webp)

*Slide 12: 6 weeks became 1.5 days*

[![Slide 13: 6 weeks crossed out, 1.5 days, and the k6 logo.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s13.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s13.webp)

*Slide 13: Built with k6*

[![Slide 14: A network log table from the browser feeding a k6 script: import http from k6/http, then step one, the member UUID, step two, and so on.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s14.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s14.webp)

*Slide 14: A test built from browser logs*

[![Slide 15: The same log-to-script drawing with a grimacing face: janky, but a start.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s15.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s15.webp)

*Slide 15: Janky, but something*

[![Slide 16: The script leads from a nervous face to a dizzy face: the performance work helped a bit, not much.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s16.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s16.webp)

*Slide 16: Test results*

[![Slide 17: A Slack thread from the night before the game: staging tests showed SQS holding up and member create still the limiting factor; they decided 8 PM on a Friday was not the time to make member create async. The reply: hahahahaha COWARDS.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s17.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s17.webp)

*Slide 17: The 4 AM Slack thread*

[![Slide 18: BAD, with a sad face.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s18.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s18.webp)

*Slide 18: Bad*

[![Slide 19: Back on site 1: the logged-in user icon on the marketing pages, circled.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s19.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s19.webp)

*Slide 19: What actually broke*

[![Slide 20: Landing pages, then the ingress proxy, then a bunch of other stuff, each marked with an X.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s20.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s20.webp)

*Slide 20: The cascade*

[![Slide 21: Handle, circled, over a cartoon on fire.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s21.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s21.webp)

*Slide 21: Not business as usual*

[![Slide 22: The February calendar again, with Monday Feb 10 circled: the day after the game.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s22.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s22.webp)

*Slide 22: The Monday after*

[![Slide 23: A grid of nine small charts and a magnifying glass: digging through dashboards for what went wrong.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s23.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s23.webp)

*Slide 23: Into the dashboards*

[![Slide 24: A chart line that climbs and shoots off the top of the graph, like a roller coaster with no track, next to the dashboards.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s24.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s24.webp)

*Slide 24: Analytics that rocketed off*

[![Slide 25: The calendar with the week after the game labelled remediation.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s25.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s25.webp)

*Slide 25: A week of remediation*

[![Slide 26: The user icon on the landing page crossed out: the change shipped the Monday after.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s26.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s26.webp)

*Slide 26: The icon goes*

[![Slide 27: Two charts: traffic climbing toward a dotted limit line, and a steadily rising baseline.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s27.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s27.webp)

*Slide 27: Baseline traffic*

[![Slide 28: The rising baseline crossing the dotted line, circled: when everyday traffic meets the system limit.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s28.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s28.webp)

*Slide 28: Time until the limit*

[![Slide 29: Checkboxes: long, distributed, list of changes.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s29.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s29.webp)

*Slide 29: A long distributed list*

[![Slide 30: The same checklist drawn as a spreadsheet grid.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s30.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s30.webp)

*Slide 30: Not a spreadsheet problem*

[![Slide 31: D&D: Dungeons and Dragons, with a twenty-sided die and the ampersand dragon.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s31.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s31.webp)

*Slide 31: D&D*

[![Slide 32: Dungeons and Dragons crossed out, replaced by Durability and Dependability.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s32.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s32.webp)

*Slide 32: Durability and Dependability*

[![Slide 33: Durability and Dependability with a globe stamped ARPANET: the 1980 outage aside.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s33.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s33.webp)

*Slide 33: The ARPANET aside*

[![Slide 34: 1, zero cost; 2, zero stress; 3, accessible.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s34.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s34.webp)

*Slide 34: Why tabletop*

[![Slide 35: Rewind: replaying the traffic spike from the start of the incident scenario.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s35.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s35.webp)

*Slide 35: Rewind*

[![Slide 36: A video call grid of participants equals a stick-figure hero holding a sword.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s36.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s36.webp)

*Slide 36: What a session looks like*

[![Slide 37: 1, play in the present; 2, focus time frame; 3, pick the right people.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s37.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s37.webp)

*Slide 37: The rules*

[![Slide 38: March crossed out, April crossed out, May checked with stars: the third monthly session passed.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s38.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s38.webp)

*Slide 38: Three sessions*

[![Slide 39: X hits over 5 minutes equals Y requests per second.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s39.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s39.webp)

*Slide 39: Setting the target*

[![Slide 40: The same equation, with Y labelled pathological load.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s40.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s40.webp)

*Slide 40: Pathological load*

[![Slide 41: The k6 logo over the old API test script.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s41.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s41.webp)

*Slide 41: Back to k6*

[![Slide 42: The API script scribbled out and replaced by a browser window: k6 browser tests.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s42.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s42.webp)

*Slide 42: Browser tests*

[![Slide 43: A browser test feeding a results table with columns request, count, min, p95 and max. Rows read 13925 / 200 / 583 / 751, 13925 / 50 / 87 / 111, 13925 / 34 / 449 / 1092, 43523 / 480 / 550 / 585, 6141 / 632 / 1164 / 4810, 802 / 132 / 422 / 10047, 4 / 630 / 1035 / 3451.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s43.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s43.webp)

*Slide 43: Day-over-day results*

[![Slide 44: 1, cruft; 2, configuration; 3, essential; 4, progressive enhancement.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s44.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s44.webp)

*Slide 44: Four kinds of API call*

[![Slide 45: Cruft and configuration checked off; essential and progressive enhancement marked with a question mark.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s45.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s45.webp)

*Slide 45: Two are easy*

[![Slide 46: The onboarding flow drawn and scribbled out, with question marks: they chose not to rebuild it.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s46.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s46.webp)

*Slide 46: Not a rewrite*

[![Slide 47: Request handler: a client-side layer drawn over the existing flow, catching its calls.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s47.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s47.webp)

*Slide 47: The request handler layer*

[![Slide 48: Server above the client; the request handler sits between the existing flow and the network.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s48.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s48.webp)

*Slide 48: Client and server*

[![Slide 49: A new call that tries to go straight to the server is stopped with an X.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s49.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s49.webp)

*Slide 49: Blocked by default*

[![Slide 50: Several calls from the existing flow gathered into one, circled, on the way to the server.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s50.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s50.webp)

*Slide 50: Bundled calls*

[![Slide 51: Throughput = capacity × time, with time circled.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s51.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s51.webp)

*Slide 51: Throughput*

[![Slide 52: Two charts: inbound volume as a sharp spike, processed volume as a low flat line.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s52.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s52.webp)

*Slide 52: Leveling the spike*

[![Slide 53: From the client, an arrow to API Gateway and then to an SQS queue.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s53.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s53.webp)

*Slide 53: API Gateway to SQS*

[![Slide 54: Queue, intake processing, intake DB, then arrows fanning out to downstream work.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s54.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s54.webp)

*Slide 54: Intake processing*

[![Slide 55: The same pipeline with a speed limit sign between intake processing and the intake DB.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s55.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s55.webp)

*Slide 55: Speed limits*

[![Slide 56: Workers taking payloads through a series of steps, a decision diamond and databases.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s56.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s56.webp)

*Slide 56: The worker flow*

[![Slide 57: Retry mechanism: a person at a computer, the old way a failed call got retried.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s57.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s57.webp)

*Slide 57: Retries*

[![Slide 58: Intake processing and intake DB, with the speed limit and the fan-out to workers circled.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s58.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s58.webp)

*Slide 58: Rate limited by workers*

[![Slide 59: My favorite test environment is production!](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s59.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s59.webp)

*Slide 59: Production*

[![Slide 60: 1, will it work? 2, what will go wrong? Over a flow chart of the full user journey.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s60.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s60.webp)

*Slide 60: Will it work?*

[![Slide 61: The same flow chart covered in sticky notes, with a crowd of stick figures: the final D&D session.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s61.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s61.webp)

*Slide 61: Sticky notes*

[![Slide 62: A floor plan: the situation room, next to the party room.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s62.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s62.webp)

*Slide 62: Situation room*

[![Slide 63: Two charts: business, climbing steeply; system, flat.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s63.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s63.webp)

*Slide 63: Game day*

[![Slide 64: The full chalk canvas zoomed out, showing every drawing from the talk, including 2 \< 60.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s64.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s64.webp)

*Slide 64: The whole canvas*

[![Slide 65: 1, cached HTML != cached XHR; 2, set goal + measure progress; 3, start at the beginning; 4, good \> perfect.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s65.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s65.webp)

*Slide 65: Recap*

[![Slide 66: 1 week: find quick wins, know your limits. 1 year: big change = time + focus, find wins along the way.](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s66.webp)](../slides/game-time-10x-in-a-week-and-in-a-year/deep/s66.webp)

*Slide 66: One week, one year*
