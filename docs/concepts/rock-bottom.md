# Rock bottom

**Rock bottom** (also called *minimum gas*) is the amount of bottom gas you must hold in reserve to support **two divers** ascending safely to the surface from the deepest point of the dive in an emergency — even if one of them has lost their primary supply.

It's the gas planning concept that distinguishes "I have enough gas to do this dive" from "I have enough gas to do this dive *and* still get out alive if something breaks."

## What goes into the calculation

For each bottom-gas cylinder, AeroPlus Deco computes rock bottom as:

```
rb = (descent + bottom hold + ascent to first deco gas + gas switch pause)
     × emergency SAC × 2 divers / cylinder size
```

In plain language:

1. Start at the deepest depth (with a 1-minute hold for problem assessment)
2. Ascend at the emergency ascent rate
3. Continue on bottom gas until the first deco gas can be used (its MOD)
4. Include the gas switch pause (deco gas onset)
5. Apply a doubled SAC rate — emergency consumption is higher and you're supporting a buddy
6. Convert litres to bar using the cylinder's size

The result is a **per-cylinder bar pressure** that must remain at the end of the dive.

## Where to find it in the app

In the **Rock bottom & TTS card** at the bottom of the plan output:

| Cylinder | Reserve |
|---|---|
| 16/58 | 163 bar |
| 50/0 | — |
| 100/0 | — |

Only **bottom-gas** cylinders get a reserve — deco gases are short-duration and you switch off them quickly. Travel gases get a smaller calculated reserve (configurable as **Travel gas reserve** in settings, default 50 bar) since they're emergency-relevant but consumed faster.

## Reading the gas plan bars

In the **Gas plan card**, each cylinder is drawn as a stacked bar:

| Segment | Meaning |
|---|---|
| **Blue (Used)** | Gas actually consumed during the planned dive |
| **Red (Reserve)** | Rock-bottom reserve preserved in the cylinder after the dive |
| **Grey (Unused)** | Surplus beyond used + reserve |

The three segments together equal the cylinder fill. If the **red Reserve** segment is smaller than the rock-bottom requirement shown in the Rock bottom card, **the dive ate into the reserve** — your plan doesn't carry enough gas. Increase fill, larger cylinder, or shorten the dive.

## Adjustable inputs

The rock bottom calculation pulls from several Settings values:

- **Gas usage emergency** (SAC during emergency, default 30 ℓ/min) — used as the per-diver consumption rate
- **Gas usage** (normal SAC) — used for the planned dive consumption (not rock-bottom)
- **Ascent speed** — emergency ascent rate
- **Gas switch time** — pause duration on the bottom gas before transitioning to deco gas
- **Max deco PPO₂** — determines the depth at which the first deco gas becomes breathable

## Caveats and limitations

- **Two-diver assumption** — the standard tech-diving model. Solo divers can halve the requirement, but most tech curricula teach the two-diver standard regardless of buddy presence on the day.
- **Single failure** — the calculation assumes one out-of-gas event from max depth. Multiple cascading failures would require more reserve.
- **No buoyancy correction** — assumes neutral buoyancy throughout the emergency ascent.
- **Bottom-segment hold** — the model assumes a brief stabilisation pause at max depth, not a full problem-solving cycle. For complex environments (wreck penetration, cave) you may want a larger personal reserve on top.

## Practical tips

- **Plan to use 1/3 of bottom gas** — a common rule that approximates rock-bottom plus contingency for non-emergency reasons (extended bottom time, missed deco gas).
- **If the bar shows no red Reserve segment** — your dive is overdrawing the cylinder; rethink the plan.
- **Cross-check between this card and the Limits table** — if both say you're tight on gas, you really are.

!!! warning "Rock bottom is the floor, not the ceiling"
    Just because you have rock bottom doesn't mean the dive is safe — it means you can probably extract yourself if everything else goes right. Plan additional margin for environmental factors, equipment quirks, and your own fatigue level.
