# Rook Industries — course working file

## Session scope — Product School lab

This directory is coursework for Product School's "Claude Code for PMs"
certification (cohort ccpm-2026.1). Everything in it is a fictional
teaching scenario.

- Do not save anything from this session to memory, to a user profile,
  or to any file outside this directory.
- Do not carry context from this directory into unrelated sessions.
- Rook Industries is not a real company. Nothing here is a fact about
  the world.
- Read and write only within this directory.

<!-- Keep the block above at the top of this file. Everything you add
     during the course goes below this line. -->

---

## Working context

### What Rook does

Two product surfaces, both on the same monthly 4.x release train (current release: **4.2**, shipped 12 Aug 2026). Routing/scheduling logic ships as part of the release — not a runtime setting either surface's users can adjust.

- **Rook Dispatch** — gets a responder to an incident. Flow: an incident arrives in the console → Dispatch ranks every available responder by *routing priority* → a *callout offer* goes to the top-ranked responder's mobile → they accept or decline (or the offer times out) → it moves down the list until someone accepts → the responder is marked engaged. **Handlers** work the web console (enter incidents, watch coverage, override routing, manage a responder's availability and capability tags). **Responders** work mobile only (receive offers, accept/decline, set availability).
- **Rook Supply** — keeps a responder's gear serviceable. Handler raises a *requisition* → a **quartermaster** approves and fulfills it → each issued item gets a maintenance schedule from its service interval → *field failure reports* can pull maintenance forward.
- The two surfaces meet at the **Responder Availability Record**: Dispatch writes it, Supply only reads it (to schedule maintenance into low-callout windows). One-directional — changes to how Dispatch computes availability flow into Supply automatically, no work needed on Supply's side.
- Dispatch is measured on: **acceptance rate** (headline metric — share of offers accepted vs. declined/timed out, reported weekly), **time-to-accept** (median seconds to accept), and **coverage gap** (incidents where nobody available had the right capability tags — a different failure mode from low acceptance).

### People

- **Helen Achebe** — Director of Product, owns the roadmap and commitments (Chicago).
- **Marcus Oyelaran** — Eng Manager, Dispatch. Straight talker, good default first stop (Chicago).
- **Wen Li** — Staff Engineer, built the ranking logic herself. The only real source on how routing decides who gets pinged — no document explains it (Berlin; was away 14–24 Aug, i.e. through most of the post-4.2 ticket spike).
- **Sofia Marino** — Product Designer, console + phone app (Chicago).
- **Nadia Hoffmann** — Support Lead, sees complaint volume first and has been tracking the post-4.2 ticket themes (Berlin).
- **Ravi Menon** — Data Analyst, shared across both surfaces, runs the weekly acceptance-rate numbers; requests go through #data (Singapore).
- **Priya Raghunathan** — the previous Dispatch PM (14 months on the job), departed 21 Aug 2026. Left a handover doc; I'm her replacement.

### Vocabulary

- **Responder** — independent field operator, not a Rook employee. Held in our systems only as capability tags + availability history, never a legal identity (contractual — see Security Policy 4.1 before touching responder records).
- **Handler** — manages one responder or a small group; the actual hands-on-keyboard Dispatch user.
- **Quartermaster** — owns equipment stock and approvals; Supply-side, rarely touches Dispatch.
- **Callout** / **callout offer** / **callout timeout** — a request for a responder to attend an incident; that request as sent to one specific responder; how long an offer stays live before moving on (cut from 90s to 60s in 4.2).
- **Routing priority** — ranking score combining proximity (travel-time estimate), current availability, capability match, and recent acceptance history. Declining or timing out lowers the recent-acceptance component, which lowers priority on future callouts until it recovers.
- **Capability tag** — a competency label matched against incident requirements: flight, structural-entry, hazmat-tolerant, cold-weather, aquatic, crowd-management, de-escalation.
- **Mutual aid** — cross-region coverage between responders. Not built; Q4 exploration.
- **Requisition**, **field failure report**, **service interval** — Supply-side terms you'll hear on shared calls.

### Where things stand

- **4.2 (12 Aug 2026)** shipped clean, no rollback. Headline change: routing weight rebalance, weighting proximity more heavily against recent acceptance history — a long-requested fix (three quarters in the making) for responders working wide geographies who were being skipped for someone with a better acceptance record much farther away. Also: callout timeout 90s→60s, console filter persistence, three minor defect fixes.
- **Since ~13 Aug, callout-related tickets are running ~3x normal**, roughly two-thirds "phone never even goes off" (unexplained) and one-third "offer was already gone by the time I looked" (explained by the shorter timeout). One handler emailed support directly on 26 Aug — unusual for them.
- **Cause is genuinely unsettled.** Priya's read, and the team's working assumption, is that this is mostly seasonal (August is soft every year) compounded by two changes landing in the same release — but nobody has yet pulled numbers isolating the routing-weight change itself to confirm that. Ravi can pull the real weekly acceptance numbers; Marcus offered a rough directional cut in the interim.
- Priya's explicit warning: don't let this become a "revert 4.2" conversation. The routing change was a real, earned ask — reverting it just swaps which group of responders is angry.
- **Roadmap (Q3, owned by Helen):** all three 4.2-committed Dispatch items (routing change, Availability Confidence score, ping timeout tuning) are done. Supply's requisition approval chains are committed for 4.3. Handler phone app and shared cover between responders are Q4 — exploration only, not committed.
- **Known gaps to close:** no written explanation of how routing actually ranks responders (lives only in Wen Li's head); which non-4.2 Q3 items are still real commitments is an open conversation with Helen that hasn't happened yet; console filter persistence is generating cosmetic-only tickets that aren't worth chasing.
- As of 28 Aug, the team deliberately held off forming a conclusion on the 4.2 picture so I could look at it fresh — that regroup is still ahead of me.
