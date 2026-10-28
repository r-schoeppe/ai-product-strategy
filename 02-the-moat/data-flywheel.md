# Data Flywheel Map

> Score each loop 1-5. Your weakest loop is where competitors attack first.
> The four loops below are the M2 starting point - adapt if your product has 2 or 6 loops instead of 4.

## Flywheel Loops

| Loop | What It Measures | Score 1 | Score 5 | Score |
|------|------------------|---------|---------|-------|
| **Correction** | Do users fix AI outputs? Is that signal captured and reused? | No capture | Automated retraining | 1/5 |
| **Preference** | Does the product learn individual / team preferences over time? | Stateless | Deep personalization | 1/5 |
| **Domain Context** | Does usage in one area improve quality in adjacent areas? | Siloed | Cross-domain transfer | 2/5 |
| **Network** | Does each new user / team make the product better for everyone? | Isolated | Strong network effects | 1/5 |

### Correction Loop - 1/5
**What you capture today:** Nothing from the coach. The report is computed from tagged plays and displayed; there is no way to mark a tell or a tag as wrong. Manual tagging is data entry, not correction of an AI output.
**How it compounds:** It does not. A wrong tell is shown again next week with the same ranking.

### Preference Loop - 1/5
**What you capture today:** Nothing per coach or team. Every coach who picks the same opponent sees the same report in the same order. The product does not track which tells are read, pinned or ignored. Stored team tags and games are team data, not learned preference.
**How it compounds:** It does not. A coach gets the same experience in month six as on day one, so taste creates no switching cost.

### Domain Context Loop - 2/5
**What you capture today:** A shared tag vocabulary (formation, situation, call, result, defence). One set of tagged plays feeds every section of the report, and each extra tagged game sharpens the report for that same opponent.
**How it compounds:** Only within one opponent, and linearly. Tagging one opponent does nothing for another, and no general flag-football pattern is learned across teams.

### Network Loop - 1/5
**What you capture today:** Nothing across teams. Tags, games and reports are scoped to one team (row-level security), and users belong to a single team. Players seeing the manager's tags is collaboration inside a team, not a network effect.
**How it compounds:** It does not. Ten teams on TapeMine are ten separate products.

**Total Flywheel Score: 5/20**
**Weakest Loop:** Correction (tied with Preference and Network at 1/5; Correction is the module's central test and the cheapest to build)
**Fix for weakest loop:** Keep what coaches change in the AI output (retagged plays, tells they reject) and use it to re-rank tells for that team and to tune the tag suggestions. This is the one loop a competitor with only films and annotations cannot copy quickly, because it needs TapeMine's own corrections history.

---

## Encroachment Threat Assessment

### 1. Platform Encroachment
**Attacker:** Google (Gemini video understanding); OpenAI is the alternative.
**Vector:** A coach uploads an opponent's clips to a general video model and asks for tendencies, with no TapeMine account. The platform never has to ship a flag football feature, only make video analysis good and cheap enough.
**Time-to-threat:** A rough version exists now; a version coaches prefer over TapeMine in 6-12 months.
**% of value at risk:** 20%. Running raw video through a model for every opponent is comparatively costly, while coach-made tags are a cheap, accurate input. The gap will shrink as model prices fall.

### 2. Vertical Competitor
**Attacker:** Hudl (Assist, and Hudl IQ at pro level). It is the tackle football incumbent.
**Vector:** Assist already generates tendency analysis from tagged film. Hudl lists formation, backfield and series data as 11-man only today, so 5-on-5 is its gap. With flag football becoming an Olympic sport, extending its pipeline to flag is now worth the work, and it can move fast.
**Time-to-threat:** 6-12 months.
**% of value at risk:** 70%. Hudl has the tagging pipeline, a very large labelled film library and a huge coach base. Vendor claims, not independently tested.

### 3. Adjacent Expansion
**Attacker:** WatchGameFilm (Hudl is also possible).
**Vector:** It already has the video plays and the annotation workflow, and it auto-cuts full games into plays. It only has to add a scouting summary on top, with high probability.
**Distribution advantage:** Coaches already upload film and pay, and it takes feeds from Veo cameras and Hudl links.
**Time-to-threat:** 3-6 months.
**% of value at risk:** 60%. These percentages overlap and cannot be added: Hudl and WatchGameFilm both attack the same AI report.

---

## 90-Day Encroachment Plan

*Your partner played the Big Tech attacker. What was their plan to kill you?*

**Attacker:** WatchGameFilm, Head of Product. (Played by Claude as the partner.)
**Attack vector (target the weakest loop):** TapeMine's Correction, Preference and Network loops are all at 1/5, so it is stateless and every team stays isolated. WatchGameFilm already has the plays, the annotation and the coach accounts. It adds a scouting summary on top and wins on its existing film, annotation and coach accounts, not on better AI.
**Weeks 1-4 - what they ship:**
- "Scout this opponent": one button on any film a coach has already annotated, giving tendencies by down and distance, formation and call, in the same layout coaches already read.
- Flag football presets: 5-on-5 formations and situations (including PAT) preloaded so no setup is needed.
- A simple free tier of the summary so every existing coach tries it without a purchase decision.
**Weeks 5-8 - how they poach users:**
- An importer for TapeMine's tags and clips (it already takes Hudl links and cloud transfers), plus 90 free days for any team that brings its season over.
- Coaches keep their own annotation workflow, so the summary arrives without any retraining.
**Weeks 9-12 - why users don't return:**
- Film, annotation and scouting all sit in one place, so going back to TapeMine means moving a season of film.
- Their coach has no reason to leave: the same tool does film, breakdown and scouting.
**Your defense:** Out-specialise on 5-on-5 flag football, stay far cheaper than the competition for amateur teams (the core value proposition at the moment), and win on usability and performance. Usability and speed were WatchGameFilm's weak point, and Hudl is too expensive for this niche.
