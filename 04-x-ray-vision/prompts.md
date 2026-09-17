# 04 · X-Ray Vision — prompts

**Context:** You joined Rook two weeks ago as PM on Dispatch.
Release 4.2 shipped on 12 August, just before you arrived, and
landed badly. Last session the numbers showed you what happened: a
ping used to wait ninety seconds and now it waits sixty, people
missed pings they used to catch, and missing one counts the same as
turning one down — so four responders stopped hearing from us
altogether.

At the end of the session, ask Claude Code to save the prompts you
wrote yourself below — not the starter prompt. The closing slide has
the exact prompt to paste. By Module 6 this file is a prompt library
built from your own questions.

---

### 1.

Using Vesper's or Meteor Mite's actual travel-time and capability numbers, run routing.py's score() formula twice — once with the pre-4.2 weights (proximity 0.45, recent-acceptance 0.40) and once with the current ones (0.60/0.25) from config.py — holding their recent-acceptance score constant. How many ranking positions does the weight change alone cost them, before any decline even happens?

### 2.

The timeout cut (90s→60s) and the weight rebalance shipped in the same release, and offer.py treats a timeout and an explicit decline identically — both call history.record_declined(). Does a shorter window measurably increase how often "didn't answer in time" gets counted as a decline, meaning the timeout change alone — independent of the weight rebalance — could be feeding the same downward spiral?

### 3.

Given the score floor in history.py and the still-unresolved 2019 TODO about whether the score ever drifts back to neutral on its own — once a responder is at the floor and getting close to zero offers, is a routing override (mentioned in the 4.0 changelog) the only way back in, and if so, is anyone actually using it, or is it sitting unused while people fall through?

### 4.

Pull whatever proximity/region signal exists for all 16 responders — not just the 9 already flagged — and check whether travel time to typical incident locations actually separates the collapsing four from the climbing five, or from everyone else too. We ruled out acceptance history; proximity is the other input that changed weight, so test it directly instead of assuming it by elimination.

### 5.

Among the six flat/unchanged responders (Cindermark, Ashgrove, Halfmoon, Ironvale, Bulwark, The Longcast), do any of them sit at a similar travel-time distance to the collapsing four? If a similarly-far responder didn't collapse, proximity alone doesn't explain the split and something else — capability tags, region-specific incident volume — is doing real work too.

### 6.

proximity_score() in routing.py hits zero at exactly 45 minutes (PROXIMITY_HORIZON_MINUTES) and falls off linearly before that. With the new weights, is there a specific travel-time cutoff where a responder flips from "usually competitive" to "almost never ranked high enough to get asked" — and do the four collapsing responders sit right on the wrong side of that line, which would explain why this looks like a hard split into two groups instead of a smooth gradient?

### 7.

The README says "everyone available is on the list — nobody removed." So a responder at the score floor is technically still ranked on every callout, just last. Walk through exactly what would have to happen for them to actually reach the top anyway — does it only happen when nobody else available outranks them (e.g., they're the only one free in their region for that window), and if so, how rare would that have to be in practice for someone to stay stuck for a month?

### 8.

capability_score() in routing.py can push someone up regardless of their proximity or acceptance score if they're one of the few who match a required tag. Does that mean recovery time isn't uniform — that a responder with a rare capability tag (aquatic, hazmat-tolerant) would climb back into contention far faster than one with common tags, purely because scarcity of skill can overpower a wrecked acceptance score in a way ordinary luck can't?

### 9.

The README also says "nothing in here decides whether somebody gets asked" — implying that decision might live somewhere outside this folder. Is there any filter upstream or downstream of this code (in the console, the mobile push service, or wherever available_for() actually pulls from) that could be quietly excluding a responder below some threshold, rather than just ranking them low the way this code claims to?
