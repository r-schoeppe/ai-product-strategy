# Three-Horizon Roadmap & Board Pitch

> **Status: DRAFT.** Roadmap generated from the strategy components (Modules 1 to 5) and the pilot framing; not yet reviewed. All thresholds in the kill criteria are placeholders to be set by the owner. The AI Evaluation and Board Pitch were written after the strategy was reviewed; the M1 comparison section is still to be written.
<!-- DRAFT: first version, 2026-11-16. Horizons use the AI-compressed scale from Module 6 (H1 0-4 weeks, H2 1-3 months, H3 3-6 months). -->

## Roadmap

### Horizon 1, Ship (0-4 weeks)
*High confidence. Ship with existing capabilities.*

| Initiative | Strategy Component | Why it ships now | Confidence |
|---|---|---|---|
| Computed Scout report with confidence tiers and evidence counts | Bet | The prototype already computes it, so this is hardening | H |
| Number-fidelity gate and plain-report fallback | Contract | Plain code, no new capability | H |
| 22-row golden set, reviewed by a real coach and run weekly | Contract | The rows exist, and a coach review is cheap | H |
| Film completeness check, and confirming what the league's files contain | Contract | The red-team's biggest open risk; it decides whether tendencies are biased | H |
| Basic Mux encoding, a storage cap and a cold-storage policy | Margin | Video is 93% of cost, and this is configuration | H |
| Signal event log: confirm (slot or bulk), swap, doesn't-fit reason layer, edit | Moat | Collection only, the first step of the Correction loop | H |
| Privacy review by an advisor, row-level security check, AI-drafted labels, injection scan | Guardrails | Needed before any youth film is used | M |
| Coach interviews to replace the shadow AI hypotheses | Guardrails | Costs only time | H |

### Horizon 2, Validate (1-3 months)
*Medium confidence. Strategic bets with a named hypothesis and kill criteria (thresholds are placeholders).*

| Initiative | Strategy Component | Hypothesis | Kill Criteria | Confidence |
|---|---|---|---|---|
| Gameplan sheet builder (instant draft, section by section, from the playbook) | Bet | Given this tool, coaches build a plan before the game instead of calling plays by instinct | If fewer than half of pilot games have a coach-confirmed sheet by week 6, we stop | M |
| League pilot validating pre-game use | Bet | A league will supply film and teams, and coaches will use the sheet | If the league film-access agreement is not signed by week 4, we stop | M |
| Team playbook setup plus a sport knowledge pack (rules, mechanics, verified stats as priors) | Moat | Priors from the sport help thin-data teams | If verified stats cannot be sourced by week 6, keep rules and mechanics only | M |
| Evidence-panel play corrections that recompute the tell | Moat | Coaches fix mis-tagged plays when they see the effect | If under 1 in 5 pilot teams use it by week 6, we stop | L |
| After-match debrief (worked, did not, not run) linked to confirms | Moat | A short debrief yields usable team-specific results | If under a third of debriefs are completed by week 6, we change the format | M |
| Weekly gate, calibrated LLM judge and monthly coach audit | Contract | The gate catches regressions before coaches do | If the judge disagrees with coach labels on more than 1 in 5 rows by week 6, we stop using it | M |
| Model-agnostic layer with routing by turn type and a second-model fallback | Margin | Routing cuts chat cost by about 65% without lowering plan quality | If the routed plan scores worse than the single-model baseline on the gold set, we stop | M |
| Shareable sheet for players on phones | Bet | Players read the sheet before the game | If under a third of players open it by week 6, we stop | M |

### Horizon 3, Explore (3-6 months)
*Low confidence. Small-investment experiments.*

| Initiative | Strategy Component | What must be true first | Confidence |
|---|---|---|---|
| Signal Processor (read-only) and the compounding workflow | Moat | The pilot produces enough events, and thresholds for acting on signals are defined | L |
| Gameplan season pass with soft cap and reason-gated refill | Margin | Pre-game use is proven, and the chat's real cost per team is measured | M |
| League-level flag football platform (benchmarks, shared film access, optional pooled priors) | Bet | A league commits, and a privacy decision is made on pooling | L |
| Other small-sided sports through new sport knowledge packs | Bet | The flag football knowledge pack works and each new sport can be built cheaply | L |

