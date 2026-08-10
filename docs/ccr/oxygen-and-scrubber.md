# Oxygen & scrubber

Your oxygen supply and your CO₂ scrubber are the two consumables that keep a rebreather running, and on a long dive either can end it. **AeroPlus Deco deliberately does not calculate or track them.** This page explains that decision, and what the app does bound instead.

!!! warning "Neither is modelled — monitor both in the water"
    AeroPlus Deco shows no O₂ consumption figure, no O₂ remaining duration, and no scrubber endurance countdown. Your handset and your own procedures are the authority on both. Plan your gas and absorbent duration with your unit's manufacturer figures and your training, not with this app.

## Why oxygen use is not calculated

Earlier versions estimated O₂ consumption from a metabolic rate plus setpoint-maintenance additions. That figure was removed on the advice of a CCR instructor trainer, for a straightforward reason: **it looked far more precise than it could possibly be.**

Real oxygen use on a rebreather is dominated by things the app cannot know:

- **Manual additions.** Loop volume changes constantly with depth, buoyancy adjustment, drysuit feeding from the O₂ or diluent supply, and diver habit. Manual O₂ shots routinely swamp metabolic consumption.
- **Flushes.** Diluent flushes, O₂ flushes for cell validation, and pre-breathe all consume gas that no profile-based model predicts.
- **Metabolic rate is personal and variable.** It swings with workload, thermal stress and fitness — easily a factor of three between a warm, relaxed diver and a cold, working one.
- **Leaks and solenoid behaviour** vary by unit and by day.

A number that is wrong by a factor of two is worse than no number, because divers trust displayed figures. The same reasoning removed the scrubber endurance countdown: a minutes-remaining readout computed from a nominal capacity invites you to dive to a number that depends on water temperature, work rate, CO₂ production, packing quality and absorbent age — none of which the app can observe.

This is a deliberate design principle in AeroPlus Deco: **where a calculated value would be trusted more than it deserves, it is not shown.**

## What you should do instead

- **Oxygen** — check your onboard O₂ pressure before the dive and monitor it throughout. Use your unit's guidance for the minimum you need for the planned runtime plus a real reserve. Treat the O₂ supply as a hard turn criterion in your dive plan.
- **Scrubber** — track absorbent duration yourself against the manufacturer's figure, derated for cold water and workload (many teams plan at 60–75 % of the rated duration). Log the elapsed time on each fill.
- **Record it on a checklist.** The bundled *Generic CCR — Assembly* checklist has a **Scrubber filled and seated** step with a field for the absorbent duration set for this fill, so the figure is captured with the build and stored in the saved run. See [Checklists](../planning/checklists.md).

## Maximum TTS on CCR

The app still reports a **maximum loop TTS** under the ascent trigger — the longest time-to-surface you could reach before you run out of something. On CCR the loop itself is not consumed, and neither oxygen nor scrubber is modelled, so **the only consumable that bounds it is your bailout gas**.

> **Maximum loop TTS ≈ N min** — the longest before your bailout would be exhausted. Turn at your target TTS for margin; never exceed this.

### How it's checked

Exactly as on open circuit, the app re-runs the full plan repeatedly, lengthening the last bottom segment a little more on each pass (a binary search), so every trial is a complete, valid schedule. At each trial it checks whether an open-circuit bailout from that point would still be covered by the gas you carry — see [Bailout planning](bailout-planning.md).

This check applies in **independent** bailout mode only. In **group** mode, bailout sufficiency is the team's responsibility and is not used as a limit, so no maximum loop TTS is bound by gas at all.

!!! warning "This is a bailout limit, not an endurance limit"
    The maximum loop TTS tells you when your **bailout** runs out. It says nothing about your oxygen supply or your scrubber, and either of those may well bind first on a long dive. It also assumes your emergency SAC is accurate and that you **ascend at exactly the rate set in preferences and execute every decompression stop to the letter**. Treat it as a ceiling, never a target, and keep your own O₂ and absorbent limits alongside it.

## Repetitive CCR diving

Tissue loading, CNS and OTU all carry across dives through the surface interval — see [Reading the output](../planning/reading-the-output.md). Oxygen and scrubber use do **not** carry across, because they are not tracked at all. Between dives in a series, manage both yourself:

1. Check and top up the onboard O₂; note the starting pressure.
2. Decide whether the absorbent has enough remaining duration for the next dive, or repack.
3. Record both on your pre-dive checklist so the decision is captured with the run.
