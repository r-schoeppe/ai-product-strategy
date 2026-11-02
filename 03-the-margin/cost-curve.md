# Cost Curve & Pricing Strategy

## Packaging Decision

| | Feature |
|---|---|
| **Leader** | Scout summary |
| **Filler** | None at the moment (candidates later: inconsistent-tag detection, suggested playlists to annotate) |
| **Killer** | Deep gameplan conversation with coaches |
| **Killer usage %** | 20% (hypothesis, not measured; most coaches work differently for the moment) |
| **Bundle or add-on** | Leader in the base plan; Killer as an add-on, sold as a season pass |

70% rule: Killer usage is under 70%, so it is an add-on.

## Cost Model

Per team per month (one team = one user). Mux prices in USD treated as EUR. All prices are placeholders to check.

| Cost Category | Per-User/Month | Notes |
|--------------|----------------|-------|
| Inference (primary model) | €0.219 | Scout summary on a medium model, plus medium and frontier turns of the gameplan chat |
| Inference (cascading/triage) | €0.009 | Small-model turns of the gameplan chat |
| Infrastructure | €0.80 | Mux encoding (basic tier, free) and delivery |
| Data/storage | €2.16 | Mux storage, average over an 8-month season (32 games x 40 min) |
| Human-in-the-loop | €0.00 | None yet; simple coach feedback to be collected |
| **Total AI COGS** | **€3.19** | 93% is video, AI is €0.23 |

Auto-tagging from raw video is not built and is excluded from the totals. If every team used it, it would add about €6.00 per team per month.

## Cascading Strategy

Applies to the gameplan conversation. Compared five policies across four game situations (quick check, full gameplan build, halftime adjustment, post-game review) with each turn typed as Lookup, Explain or Synthesis.

**Triage model:** small tier, about €0.30 per 1M tokens (lookups from the computed tendencies)
**Frontier model:** frontier tier, about €6.00 per 1M tokens (writing the structured gameplan); medium tier about €1.50 for explanations
**Routing rule:** by turn type, not a fixed percentage. Lookups to small, explanations to medium, gameplan synthesis to frontier.
**Expected cascade ratio:** 37% small / 42% medium / 21% frontier (share of turns)

| Policy | Cost per conversation | vs all-frontier | Synthesis turns on frontier |
|---|---|---|---|
| Single medium model | €0.084 | -75% | 0% |
| Single frontier model (quality bar) | €0.335 | baseline | 100% |
| Blind 80/20 split | €0.080 | -76% | 20% |
| Task-routed (L small, E medium, S frontier) | €0.117 | -65% | 100% |
| Task-routed lean (L, E small, S frontier) | €0.089 | -74% | 100% |

A blind 80/20 split is cheaper but sends the gameplan writing to the small model 80% of the time, so it is rejected.

## Pricing Model

**Current pricing:** €5 per team per month (video library, tagging, review)
**Proposed AI pricing:** €10 per team per month with the Scout summary included, plus an optional gameplan season pass at €30 per season (estimated cost per conversation €0.117)
**Model:** outcome / resolution, sold as a season pass because games are not evenly distributed (Penetrate strategy)

**Soft cap:** 100 conversations per season (about 3 per game; a typical team uses about 64). It is a threshold, not a wall, because a coach who keeps iterating is often telling us the first draft was not good enough. At 80% the coach sees what is left. At 100% nothing stops and one tap asks what was missed: if our output was at fault (wrong facts, missing situation) the refill is free (+25, up to 2 per season); if it is exploration or new information, a top-up pack is offered or lookups continue on the small model. A hard stop at 200 only catches abuse, and reasons are reviewed monthly to feed the Correction loop. The pass loses money only beyond about 257 conversations a season (4x typical); at the cap a team costs about €11.69 against the €30 pass.

| Conversations per season | Margin on the pass |
|---|---|
| 64 (typical) | 75% |
| 100 (soft cap) | 61% |
| 150 | 42% |
| 200 | 22% |
| 257 (break-even) | 0% |

## Stress Tests

| Scenario | Impact on Margin | Response |
|----------|-----------------|----------|
| Inference costs 3x | 66.1% (from 70.3%) | Switch the default model through the model-agnostic package, tighten the router so fewer turns reach frontier, cache reports. |
| Heaviest segment doubles (2x conversations) | 69.4% (from 70.3%) | The pass is flat, so revenue does not follow usage. The soft cap bounds the extra cost and the top-up pack covers what is above it. |
| Every pass-holder uses the full soft cap | 69.4% (from 70.3%) | Worst case the cap allows. Cost per team is bounded by the cap, so this is the margin floor for the add-on. |
| Model provider raises prices 50% | 69.3% (from 70.3%) | Fall back to the second provider, run the test set, switch the default. |
| Video cost 2x | 42.8% (from 70.3%) | Move old film to cold storage and cap storage per team. |
| Mux Plus encoding instead of basic | 24.2% (from 70.3%) | Stay on basic encoding unless a coach feature needs more. |

## Board One-Pager

**Before (traditional SaaS):** 10 teams x €5 = €50 per month; COGS €30 (video); gross margin 40.8%
**After (AI-enabled):** 10 teams x €10 base plus the optional season pass = €108 per month; COGS €32 (video plus AI); gross margin 70.3%
**Soft-cap floor:** if every pass-holder used the full cap, margin would be 69.4%.
**Net margin shift:** +29.5 points; gross profit from €20 to €76 per month. Before, 10 teams at €5 leave 41% margin, because video costs about €2.96 per team whatever the price. After, revenue rises 115% (a higher base plus the optional season pass) while AI adds only €2 of cost, so margin moves from 41% to 70% and gross profit from €20 to €76 a month.

**Risks we are carrying:**
- Heavy-use tail: a pass-holder loses money only beyond about 257 conversations a season (4x typical). The soft cap with a reason-gated refill bounds it: 61% margin on the pass at the cap, 69% overall floor.
- Video drives margin: it is 93% of cost. Video cost 2x gives 43% and the paid encoding tier 24%. Stay on basic encoding and watch storage per team.
- Price acceptance is untested: the margin depends on teams accepting €10 instead of €5 for Scout. Test with real coaches first.
- Quality drives cost: iterations per accepted gameplan is both a cost driver and a quality signal. We assume heavy iteration means a weak first draft, which still needs validating because it can also be exploration.
- Placeholders: token and Mux prices, and 20% add-on adoption, are estimates not yet measured.

## Summary

TapeMine Scout gives flag football coaches a scouting report on their next opponent from the plays they have tagged. The base plan is €10 per team per month, with Scout included, plus an optional season pass at €30 for the gameplan conversation, with a soft cap of 100 conversations.

One team costs us about €3.19 a month to serve and brings in about €10.75, so we keep about 70%. The surprise is where the cost sits: 93% is video storage and playback, and the whole AI side is €0.23. Even if AI prices triple, margin only moves to 66%. What moves it is video: double the video cost and margin is 43%, and the paid Mux tier would take it to 24%.

The gameplan chat is the only feature whose cost grows with use, so it is sold as a season pass because games are not evenly spread, and a soft cap bounds the worst case at 69% margin. We route it by turn type, lookups on a small model, explanations on a medium one and the gameplan writing on a frontier model, which costs €0.117 per conversation, 65% below running everything on frontier, without lowering quality where coaches look.

Compared with the €5 video-only product, 10 teams move from 41% to 70% gross margin. The open risk is whether coaches will pay the higher base for Scout.