### Unmapped (cut or rethink)

| Initiative | Why it's unmapped | Recommendation |
|---|---|---|
| Automatic tagging from raw video | Not in the pilot; expensive, and WatchGameFilm already offers it | Rethink: a post-gate platform item that cuts the coach's tagging effort |
| Connector to coaches' own AI assistants | Dropped earlier; not margin-relevant and it loses the feedback signal | Cut |
| Open chat Q&A as the main interface | Replaced by the structured sheet builder | Cut |
| Wired keyboard shortcuts and print styling | Polish, connects to no component | Rethink as polish after the pilot |

**Mapping disagreements:** none, no user mappings were given.

**Most over-indexed horizon:** H1, and Contract and Guardrails, because trust and safety work is cheap to plan and no coach has used the product yet. Missing: H2 user evidence beyond the pilot and an H3 answer to the market-size doubt.
**H3 bet to protect if budget is cut:** the league-level flag football platform, the only item that answers "can this be a business in an amateur sport".
**Initiative to kill today:** automatic tagging from raw video.

## AI Evaluation

*Written as a critical review of the strategy as it stands (Modules 1 to 5, the roadmap and the pitch). Nothing has been tested with real coaches yet, so scores reflect that. Numbers marked "guess" are our own estimates.*

**Bet Validation**, Score: 2/5
- Strengths: A falsifiable hypothesis (coaches confirm a gameplan before kickoff and put in the data afterwards), dated kill criteria (February 2027, March 2027, mid-season 2027) and a defined cheapest test.
- Gaps: There is no user evidence yet: no coach interviews, no usage data, no pilot. The bet rests on conviction and competitor research. The shadow AI list is hypotheses, the league film agreement is unsigned, and the film's completeness is unconfirmed.
- Recommendation: Before the committee meets, run 10 to 15 coach interviews and a dry run with a handful of teams on last season's film, and measure the minutes of tagging per game.

**Capability Assessment**, Score: 3/5
- Strengths: The computing core exists in the prototype. Computing the numbers in code, with the AI only writing them up and a plain-report fallback, lowers the AI capability risk. Agent boundaries are clear.
- Gaps: The gameplan builder, tagging screen, playbook setup, signal log, debrief and a golden set of about 150 rows are not built. 1.6 people for about 100 teams in Europe and the US, including support, is ambitious. Dependencies: the video provider, the model provider, the league's files and a privacy review in two jurisdictions.
- Recommendation: Stage the pilot (a small first group, then expand) and build only the three flows the gate needs: tag, plan, debrief.

**Impact Analysis**, Score: 2/5
- Strengths: The pilot metrics are defined (confirmed sheet before kickoff, debrief and tagged plays), and unit margin is about 70%.
- Gaps: No metric ties to revenue, and market size is unknown. On our guess of about 1,000 amateur teams in Europe at €100 to €180 a year, even full penetration is about €100k to €180k a year, so Europe alone is small. The business case depends on the US, leagues and the platform, none of which is quantified. Compounding evidence arrives no earlier than the 2028 season.
- Recommendation: Build a bottom-up team count for Europe and the US from federation data, with real willingness-to-pay anchors, before the pitch.

**Defensibility Check**, Score: 2/5
- Strengths: The strategy concedes that the summary is copyable (we rate 60 to 70% of its value at risk from Hudl and WatchGameFilm) and bets on coach effort kept per team. Evidence on every claim and 5-on-5 specifics exist in the design.
- Gaps: A platform or competitor could ship a summary within 12 months. The data flywheel scores 5 out of 20 and the Correction loop 1/5; the loops are designed, not live. Switching cost is unproven, and the moat depends on effort coaches have not yet shown they will give.
- Recommendation: Make the team's playbook and confirmed-gameplan history the switching cost, capture correction signals from day one, and pursue a league film agreement that competitors lack.

