# 02 · Super Hearing — prompts

**Context:** You joined Rook two weeks ago as PM on Dispatch.
Release 4.2 shipped on 12 August, just before you arrived, and
landed badly. Last session you built a context file and met the
company.

You still do not know what actually went wrong.

At the end of the session, ask Claude Code to save the prompts you
wrote yourself below — not the starter prompt. The closing slide has
the exact prompt to paste. By Module 6 this file is a prompt library
built from your own questions.

---

### 1.

For the three handlers who described a callout disappearing before their responder could respond (Ambrose, Dot, Halloran), pull callout-history.csv for those specific responders in the weeks they described — does the data show an unusually fast-closing offer window, or is memory outrunning what actually happened?

### 2.

Separate the two things that shipped together in 4.2: for those same responders, did the acceptance-history component of routing priority actually drop before the incident they're describing — meaning they were already ranked lower before the offer went out — or does the timing only line up with the 90s→60s timeout cut? Those point to different fixes.

### 3.

Did anyone say something nobody else mentioned — Kip's quiet-week/busy-week split, Halloran's requisition queue — and does that lone detail show up anywhere else in the tickets or the data, or is it a genuine one-off that shouldn't be allowed to shape what I post?

### 4.

List every filer across the 25 tickets and how many tickets each is behind — and do any of the four interview subjects (Ambrose/Vantage, Dot/Vesper, Halloran/Bulwark, Kip/Mite & Gale) appear anywhere in that list, or are the interviews and the tickets two completely disjoint sets of people?

### 5.

The interviews were 3-of-4 about a fast-vanishing offer, but the tickets are two-thirds about total silence — is that a real difference in what's happening across the responder population, or does it just mean Sofia's four interview picks happened to be people with a dramatic near-miss story to tell, while "nothing happened for two weeks" is a less tellable but far more common complaint that only shows up once you count tickets?

### 6.

For the five responders who filed twice — a quiet-stretch ticket, then weeks later a lost-the-one-offer-that-came ticket, same account both times — does routing.py's acceptance-history component mean going quiet for a while actively lowers your rank further, which would explain why the first offer to arrive after a drought is also the one most likely to vanish fast?

### 7.

Were Ambrose, Dot, Halloran, and Kip picked at random for this research, or by convenience/willingness — and does their selection line up with the split in callout-history.csv, where three of their four responders (Vantage, Bulwark, and Gale) are on the rising side and only Vesper and Meteor Mite are on the collapsing side? If the sample is skewed toward "winning" responders, the interviews wouldn't be wrong, just incomplete.

### 8.

Look at each ticket-filing responder's own callout-history trajectory across the ten weeks — do the "total silence" complaints and the "offer vanished" complaints actually belong to the same responders at different points in the same slide (quiet for weeks, then losing the one offer that finally arrives), meaning tickets and interviews are describing two ends of one mechanism rather than two different problems?

### 9.

Sofia's interview script opens on layout and console habits and only reaches "has anything felt too quiet" as a follow-up question — while a ticket requires someone to be bothered enough to proactively write one. Does that difference in how each pile gets generated (prompted conversation vs. self-initiated complaint) fully explain why silence dominates the tickets but had to be drawn out in the interviews, without needing to assume either group is wrong about what's happening to them?
