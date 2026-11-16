# Compounding System Design

## Feedback Loops

| Loop | Input | Output | Compounds? | Status |
|------|-------|--------|-----------|--------|
| Recursive Learning | Coach confirms, swaps, doesn't-fit reasons and edits per answer, plus after-match debrief results | Suggestions re-ranked per team; tell weights; better tag checks | Y | broken |
| Cross-Domain Transfer | Which counters worked for which situation and formation | Better suggestions for adjacent situations and opponents | Y | missing |
| Network Intelligence | Anonymised, coach picks and outcomes pooled across teams | Priors for thin-sample opponents, league benchmarks | Y | missing |

### Signal collection (recursive learning)

Scope for now: collect the signals. How they compound is defined later.

| Signal | What it likely means | Strength | Caveat |
|---|---|---|---|
| Confirm | The suggestion was good enough to use | Medium. Counted as first-pass acceptance rate on each answer's first decision, by situation, side and evidence tier | A bulk confirm (the "Confirm situation & next" button) is recorded as `via bulk` and counts as weaker; it is checked later against the debrief. A reopen retracts a confirm. |
| Swap | A bad fit, or just a different taste | Weak. Only counted if the alternative is kept | Two options may be equally good; mostly team preference, not a verdict on the suggestion |
| Doesn't fit | The suggestion was wrong; the reason says which layer failed | Strong with a reason | Reason is optional. Layers: the read is wrong, we can't run this, this game is different, I prefer another approach |
| Edit | What the coach would do instead | Strong, because it is the answer itself | Compared by playbook concept: unchanged, different playbook concept, free text unmatched (possible playbook gap), or a new answer on an open slot. Number edits to a tell follow the 20-point rule. |
| After-match debrief | Whether the plan helped, per answer: worked, did not, not run | Weak and noisy | Team-specific, tiny samples, results mix a wrong read, a bad plan, execution and luck |

**Event record (one per action):** time, team, game, answer, actor, type (confirm, swap, doesnt_fit, edit, reopen, outcome) and details (via answer button or bulk, evidence viewed or not, reason layer, from and to concept).

**Handling the debrief carefully:** results are stored per team and never pooled with other teams. "Not run" is an option so untested calls do not look like failures. Results are shown as plain evidence ("worked 4 of 5 times for you") and do not reorder suggestions until a call has been run several times; the threshold is defined with the compounding workflow. The debrief is agreed as a mechanism, and its exact format is to be tested with coaches.

**Scope of signals:** swaps, preference edits, playbook gaps and outcomes stay with the team. "The read is wrong" reasons and play corrections could help all teams later, only after review.

**Prototype:** the builder board in the design canvas records these events and shows them in an owner-only panel.

**Broken loop identified by partner:** Recursive Learning is broken because it is collect-only. Signals are recorded, but nothing reads them, so a coach's "the read is wrong" on a tell changes nothing next game. A second problem: bulk confirms inflate acceptance, and nothing links a confirm to its debrief result yet. (Partner played by Claude.)

**Fix plan:** (1) An owner-run monthly review reads the flagged events, as in the audit cadence. (2) Every confirmed "the read is wrong" becomes a golden-set row and a tag-consistency check. (3) Debrief results are shown to the coach as plain evidence ("worked 4 of 5 times for you") but do not reorder suggestions until a call has been run several times. (4) Each confirm is linked to its debrief result so bulk confirms can be checked.

## Context Connectivity

**Flows well:** within one team, tags feed the Scout report, the gameplan sheet and the collected signals.

**Where knowledge silos:**
- Team to team: each team's tags, playbook and results stay in their own scope. This is right for privacy, but no team learns from another.
- Season to season: data resets with roster changes, so a team starts almost fresh each season.
- Film to outcomes: tags and after-match results are stored apart and not yet linked.
- Insights to playbook: the sheet suggests only from the team's playbook, and only "playbook gap" edits tell us what is missing.

**Freeze test:** if the model were frozen for 3 months, TapeMine would still win today, on price, flag-football depth and usability. By the course's rule that means it is not compounding yet; the loops above are what would change that.

## Governance Policy

**Scope:** TapeMine Scout and Gameplan Builder, v0.1. Covers the Scout report generated from a team's tagged plays; the gameplan sheet builder (structured steps and a contextual chat inside a section); and the data they use: tagged plays and results, the team's playbook, coach confirms, swaps, reasons and edits, after-match debrief results, and play video served through Mux. Excludes automatic tagging from raw video (not built), anything that identifies individual players, pooling data across teams (not decided), and any assistant outside TapeMine.

