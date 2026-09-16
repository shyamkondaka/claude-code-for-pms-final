# 03 · Rewind — prompts

**Context:** You joined Rook two weeks ago as PM on Dispatch.
Release 4.2 shipped on 12 August, just before you arrived, and
landed badly.

Last session you read four conversations and every support ticket
since 4.2 — and found the two piles did not agree.

At the end of the session, ask Claude Code to save the prompts you
wrote yourself below — not the starter prompt. The closing slide has
the exact prompt to paste. By Module 6 this file is a prompt library
built from your own questions.

---

### 1.

Pull whatever's known about each of these nine responders — capability tags, region, the "wide geography" description from the 4.2 release notes — and check whether the four collapsing responders (Farlight, Meteor Mite, The Undertow, Vesper) share something structural in common that the routing-weight rebalance would specifically penalize, versus the five climbing ones. If there's no shared trait, the split might not be routing at all.

### 2.

The last two weeks show 0 of 6 and 0 of 3 accepted for the collapsing group — is that a real trend or just a small-denominator artifact? What does the drop look like if I extend the window a few more weeks, or is two weeks at single-digit ping counts too thin to call "collapsed to zero" rather than "temporarily quiet"?

### 3.

Trace these nine responders' actual inputs — proximity, capability match, recent-acceptance history — through routing.py's formula for the weeks in question. Does the code, run on their real numbers, predict this exact split, or is it equally consistent with something else that changed the same week (incident geography that period, a capability-tag mismatch) that has nothing to do with the rebalance?

### 4.

Priya's working theory is "mostly seasonal, August is soft every year." If that were true, all 16 responders in callout-history.csv should dip together during the same weeks. Does the data show a uniform dip across everyone, or does it show a split where roughly half climb while the other half collapse — and if it's a split, can "seasonal" survive that, or does seasonality only ever produce a uniform effect?

### 5.

For each ticket in 00-rook/feedback/tickets, compare its filing date against that specific responder's own row for that week — does the complaint ever get filed before the CSV shows anything wrong for that responder? If handlers are filing "gone quiet" tickets ahead of their own responder's actual numbers moving, that's a sign of handlers reacting to rumor or to what they're hearing from other handlers, not to what's happening in their own coverage view.

### 6.

Tickets carry a self-assigned severity (Low/Medium/High). Does that severity actually track the size of the real decline in the CSV for that responder — or are there Low-severity tickets sitting on top of a near-total collapse (Farlight, filed Medium despite going to zero) and Medium-severity tickets where the CSV shows no real change at all (Cindermark, Longcast)? If severity doesn't track magnitude, it can't be used to triage which of these are worth engineering time.

### 7.

If Vesper's recent-acceptance history dropped because she stopped getting offers, and getting offers is exactly what would let that history recover — does routing.py or history.py show a way out of that loop on its own, or is a responder who's been pushed to near-zero offers structurally stuck there until someone intervenes? I need to know if "it'll fix itself" is something I can honestly tell her.

### 8.

Was there anything in the console or the app that would have shown Vesper or Dot this was happening in real time — a declining trend, a rank drop, anything — or is this only visible now because I went and built a week-by-week table from a raw CSV nobody hands a handler? If she asks "could I have known," I want the true answer before I give her one.

### 9.

Given Priya's warning that this can't become a "revert 4.2" conversation, what's the actual remedy I could describe to Vesper — a floor on how far acceptance history can suppress someone's rank, a manual re-rank, something else in the routing code — that fixes her situation without undoing the proximity fix the wide-geography responders earned?
