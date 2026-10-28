# Kill Switch Audit

Scope: the Scout AI feature (scouting summary), in its ideation state with OpenAI as the working choice. Nothing is built yet, so these ratings hold only while no provider-specific code exists.

## Vendor Dependency Assessment

| Dimension | Current State | Risk Level | 48-Hour Action |
|-----------|--------------|------------|---------------|
| **Provider** | Ideation. OpenAI is the working choice; no code exists yet. | L | Select any other provider. |
| **Abstraction** | No AI code yet, so no direct provider calls. The feature can be abstracted easily. | L | Use a model-agnostic package when integrating. |
| **Routing** | None. One task (write a report from tagged plays), run on demand. The tendencies are computed from tags by ordinary code; the model only writes them up. | L | Configure a second model as automatic fallback in the same package, and keep the last generated report per opponent so a coach sees something during an outage. |
| **Eval** | Only a few examples used to choose the first default model. No test set and no coach feedback. | H | Build a test set, and start collecting simple coach feedback. |

## Portability Score
**Partial.** Three of four dimensions are easy, but without an eval there is no proof a new model is good enough to switch to in 48 hours. Fixing Eval would move this to Ready.

## If OpenAI doubles pricing tomorrow:
Low impact, because Scout is a small, on-demand text task and the numbers come from ordinary code. Within 48 hours: switch the default model in the model-agnostic package, run the test set (once it exists) to confirm the report is still correct, and cache each opponent's report so it is only regenerated when new tags are added.

## If OpenAI ships a competing product:
The AI summary on its own is not defensible, since a general model can write one from video or tags. What they cannot replicate quickly: the 5-on-5 flag football specialisation (taxonomy, situations, report layout), the coach-made tags and team film library, a price built for amateur teams, and usability for this niche. This matches the 20% platform-risk estimate in `data-flywheel.md`.
