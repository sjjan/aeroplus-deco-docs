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

With more than one back gas enabled, this reserve is computed once and **pooled** across the cylinders rather than duplicated — see [Multiple back gases](#multiple-back-gases) below.

## Where to find it in the app

In the **Rock bottom & TTS card** at the bottom of the plan output:

| Cylinder | Reserve |
|---|---|
| 16/58 | 163 bar |
| 50/0 | — |
| 100/0 | — |

Only **bottom-gas** cylinders get a reserve — deco gases are short-duration and you switch off them quickly. Travel gases get a smaller calculated reserve (configurable as **Travel gas reserve** in settings, default 50 bar) since they're emergency-relevant but consumed faster.

## Maximum TTS and the ascent trigger

Two separate things tell you when to leave the bottom, and they are not the same number:

- **Planned TTS** — the time-to-surface of the runtime you entered. It's what your computer will show at your planned turn time.
- **Maximum TTS** — the time-to-surface you would face if you stayed down until your **back gas is drawn down to the rock-bottom reserve**, with your deco gas still sufficient. It's the latest TTS you could reach without eating into your reserve.

Because a typical plan surfaces with some unused back gas, the maximum TTS is **larger** than the planned TTS. It's shown directly under the **Target TTS** field:

> **Maximum TTS ≈ N min** — the longest your computer's TTS can reach before your back gas would hit the rock-bottom reserve (deco gas still sufficient). Turn at your target TTS for margin; never let TTS exceed this.

### How it's calculated

AeroPlus Deco doesn't estimate this from a single formula — it re-runs your **entire decompression plan** repeatedly, lengthening the last bottom segment a little more on each pass (a binary search), so every trial is a complete, valid schedule for that longer bottom time. At each trial, on open circuit, it checks two things:

1. **Back gas vs reserve** — your bottom-gas consumption hasn't dropped the cylinder below the rock-bottom reserve. The reserve is recomputed for each longer profile (though, being a direct ascent to your first deco gas, it barely changes with bottom time).
2. **Deco gas** — it **iterates through every enabled deco gas** and confirms none would run dry at the longer runtime, since more bottom time means more decompression and therefore more deco-gas demand.

It stops at the last bottom time that still passes both checks and reports the TTS there, never below your planned TTS. Whichever limit binds first (back gas reaching the reserve, or a deco gas running out) is named in the readout, and the **deco-gas demand at that maximum is shown per cylinder** against the planned figure, so you can confirm you're carrying enough.

### Using it

Plan and turn at your target/planned TTS, but know the maximum TTS is the hard ceiling set by gas. If you ever drift past your plan, that ceiling — not the planned number — is what keeps you out of your reserve. If you set a **Target TTS** above this maximum, the app flags it in red (it would draw into your reserve); a target between your planned and maximum TTS is allowed and shown as an amber advisory rather than an error.

!!! warning "Check your assumptions and plan conservatively"
    The reserve and the maximum TTS are computed from the values you entered, and they assume you **ascend at exactly the rate set in preferences and execute every decompression stop to the letter**. Double-check your normal and emergency SAC, your ascent rate and your deco settings, and plan conservatively — real-world consumption (cold, workload, stress) is often higher than planned, which pulls the maximum TTS down.

## Reading the gas plan bars

In the **Gas plan card**, each cylinder is drawn as a stacked bar:

| Segment | Meaning |
|---|---|
| **Blue (Used)** | Gas actually consumed during the planned dive |
| **Red (Reserve)** | Rock-bottom reserve preserved in the cylinder after the dive |
| **Grey (Unused)** | Surplus beyond used + reserve |

The three segments together equal the cylinder fill. If the **red Reserve** segment is smaller than the rock-bottom requirement shown in the Rock bottom card, **the dive ate into the reserve** — your plan doesn't carry enough gas. Increase fill, larger cylinder, or shorten the dive.

## Multiple back gases

You can enable **more than one bottom-gas cylinder** at once — for example a back-mounted twinset plus a stage of the same mix, or two cylinders filled a percent or two apart because the blend wasn't perfect. Tick each one in **Gas & cylinders**; the app always keeps at least one bottom gas enabled.

With several back gases enabled, AeroPlus Deco treats them as a single **interchangeable pool**:

- **Gas selection** — at each depth the algorithm breathes the richest enabled gas that's within PPO₂ limits.
- **One pooled reserve** — rock bottom is a single reserve *volume* (computed once, as above), not one per cylinder. It's placed on the **last-added** back cylinder first and spills back to earlier ones only if that cylinder can't hold it — counting only the gas left **after** planned consumption. That's why the reserve in the Gas plan card and the Rock bottom card always match, and why a cylinder you also breathe from carries less reserve than an untouched one.

!!! note "Interchangeable only holds for near-identical fills"
    Pooling assumes the gases are genuinely substitutable. If two enabled bottom gases differ by more than roughly **3 percentage points of O₂** or **5 of helium**, the plan shows a note — the mixes aren't really interchangeable, and the one you'd breathe at a different phase is probably a **travel** or **deco** gas. Set its role accordingly rather than leaving it as a second bottom gas. Large helium-to-nitrogen differences also make the [ICD](icd-and-hpns.md) note relevant on deep switches.

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
