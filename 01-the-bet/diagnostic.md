# Three-Axis Vulnerability Diagnostic

## Product

**Product:** TapeMine, a 5-on-5 flag football video-review platform. The AI hero feature is the scouting summary: an AI-generated overview of an opponent drawn from tagged play videos.
**Your Role:** Founder / product owner (TO CONFIRM)

> Draft status: scores are provisional, written from MVP.md and CLAUDE.md. The scouting summary's exact inputs and outputs are assumed, not confirmed. Revise once they are pinned down.

---

## Scores

### Contextual Moat — 2/5
*Workflow depth × switching cost. Would users leave in a weekend if a competitor showed up?*

**Score rationale:** A manager who has imported, ordered and tagged a season has some lock-in, and the game → play queue → tag workflow is more than a file viewer. But the video comes from the league as already-cut files that anyone can re-import, tags are plain JSON that could be exported, and watchlists (the stickiest feature) are not built yet. A team could move in a weekend. Teams are small and the user base is niche, so there is also no team-to-team network effect yet.

**Named attacker (from partner challenge):** Hudl, which already owns team video workflows and could add a flag football mode. TO VALIDATE with the partner challenge.

---

### Data Advantage — 2/5
*Proprietary signal that compounds with usage. What do you see that OpenAI doesn't?*

**Score rationale:** The tag set (offence, defence, result per play) is a labelled dataset for a sport general models barely cover, and that is a real edge. But it only compounds if the labels are volume and consistent: today they are entered by hand by managers, per team, with a flexible taxonomy, so quality will vary. Nothing yet shows that scouting summaries improve from usage or feed corrections back into the tags. Without that loop, the data is an asset but not a flywheel.

**Named attacker (from partner challenge):** A general multimodal model (OpenAI / Google) that tags plays from raw video, which would erase the manual labelling advantage. TO VALIDATE.

---

### Platform Exposure — 3/5
*Encroachment risk × pivot speed. If Apple/Google/OpenAI ships your hero feature native — then what?*

**Score rationale:** "Summarise this opponent from their clips" is a prompt on a video-capable model, so the summary on its own is the easiest part to copy and has no technical barrier. Exposure is moderated by niche size (too small for a platform to target) and by the dependency on league-supplied play files, which a platform cannot get. Pivot speed is good: Mux and Supabase sit behind service modules and the team is small. If the summary becomes a commodity, the fallback is the league-integrated workflow, not the AI.

**Named attacker (from partner challenge):** A general AI assistant with video upload, used directly by a coach. TO VALIDATE.

---

## Top Vulnerability
The AI scouting summary has no defensible moat on its own. Defensibility depends on the league relationship and on turning manual tags into a compounding data loop, and neither exists yet.

## Confidence Level
M. The product problem is real, but the scores rest on assumptions about the scouting summary and on unvalidated attackers.
