# Oxygen & scrubber

CCR mode adds two consumable-tracking concerns that don't exist on OC: the oxygen cylinder feeding the loop, and the CO₂ scrubber. AeroPlus Deco tracks both.

## Oxygen consumption

### Metabolic O₂ rate

Your body consumes O₂ at a roughly constant rate (depending on workload). This is independent of depth — on a rebreather, you consume the same molecules per minute at 60 m as you do at 6 m.

**Settings → CCR → O₂ metabolic rate** (default 1.5 ℓ/min STPD). Typical ranges:

| Activity | Rate (ℓ/min STPD) |
|---|---|
| Resting, warm | 0.6–0.8 |
| Normal diving | 1.0–1.3 |
| Active diving (cold, work) | 1.5–2.0 |
| Heavy work | 2.0–3.0 |

Use the setting that matches your typical effort. Conservative is higher (1.5 is widely cited for tech CCR planning).

### Setpoint-driven flushes

Apart from metabolic consumption, the rebreather also adds O₂ to maintain setpoint during ascent (the loop gets richer as pressure decreases). This is calculated by the algorithm based on the setpoint and depth profile.

The total O₂ shown as **Used** in the gas plan reflects both metabolic and setpoint-maintenance consumption.

### Reading the output

In the **Gas plan card**, the oxygen cylinder gets its own bar:

- **Used** (blue) — total O₂ consumed during the planned dive
- **Reserve / Unused** (grey) — what remains in the cylinder after the dive

The cylinder's remaining duration (in min) at the current consumption rate is also displayed in the **Rock bottom & TTS card** under "**O₂ remaining**".

### Marking O₂ as refilled

In the **Plans bar** at the top of the app, an active plan can be marked as having had a fresh O₂ refill before the dive. This resets the O₂ tracking for repetitive dive sequences.

For a single dive, you don't need to do anything — the O₂ usage is just for that dive.

For a repetitive dive series:

1. Plan dive 1; calculate
2. Set surface interval (if applicable)
3. Add dive 2 (new plan tab); the app carries forward O₂ remaining from dive 1
4. If you refilled between dives, mark **O₂ refilled** in the new plan — this resets

## Scrubber endurance

### What the scrubber does

The rebreather's CO₂ scrubber removes carbon dioxide from the exhaled loop gas via a chemical absorbent (e.g. soda lime). Scrubber capacity is measured in minutes of CO₂ absorption at a typical breathing rate. As scrubbers age (per-dive use), their absorbing capacity drops; at some point you must repack.

### Settings

In **Settings → CCR → Scrubber capacity** (default 180 min, range 30–480):

The exact capacity depends on:

- **Scrubber size and type** — different units have different capacities
- **Water temperature** — cold water reduces capacity
- **Breathing rate** — heavier work draws CO₂ faster

Common values for tech-grade units: 120–180 min in warm water, 90–150 min in cold water.

### Tracking across dives

Each plan has a **Scrubber fresh** flag. When set:

- The scrubber is assumed to be at full capacity for this dive
- The current dive's duration is logged against capacity

When not set (a repetitive dive on the same scrubber):

- The previous dives' durations subtract from capacity
- The remaining capacity is what's left for this dive
- If the planned duration exceeds remaining capacity, a warning appears

### Reading the output

In the **Rock bottom & TTS card** (CCR mode):

- **Scrubber endurance** — total capacity (e.g. 180 min)
- **Used (prev dives)** — sum of durations from prior plans on the same scrubber
- **Used (this dive)** — planned dive duration
- **Remaining** — capacity minus all uses

A warning is raised if **Remaining** goes below a buffer (default: 10 min of margin).

## Maximum TTS on CCR

On a rebreather the diluent loop is **effectively unlimited** for normal diving, so the maximum TTS isn't set by back gas. Instead AeroPlus Deco extends your bottom time until the first of three consumables would be exhausted — **bailout gas, scrubber endurance, or onboard oxygen** (at your metabolic rate) — and reports the TTS at that point.

> **Maximum TTS ≈ N min** (shown at your bottom setpoint; it drops once you switch to the deco setpoint) — the longest before your bailout, scrubber or O₂ would be exhausted. Turn at your target TTS for margin; never exceed this.

### How it's checked

Exactly as on open circuit, the app re-runs the full plan repeatedly, lengthening the last bottom segment a little more on each pass (a binary search). At each trial it checks three consumables, all of which grow with a longer dive:

1. **Scrubber** — time already used plus this dive's total duration (bottom time *plus* the ascent and deco it implies) stays within scrubber capacity.
2. **Oxygen** — onboard O₂ consumed (metabolic plus setpoint maintenance) stays within what the cylinder holds, at your configured metabolic rate.
3. **Bailout** — *independent mode only* — your bailout still covers an open-circuit ascent from depth. In **group** bailout mode this is the dive team's responsibility and is **not** used as a limit, so only scrubber and oxygen bound the maximum there.

It stops at the last bottom time that passes all applicable checks and reports the TTS there (at your bottom setpoint), never below your planned TTS. The readout **names whichever consumable binds first**. The diluent loop itself is not a limit — it is recirculated, not consumed.

!!! warning "Check your rates and plan conservatively"
    The maximum TTS depends on your metabolic O₂ rate, your SAC (for bailout) and your scrubber assumptions, and it assumes you **ascend at exactly the rate set in preferences and execute every decompression stop to the letter**. Double-check all of these and plan conservatively — see [Conservative practice](#conservative-practice). Treat the maximum TTS as a ceiling, not a target.

## Practical patterns

### Single tech CCR dive

- Mark scrubber as fresh (default for new plan)
- Plan the dive
- Verify O₂ remaining is comfortable (typically 2–3× planned dive duration)

### Repetitive CCR diving

- Plan dive 1: scrubber fresh, calculate
- Plan dive 2 in a new tab: scrubber **not** fresh; carry forward from dive 1
  - If you refilled O₂, mark **O₂ refilled** = true for dive 2
- The app will track cumulative scrubber use across the series

### Replanning after repack

If you repack mid-trip:

1. Open the active plan
2. Toggle **Scrubber fresh** on
3. The scrubber count resets for subsequent plans built on this base

## Conservative practice

The scrubber capacity from the manufacturer is typically a "calm water, normal effort, single-diver" figure. For real-world tech ops, divers typically derate it by 25–40 %:

- Manufacturer's 180 min → planning at 120–135 min
- Manufacturer's 240 min → planning at 150–180 min

Set the scrubber capacity in settings to your planning value, not the manufacturer's number.

Same applies to O₂ consumption — use 1.5 ℓ/min metabolic for planning even if your real-world rate is 1.2 ℓ/min, just to keep a margin.
