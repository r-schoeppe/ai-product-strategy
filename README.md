# My AI Product Strategy

> A living strategy built across 6 sessions. Each module adds one component. By Module 6, this repo IS your strategy — version-controlled, board-ready, portable.

---

## Strategy at a Glance

| Component | Module | Status | Key Artifact |
|-----------|--------|--------|-------------|
| **The Bet** | M1 | [x] | `01-the-bet/` |
| **The Moat** | M2 | [x] | `02-the-moat/` |
| **The Margin** | M3 | [x] | `03-the-margin/` |
| **The Contract** | M4 | [x] | `04-the-contract/` |
| **The Guardrails** | M5 | [x] | `05-the-guardrails/` |
| **The Pitch** | M6 | [ ] | `06-the-pitch/` |

---

## The Bet (M1)

**What we're building, for whom, why now.**

- **Product:** TapeMine, 5-on-5 flag football video review, with the AI Scout scouting report for coaches
- **AI Value Archetype:** Oracle
- **Vulnerability Scores:** Moat 2/5 · Data 2/5 · Platform 3/5
- **Top Risk:** The AI summary alone is easy to copy; the moat depends on league relationships and a tag-data loop that does not exist yet
- **Confidence:** M
- **Prototype:** [`01-the-bet/prototype/index.html`](01-the-bet/prototype/index.html)
- **Kill Criteria:** In a 5-team pilot, fewer than 3 coaches read the report before a game for 2 straight weeks, or tendencies are rated wrong in more than 1 of 3 reports

→ Details: [`01-the-bet/`](01-the-bet/)

---

## The Moat (M2)

**Why this won't get copied in 6 months.**

- **Data Flywheel Score:** 5/20
- **Weakest Loop:** Correction (tied with Preference and Network at 1/5)
- **Competitive Position:** Axes: price for amateur teams (cheap to expensive) and depth in 5-on-5 flag football (specialised to generic). TapeMine: cheap and flag-specialised. Hudl: expensive and tackle-focused. WatchGameFilm: mid-priced, tackle-focused, weaker on usability.
- **Encroachment Defense:** Out-specialise on 5-on-5 flag football, stay far cheaper than competitors for amateur teams, and win on usability and performance. Top threats: Hudl Assist (70% of value at risk), WatchGameFilm (60%), Google (20%).
- **Vendor Portability:** Partial

→ Details: [`02-the-moat/`](02-the-moat/)

---

## The Margin (M3)

**Will this make money or bleed it?**

- **Gross Margin (current):** 40.8% before AI (€5 base per team; video costs about €2.96 per team whatever the price)
- **Gross Margin (AI-adjusted):** 70.3% (€10 base with Scout included plus an optional season pass; about €3.19 cost per team, of which 93% is video and only €0.23 is AI)
- **Pricing Model:** Outcome / resolution, Penetrate strategy. €10 base per team per month with the Scout report included, plus an optional gameplan season pass at €30 with a soft cap of 100 conversations
- **Cascading Strategy:** Routed by turn type, not a fixed split: lookups on a small model, explanations on a medium one, writing the gameplan on a frontier model (37% / 42% / 21% of turns). €0.117 per conversation, 65% below all-frontier
- **Break-even at:** The season pass loses money only beyond about 257 conversations a season (4x typical use). Video is the real margin driver: doubling video cost gives 43% margin, the paid encoding tier 24%

→ Details: [`03-the-margin/`](03-the-margin/)

---

## The Contract (M4)

**Why users will trust a probabilistic system.**

- **Reliability Target:** Accuracy 92%, hallucination under 1%, latency p95 under 4 s, drift under 0.5% a week, plus a hard gate of 100% number fidelity (all starting values, not yet measured)
- **Golden Dataset:** 22 rows, 6 adversarial (v1 target about 150)
- **Confidence UX:** Confidence is evidence, not the model's opinion: three tiers from the 95% lower bound of each tell (High 60% or more, Medium 40 to 60%, Low below 40% or under 4 plays), with counts, links to the plays behind it, and coach controls to correct and override
- **HITL Architecture:** Thresholded and sampled review. Coach "wrong" verdicts and failed checks go to a reviewer; every confirmed error becomes a golden row. The plain computed report is the fallback when the model fails
- **Failure Mode Coverage:** Red team found three failures now covered by test rows: hidden instructions in file names and notes, stale tendencies, and cross-team data access. Still open: whether the league's cut files contain all plays (biased sample), and youth player privacy

→ Details: [`04-the-contract/`](04-the-contract/)

---

## The Guardrails (M5)

**What breaks when this scales — and what compounds.**

- **Compounding System:** Recursive learning is broken (signals are collected but nothing reads them yet); cross-domain transfer and network intelligence are missing. Collected signals: confirm, swap, doesn't fit with a reason layer, edit, and the after-match debrief
- **Governance Posture:** Insights are kept apart from gameplan decisions. The AI drafts and the coach confirms every answer; actions outside the policy are unavailable by design; monthly review of flagged items by the product owner
- **Shadow AI Status:** 6 workarounds found (hypotheses to validate with coaches), 2 build candidates after triage
- **Agent Boundaries:** Opponent Insights is read-only; Gameplan Builder drafts and the coach decides; Signal Processor (planned) is read-only and its suggestions are evaluated by the product owner
- **Regulatory Exposure:** EU AI Act minimal to limited risk; GDPR applies because film shows players, possibly minors (no player identification, team data separated, processor agreements). To be confirmed with a data protection advisor

→ Details: [`05-the-guardrails/`](05-the-guardrails/)

---

## The Pitch (M6)

**How you get this funded, shipped, and adopted.**

- **Horizon 1 (Now):** (draft until the roadmap is built) Number-fidelity gate with plain-report fallback; evidence counts and clip links; golden set of 22 rows
- **Horizon 2 (Next):** (draft) Gameplan builder with three-tier confidence, signal capture and after-match debrief; 5-team pilot and a pricing test, with kill criteria
- **Horizon 3 (Bet):** (draft) Signal Processor and a published reliability report per season; league-level learning only after privacy and trust are settled
- **Board Narrative:** (draft) TapeMine gives amateur flag football teams an evidence-backed scouting report and a gameplan they confirm themselves, at about 70% gross margin, with trust built from checks and a published test gate and not from model quality

- **Key Metric:** (draft) First-pass acceptance of suggested answers, checked against the after-match "worked" rate

→ Details: [`06-the-pitch/`](06-the-pitch/)