**Pricing Alignment**, Score: 3/5
- Strengths: About €3.19 to serve a team per month, with AI only €0.23. Price is close to what teams pay today (WatchGameFilm lists $100 a year, Hudl $400 to $1,600). Margin is about 70% at €10 and about 79% at a placeholder €15. A soft cap bounds heavy users, and stress tests were run.
- Gaps: There is no willingness-to-pay signal. Today's price is inconsistent between files (€5 in the cost model, about €10 in the deck). The higher justified price is a placeholder. Video cost drives margin (the paid video tier would leave about 19%).
- Recommendation: Settle one price baseline and ask the interviewed coaches for price reactions. Keep the paid video tier off.

**Trust & Reliability**, Score: 4/5
- Strengths: A golden set of 22 rows with 6 adversarial cases. Confidence is evidence (counts and a lower bound), every claim links to its plays, a number-fidelity gate and a plain-report fallback exist, and a reliability contract has targets and consequences.
- Gaps: Nothing is measured yet, and the targets are placeholders. A real coach has not reviewed the 22 rows, and 22 is far from the 150 planned. Film completeness bias is unknown.
- Recommendation: Have two real coaches review the 22 rows and run the number-fidelity check on the prototype before the pilot.

**Governance & Scale**, Score: 3/5
- Strengths: A governance policy v0.1 with scope, autonomy boundaries, escalation, an audit cadence with named owners and regulatory notes. Read-only insight agents and a coach who confirms every answer. A feedback design that records confirms, swaps, doesn't-fit reasons, edits and debriefs.
- Gaps: All of it is designed and none live. One owner holds every audit row. The privacy review for youth film (EU and US) is not done. At 10x, video storage and support load break first. The shadow AI audit is hypotheses, and the compounding workflow is undefined.
- Recommendation: Run the privacy review before any youth film is used, replace the shadow AI hypotheses with coach interviews, and name a second reviewer or advisor.

**Gap Identification**, Score: 3/5
- Strengths: The strategy names most of its own gaps (the effort bet, the thin moat, the placeholder numbers).
- Gaps: The weakest components are the Bet (no user evidence) and the Moat (flywheel 5/20). Untested assumptions: coaches will tag and debrief, the league's files are complete, €10 to €15 is acceptable, the team-count guess and that competitors will not ship soon. A skeptical board member would ask: why would a volunteer coach spend time tagging and debriefing every week? That is not yet answered.
- Recommendation: Measure the minutes of effort per game in the dry run, and treat automated tagging as the post-gate fix if the effort is too high.

- **Overall Score:** 2.8/5. A coherent strategy at the pre-validation stage: strong on trust and honesty about weaknesses, weak on user evidence, market size and defensibility.
- **Biggest Risk:** Coaches do not put in the tagging and debrief effort that both the product and the moat depend on.
- **Top 3 Actions:**
  1. Run 10 to 15 coach interviews and a dry run on last season's film before January 2027, to measure effort, pre-game intent and price reaction.
  2. Secure the league film-access agreement, confirm the files contain every play, and complete the EU and US privacy review before youth film is used.
  3. Fix the numbers: one price baseline, a bottom-up team count for Europe and the US, and a coach-reviewed golden set with a measured number-fidelity check.

## Board Pitch

**Audience:** a founders or funding committee deciding whether to fund a first pilot. Cares most about why now, why this team and the cheapest way to find out. Doubts that an AI scouting product can become a real business in an amateur sport, where budgets are small, coaches are volunteers and league analytics are thin to nonexistent.

**Thesis (1 sentence):**
TapeMine gives volunteer flag football coaches a gameplan built from their own film before kickoff, and the effort they put in becomes team data no competitor can copy.

