# Breaking the Quiet-Responder Loop

**To:** Helen Achebe
**From:** Dispatch PM
**Re:** Post-4.2 routing follow-up
**Status:** Draft — not build-ready (see Open Questions)

A clickable version of this brief: https://claude.ai/artifact/3cXTMBghoqQdDx6JY2tTgC

---

## The problem, in one line

4.2's routing rebalance made recent-acceptance history matter less overall
(weight 0.40 → 0.25) — but the scoring underneath it is asymmetric and never
decays: a non-accept costs 0.12, an accept only earns back 0.08, and a
timeout counts exactly like an explicit decline (`history.record_declined()`
either way). A responder who goes quiet has no way back in, because the only
way to earn points is to be offered work, and you don't get offered work
until your score has already recovered. Wen flagged this exact gap in a 2019
TODO in `history.py` and it was never resolved.

Meteor Mite is a live instance of the closed loop: zero accepted callouts for
the last three weeks of August, and nothing in the console or on the phone
says why.

## Who this is for

- **Kip**, the handler managing Meteor Mite. Currently has no way to tell
  "quiet because unavailable" from "quiet because routing stopped offering
  them anything" — both look identical on the roster today.
- **Meteor Mite**, the responder. Marked available the whole time, received
  zero callout offers for three straight weeks, no signal that anything
  changed, no path back in without someone stumbling on it from the outside
  (which is exactly how we found this — Sofia's unrelated design-research
  interview with Kip, not a ticket).

## What changes for them

**For Kip** — the console roster flags any available, capability-matched
responder who's gone a defined stretch without an offer, visible on the row
itself, not buried in a report. From there Kip can act: override routing and
send the next matching callout directly, the way overrides already work
today.

**For Meteor Mite** — recent-acceptance score recovers on a timer, not only
on accepted offers, so going quiet stops being permanent. Paired with a
floor: no available, matched responder goes indefinitely without at least
one offer. The loop gets a built-in exit instead of relying on someone
noticing.

## What this deliberately doesn't do

- **Not a reversal of the 4.2 proximity rebalance.** That fix was three
  quarters in the making for a real problem — this brief doesn't touch it.
- **Not a change to the 60-second callout timeout.** Different failure mode —
  that's the "offer vanished before I could respond" ticket theme, not this
  one.
- **Not mutual aid or shared cover.** Q4 exploration, unrelated to fixing the
  current loop.
- **Not a silent constant change in `history.py`.** Helen's ask specifically —
  this has to be something Kip can see and Meteor Mite can feel, not a number
  nobody notices moving.
- **Not anything that assumes a legal identity behind a responder.** Per the
  glossary, Rook holds cover identities only — any responder-facing messaging
  stays inside that.
- **Not a replacement for the written routing explainer.** Still owed, still
  separate — Wen is still the only real source on how ranking works end to
  end.

## Open questions, for whoever builds this

1. **What's the actual recovery curve** — points earned back per week with no
   offer, and is there a ceiling? Wen's 2019 TODO named the gap, not a
   number. This needs her sign-off before it's a spec.
2. **What's the guaranteed floor, precisely** — "no matched responder goes
   more than N days without an offer" — and when that floor callout collides
   with a genuinely closer responder on a live incident, which one wins?
   Without an answer here this is a principle, not a mechanism.
3. **Where does Kip's flag actually live** — roster badge, filtered view,
   push notification — and does Nadia's support view get the same signal? A
   "gone quiet" ticket gets closed with a guess today. This should let it get
   closed with an answer.

---

*Grounded in `dispatch-routing` (`config.py`, `offer.py`, `history.py`) and
`callout-history.csv`, 08–31 Aug 2026.*
