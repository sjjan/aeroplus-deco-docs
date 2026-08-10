# Bailout planning

On a closed-circuit rebreather, **bailout** is the open-circuit gas you breathe if the loop becomes untrustworthy — a flooded scrubber, a controller failure, a hypoxic or hyperoxic loop, anything that means you can no longer breathe the unit. From that moment you are an open-circuit diver, and you must still complete your full decompression obligation on the gas you carry.

AeroPlus Deco plans for exactly that. When you bail out at the deepest point of the dive, it **recomputes the whole decompression schedule on open circuit** using your bailout gases, and tells you whether what you're carrying is enough to reach the surface.

!!! warning "Why this is its own calculation"
    The decompression you owe on open circuit is **not** the same as the loop schedule. On the loop you breathe an optimal high-PPO₂ mix at every stop, so you off-gas quickly. On open circuit you breathe fixed cylinder mixes, the inert load is higher, and the obligation grows. Reusing the loop TTS for bailout would **understate** the gas and time you actually need. AeroPlus Deco re-runs the plan on the bailout gas instead — so the bailout numbers are usually longer and gassier than the loop figures, and that is correct.

## Bailout mode

In the **Closed Circuit Setup** card, **Bailout** can be set to:

| Mode | Meaning |
|---|---|
| **Independent** | Every diver carries enough open-circuit gas to self-rescue from the worst point of the dive. AeroPlus Deco builds a full open-circuit bailout decompression schedule for this case. |
| **Group / team** | The team shares bailout, so a single diver's cylinders need not cover the entire obligation alone. The detailed per-diver OC schedule is not assumed in this mode. |

The bailout decompression schedule described on this page is produced in **independent** mode — the standard, most conservative assumption.

## Using the diluent as bailout

A common minimal-bailout setup (Halcyon Symbios and similar) is to breathe the **diluent open-circuit** through the bailout valve as your deep bailout gas. Enable this with:

> ☑ **Use diluent as an open-circuit bailout gas**

When ticked, AeroPlus Deco adds your diluent to the bailout gas pool and breathes it open-circuit — no setpoint, no oxygen boost, just the raw diluent mix at depth. A **descent reserve** (default 50 bar) is held back, since the diluent has already done work keeping the loop topped up on the way down.

Because the diluent is usually your *leanest* (most hypoxic) gas, the plan starts the bailout on the diluent at maximum depth and switches to richer carried gases as you ascend — the natural open-circuit progression.

## The bailout decompression schedule

The schedule is shown as an open-circuit stop table, in the same runtime-based format as the main deco plan:

```
→   75.0   19 min   +2     18/60 (dil)
↗   36.0   22 min   +3     18/60 (dil)
→   36.0   24 min   +2     18/60 (dil)
⊙   33.0   26 min   +2     ⊙ 16/58
→   30.0   28 min   +2     16/58
 …
⊙   21.0   34 min   +2     ⊙ 50/0
→   18.0   36 min   +2     50/0
 …
⊙    6.0   52 min   +2     ⊙ 100/0
→    6.0   60 min   +8     100/0
→    3.0   78 min   +18    100/0
↗    0.0   78 min   +0     100/0
```

| Column | Meaning |
|---|---|
| **Arrow** | Ascent (↗), stop (→), or a gas switch (⊙) |
| **Depth** | Stop depth in metres |
| **Runtime** | Cumulative runtime, continuing from the dive — it starts at the dive's bottom-phase runtime at the moment of bailout, not from zero |
| **Duration** | Whole-minute time on that row, with any folded 3 m ascent included |
| **Gas** | The bailout gas being breathed; `(dil)` marks the diluent |

A few things about how the table reads:

- **The runtime continues from the dive.** Bailout is assumed from the most critical point — the end of the bottom phase, just before ascent — so the Runtime column begins at that dive runtime rather than restarting at zero. The total bailout TTS (time from bailout to the surface) is shown in the summary line directly below the table.
- **3 m ascents are folded in.** A single 3 m step between stops is only a few seconds, so it isn't drawn as its own line — its time is rolled into the next stop's duration. A larger gap (where intermediate levels were skipped) keeps its own ascent (↗) line, and the first ascent to the first stop and the final ascent to the surface are always shown.
- **Durations are whole minutes**, derived from the rounded runtimes, so they always sum to the runtime without drift.

### Gas switches cost time

Every ⊙ row is a real open-circuit gas switch and is charged your configured **Gas switch time** — the pause while you change regulators and confirm the new gas. That pause is added to the runtime and to the gas required, exactly as it would be in the water.

This includes the **diluent → carried-gas handoff**. When you are bailed out on the diluent and its usable volume runs out, the plan switches you to the next carried gas that is still breathable at that depth. AeroPlus Deco models this as a genuine ⊙ switch at the handoff depth, with the switch time and switch gas accounted for — not as a free, instant change.