**The case:**
1. Why now: In July 2028 flag football debuts at the Los Angeles Olympics as a 5-on-5 sport, NFL owners have approved player participation, and Euro Flag 2025 drew a record 43 national teams from 25 nations. Teams are professionalizing while tooling lags: the one tendency product we found lists formation and series data as 11-man only, and league analytics are thin to nonexistent. The 2028 season is the Olympic year, so a pilot starting in spring 2027 reads its first compounding result in that season.
2. What's defensible: Not the summary. WatchGameFilm or Hudl could add one, and we rate 60 to 70% of its value at risk. What compounds is the coach's own effort, kept per team: corrections, preferences (confirm and swap) and debrief results, the three feedback types of the course's data flywheel. Our flywheel scores 5 out of 20 today and the Correction loop, the weakest, scores 1/5, so this is a bet the pilot must prove, not a moat we have. What exists now is evidence on every claim and a design built for 5-on-5.
3. The economics: About €3 to serve a team per month, of which only €0.23 is AI and the rest is video. At about €10 a team the gross margin is about 70%, and at a higher price justified by better value (placeholder €15) about 79%. Stress at today's price: AI cost tripling leaves about 64%, video cost doubling about 39%, the paid video tier about 19%. Price relates to what teams already pay for film software (our guess about €100 a year; WatchGameFilm lists $100, Hudl $400 to $1,600). Prices and costs are placeholders, and the pilot holds price.

**The risks:**
1. Trust / failure modes: The front-page risk is youth film exposed or misused: team data is separated by design, individual players are never identified, and a privacy review for the EU and the US is budgeted at about €5,000 and not done yet. The product failure is a confident wrong tell that costs a game: confidence is shown as counts, not a model score, every number must match the computed value, a 22-case test set blocks bad releases and a plain computed report is the fallback. The reliability targets (92% accuracy, under 1% unsupported claims, under 4 seconds, under 0.5% drift a week) are targets, not measurements.
2. Scale / governance: At 10x, video storage and support load break first, not AI cost, so we stay on the basic video tier, cap storage and stage the pilot, since 100 teams in two regions with 1.6 people is the strain. The AI only reads and drafts; the coach confirms every answer. The real scale risk is effort: if coaches do not tag and debrief, nothing compounds. This is the weakness our own evaluation scored lowest, and it is why the pilot measures effort as well as use.
3. Competitive: The scenario that forces a kill is WatchGameFilm or Hudl shipping flag scouting on film coaches already upload. The kill criteria answer it: we stop if fewer than half of pilot games have a coach-confirmed sheet before kickoff by mid-season 2027, or if fewer than a third of games get a debrief or fewer than 10 plays are tagged a game, because then a summary is the whole product. We also stop before the season if no league film-access agreement is signed by February 2027.

**The ask:**
€83k now for the first 8 months (December 2026 to June 2027), plus €88k only if the mid-season gate is passed, for 1.6 people (one full-time builder and a 0.6 FTE community and coach-success lead). That funds a pilot with about 100 amateur teams in Europe and the US, 4 to 6 coach case studies, a signed league film agreement, a tested reliability gate, and about €5,000 of AI evals and simulations. In return you get one measured answer by mid-season 2027: whether amateur coaches engage before the game (a confirmed sheet) and after it (a debrief and tagged plays). Paused until the gate and not part of this ask: deep playbook integration, automated tagging, practice plans drawn from debrief gaps and player film study, the platform direction. Decision needed by January 2027, so the pilot is ready when the season starts. All figures are estimates; salaries and the privacy review quote are placeholders.

### Presenter notes

- **Opening line (literally say this first):** "Flag football goes to the Olympics in 2028, and the teams on that path still prepare with a whiteboard and a hunch; we are betting we can change that, and we will know in eight months for €83,000."
- **If you only get 60 seconds:** Thesis: we give volunteer flag football coaches a gameplan from their own film before kickoff, and their effort becomes data no one else has. Key risk: the summary is easy to copy, so the whole bet is whether coaches put in the work. Ask: €83k for 8 months, and we stop at mid-season if fewer than half of pilot games have a confirmed sheet before kickoff.
- **The one question they'll ask first:** "Is there a business in amateur flag football, where budgets are small and volunteers coach?" Answer: We do not know yet, and on our own guess of about 1,000 teams in Europe at €100 to €180 a year, Europe alone is worth roughly €100k to €180k a year at full share, so the business case rests on the US, leagues and a platform; the first €83k buys one measurement, whether coaches engage at all, at about €3 per team per month to serve.

## M1 Baseline vs. Now
*Your 3-sentence AI strategy from Module 1 vs. what you'd say now:*

**M1 baseline:**

**Now:**
