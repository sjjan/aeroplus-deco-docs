# Reading the output

After you tap **Calculate dive plan**, the app produces a stack of cards covering every aspect of the planned dive. This page walks through each one.

## Top-line metrics

The header strip shows six numbers at a glance:

| Metric | Meaning |
|---|---|
| **Max depth** | Deepest point of the dive |
| **Avg depth** | Average depth across the entire dive (descent + bottom + ascent + deco) |
| **Run time** | Total dive duration, surface to surface |
| **TTS** | Time to surface from the start of the ascent ([details](../concepts/tts-and-deco-stops.md)) |
| **CNS** | Cumulative CNS oxygen toxicity percentage |
| **OTU** | Cumulative oxygen tolerance units |

Any value that exceeds a recommended limit becomes a red warning in the **Critical warnings** banner at the top.

## Critical warnings

If the plan has problems, a banner appears between the metrics and the charts. Common warnings:

- **Gas density above 5.2 g/ℓ** — switch to a more helium-rich mix
- **Gas density above 6.2 g/ℓ** — *hard limit exceeded*; do not dive this profile
- **Gas shortfall** — total used gas exceeds cylinder fill
- **Rock bottom IMPOSSIBLE** — the required reserve is larger than the cylinder
- **CNS approaching limit**
- **PPO₂ exceeds maximum at depth** — bottom gas is too rich for max depth
- **Hypoxic at surface** — bottom gas can't be safely breathed at shallow depths

Any red warning is a sign that something is structurally wrong with the plan. Yellow warnings are advisory.

## Deco plan card

### Total deco time

The sum of all decompression stop durations. Doesn't include ascent time between stops or the final ascent.

### TTS at ascent start

TTS measured at the moment you leave the deepest planned segment.

### Deepest ceiling

The deepest depth at which the leading tissue compartment reaches GF Lo on direct ascent. The first deco stop will be at or just shallower than this.

### Dive profile chart

A graphical depth-vs-time plot:

- **Blue line** — actual depth profile
- **Solid red line** — GF ceiling (the deepest you can be without exceeding GF Lo, evolving as tissues off-gas)
- **Dashed faded-red line** — M-value (raw Bühlmann ceiling, GF Hi = 100)
- **Dashed grey line** — average depth

The shape of the dive narrative is visible at a glance: descent slope, bottom hold, stepped ascent through stops, and the gradient between the depth line and ceiling line — that gap is your safety margin.

### GF99 chart

Tissue saturation as the dive progresses:

- **Green areas** — off-gassing (positive GF99)
- **Red areas** — on-gassing (negative GF99)
- **Solid green line** — GF99 over time
- **Blue dashed line** — target GF99 (= GF Hi / 2)
- **Red dashed line** — GF Hi limit

See [Tissue saturation & GF99](../concepts/tissue-saturation.md) for what each curve means.

### Runtime schedule

The detailed minute-by-minute plan as a table. See [TTS & deco stops](../concepts/tts-and-deco-stops.md) for symbol meanings and row interpretation.

Each row gives:

- **Symbol** — ↘ ↗ → ⊙ (descending, ascending, holding, gas switch)
- **Depth** (m)
- **Runtime** — total elapsed time
- **Duration** — segment duration (`+` prefix)
- **Gas** (OC) or **Loop SP / Dil PPO₂** (CCR)

Deco stop rows are tinted **light green**. Gas-switch marker rows are tinted **light blue**.

## Gas plan card

### Bar chart

One horizontal bar per cylinder showing:

- **Blue (Used)** — gas consumed during the planned dive (matches the "Used (bar)" column in the table below)
- **Red (Reserve)** — rock-bottom reserve still preserved in the cylinder
- **Grey (Unused)** — surplus beyond the reserve

If a cylinder's Red segment is smaller than its rock-bottom requirement, the dive overdraws the reserve — increase fill, larger cylinder, or reduce dive time.

### Cylinders table

| Column | Meaning |
|---|---|
| No. | Position in the cylinder list |
| Mix | O₂/He |
| Size (ℓ) | Cylinder volume |
| Usage (bar) | Fill → remaining (used) |
| Used (ℓ) | Total litres consumed |

### Limits table

For each gas, the depth where it's breathed and the corresponding density, EAD/PPO₂, and warning levels:

| Depth | Mix | Density | PPO₂ |
|---|---|---|---|
| 75 m | 16/58 | 5.14 g/ℓ | 1.34 |

Density coloring: green/black ≤ 5.2, orange 5.2–6.2, red > 6.2.

## Rock bottom & TTS card

### Rock bottom reserves

One per bottom and travel gas cylinder. Shows the minimum bar pressure that must remain at the end of the dive — see [Rock bottom](../concepts/rock-bottom.md).

### Ascent trigger

A target TTS field you can fill in for your reference: "Start your ascent when *either* your dive computer shows TTS ≤ your target, *or* your gas reaches the minimum reserve — whichever comes first." Doesn't affect the calculation.

## Contingency plan toggles

The **Deeper +N m** and **Longer +N min** buttons at the top of the Deco plan card show a contingency profile:

- **Deeper +3 m** — re-runs the plan with all segments 3 m deeper (default; configurable in settings)
- **Longer +3 min** — re-runs with all bottom times 3 min longer (default; configurable)

The deco plan, gas usage, and warnings update for the contingency scenario. Useful for "what if I overshoot?" planning.

## CCR-specific additions

In CCR mode, the cards expand with rebreather-specific information:

- **Diluent PPO₂** in the runtime schedule
- **Loop density** in the Limits table
- **Oxygen used / remaining** in the Rock bottom & TTS card
- **Scrubber endurance** indicator
- **Bailout sufficiency check** (when independent bailout mode is set)

See [CCR overview](../ccr/index.md) for details.

## Sharing the calculated plan

Once a plan is calculated, the share menu lets you:

- **Copy a link** that opens the same plan in a buddy's browser
- **Generate a print-ready PDF** with the same charts and tables
- **Send a plain-text briefing** for Messages, email, or notes

See [Sharing & backup](sharing-and-backup.md).