**Autonomy boundaries:**
- Opponent insights (read-only analysis of the opponent's tagged plays). OK solo: compute tendencies, assign confidence tiers, flag data-quality problems, write up the computed numbers (the plain report is the fallback), answer questions about the opponent's data. Needs a human: nothing; insights are advisory and shown only to the coach.
- Gameplan creation (what we will do, built from the insights and the team's playbook). OK solo: draft the first version of a sheet, marked as a draft; suggest counters and alternatives from the team's own playbook; run validation checks; answer questions inside a section. Needs the coach: accepting an answer into the sheet, even from a high-confidence tell; using a low-evidence tell in a plan; changing the playbook. Needs a TapeMine reviewer: confirming a coach's "wrong" verdict into the golden test set.
- Actions outside these lists (contacting players, changing tags, reading another team's data, identifying players) are not available to the system by design: no tool exists for them and team data is separated by row-level security. Sharing a sheet is a normal screen action by the coach, not an agent task.

**Escalation triggers:** (1) Background flag when a coach's edits to an opponent insight differ significantly from the suggestion: the main call changes, a tell is removed, its share moves 20 points or more, or 3 or more plays are retagged. The coach is not interrupted, the coach's edit always stands, and the original and the edit are both kept. (2) A "doesn't fit" option on every gameplan suggestion, with a reason layer (the read is wrong, we can't run this, this game is different, I prefer another approach) and an optional line, stored with the suggestion, its evidence and the coach's replacement. Flagged items are reviewed monthly by the product owner and feed improvements and golden test cases.

**Audit cadence:** every row has a named owner; the product owner until the team grows.
- Continuous: automatic checks (number fidelity, injection scan, alerts from the reliability contract). Owner: product owner.
- Weekly: golden dataset run against the current model and prompts. Owner: product owner.
- Monthly: review of flagged items (doesn't-fit reasons, significant edits), a check of bulk confirms against debrief results, and the judge audit with two coaches. Owner: product owner.
- Quarterly: policy review, data retention check and a review of this document. Owner: product owner.

**Regulatory exposure (EU AI Act / other):** to be confirmed with a data protection advisor. EU AI Act: minimal to limited risk (a sports analytics and planning tool, not in the high-risk categories); control: sheets and answers are labelled as AI-drafted. GDPR: applies, because film shows players, possibly minors; controls: no identification of individual players, team data separated by row-level security, no training on customer film without consent, processor agreements with the hosting, video and model providers, an EU data region where possible, and a human who answers privacy requests within the legal deadline.

## Agent Topology

| Agent | Can do | Can't do | Approval |
|---|---|---|---|
| Opponent Insights | Read the selected opponent's tagged plays, compute tendencies and tiers, write up the numbers | Write anything, see other teams' data, act on notes or file names | None, it is advisory |
| Gameplan Builder | Read the insights and the team's playbook, draft answers, answer questions inside a section | Confirm answers or change the playbook | The coach, for every answer |
| Signal Processor (planned) | Read one team's events, find patterns (for example repeated "the read is wrong" on one tell), propose improvement suggestions and new golden-set rows | Change live suggestions, weights or the golden set; mix data across teams | None for the agent, it is read-only. The product owner evaluates its improvement suggestions and golden-set additions before anything changes. |

**The four knobs:** Autonomy: the first two draft only and the third only proposes. Tool calls: a whitelist of read, compute and draft, all logged, no outside calls. Memory: sheet versions and events persist with the team, chat stays with its sheet, nothing carries across teams. Chain: if Opponent Insights fails the Builder shows the gaps and the plain computed report; if the Signal Processor fails nothing changes for coaches because it never writes live.

## Shadow AI Audit

Hypotheses to validate with real coaches. Columns: Tool = workaround, Owner = signal source, Risk = frequency, Decision = build, partner or ignore.

| Tool | Owner | Risk Level | Decision |
|------|-------|-----------|----------|
| Pasting report numbers into ChatGPT to write a game plan (capability gap) | Hypothesis, coach interviews | H | build (the gameplan builder) |
| Spreadsheets to track opponent tendencies by hand (workflow gap) | Hypothesis, coach interviews | H | build (the Scout report replaces them) |
| Photos of whiteboard play diagrams sent to the team chat (workflow gap) | Hypothesis, coach interviews | M | partner or ignore (a sheet export covers part of it) |
| Another video tool to share clips with players (workflow gap) | Hypothesis, coach interviews | M | ignore for now (our playlists cover it) |
| Asking an AI to summarise a game from video (capability gap) | Hypothesis, coach interviews | L | ignore (automatic video tagging is out of scope) |
| Checking competitors' pricing before renewing (pricing gap) | Hypothesis, sales calls | L | ignore (price position is the answer) |

**Total tools found:** 6
**Tools after triage:** 2 build candidates
**Estimated hidden spend:** unknown (placeholder €0, to be filled after coach interviews)