## Bailout TTS vs maximum loop TTS

Two different time-to-surface figures appear for a CCR plan, and they answer different questions:

- **Bailout TTS** — how long it takes to surface **on open circuit** if you bail out now. This is the headline figure on the bailout card.
- **Maximum loop TTS** — the bailout-limited ceiling for staying **on the loop**, shown under the ascent trigger. Oxygen and scrubber are not modelled, so bailout gas is the only consumable that bounds it. See [maximum TTS on CCR](oxygen-and-scrubber.md#maximum-tts-on-ccr).

They are deliberately separate: one is your escape plan, the other is your loop endurance.

## Is your bailout enough?

Beneath the schedule, AeroPlus Deco compares what the bailout obligation needs against what you carry:

> ✓ Bailout sufficient: 7015 ℓ available, 3702 ℓ required

- **Required** — total open-circuit volume to surface from the worst point, at the **emergency SAC** rate, including every gas-switch pause.
- **Available** — usable volume across your bailout cylinders (and the diluent, less its descent reserve, if diluent-bailout is on).

If required exceeds available, the banner turns **red** — carry more bailout, a larger cylinder, or shorten/shallow the dive.

Each bailout cylinder is also drawn as a standard gas bar (used / reserve / unused against a 0-to-fill scale), so you can see at a glance which bottle does the work and where the margin is. See [reading the output](../planning/reading-the-output.md) for the bar conventions.

## Surface and hypoxic-gas warnings

Bailout gas only helps if you can breathe it:

- **Nothing breathable at the surface** — if even your richest bailout gas has a PPO₂ below the hypoxic floor (default 0.16) at 0 m, the plan flags it in red. You would need a richer gas to safely breathe at and just below the surface.
- **Hypoxic diluent** — if the diluent (used as bailout) is too lean to breathe shallow, the plan notes the approximate depth above which it is no longer safe, so you know you must already be on a richer gas by then.

This mirrors the **Diluent PPO₂** column in the runtime schedule — see [setpoints](setpoints.md#reading-setpoints-in-the-output).

## Where to find it in the app

In CCR mode the bailout content sits at the **bottom of the plan output**, in its own card (titled **Bailout**), below the gas plan and ascent trigger. The full bailout schedule, the sufficiency banner, the per-cylinder bars, and any warnings are all there. The schedule is also included in the **print / PDF report**.

## Settings that feed the calculation

| Setting | Role in bailout |
|---|---|
| **Gas usage emergency** (emergency SAC) | Consumption rate for the whole bailout ascent |
| **Bailout switch time** | The initial pause as you come off the loop onto OC bailout |
| **Gas switch time** | The pause at every subsequent OC gas switch, including the diluent handoff |
| **Max deco PPO₂** | The depth at which each richer gas becomes usable |
| **Ascent speed** | Rate between stops |
| **Min surface PPO₂** | The hypoxic floor used for the surface-breathability check |

## Caveats and limitations

!!! warning "Cross-check before you rely on it"
    The bailout schedule is a planning aid, not gospel. **Confirm every bailout plan against a trusted desktop planner** (e.g. MultiDeco) before relying on it in the water. The in-app figures are conservative and agree well in testing, but you are responsible for the plan you dive.

- **Volume handoff is a proxy.** The depth at which the diluent hands off to a carried gas is apportioned from the diluent's usable volume, not from a second independent decompression run. It is a sound estimate of *where* you'll switch, not a re-solved stop schedule.
- **Stop lengths aren't re-timed for the switch minute.** The gas-switch pause is added to TTS and to gas required, but individual stop durations are not recomputed for the small extra time spent at the switch depth. The effect on the obligation is negligible.
- **It assumes you execute perfectly.** The numbers assume you bail at the planned worst point, breathe at the emergency SAC, ascend at exactly the set rate, and hit every stop. Real emergencies are messier and real consumption is usually higher — plan conservatively.
- **Single failure from max depth.** Like rock bottom, the model covers one loop failure at the deepest point. Cascading problems need more margin.

## Practical tips

- **Carry a useful deep bailout.** A very lean deep mix (e.g. 16/58) breathed open-circuit produces enormous, impractical shallow stops — it is a poor standalone bailout. Make sure your bailout progression includes gases rich enough to clear the obligation in sensible time.
- **Watch the first switch depth.** If your only breathable shallow gas comes on late, your deep bailout has to carry more of the dive — check the required-vs-available margin.
- **Re-check after any change.** Changing depth, bottom time, diluent, or bailout fill re-runs the schedule. Glance at the sufficiency banner each time.

!!! note "Open circuit is the fallback, not the plan"
    Sufficient bailout means you can probably get out if the loop fails — it does not make the loop failure safe. Train your bailout drills, keep your gas analysed and labelled, and treat the schedule as the minimum you must beat, not the target you aim for.
