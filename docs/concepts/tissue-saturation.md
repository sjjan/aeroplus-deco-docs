# Tissue saturation & GF99

This page explains how the Bühlmann ZHL-16C model tracks dissolved inert gas in your body, what "M-value" means, and how to read the GF99 chart in the app.

## The 16-compartment model

Bühlmann's model imagines your body as a set of **hypothetical tissue compartments**, each with a different speed of absorbing and releasing inert gas (nitrogen and helium):

- **Fast compartments** (~2–10 minute half-times) — blood, brain, kidneys. They saturate quickly during the dive and release gas quickly on ascent.
- **Medium compartments** (~20–60 min) — muscles, organs.
- **Slow compartments** (~80–635 min) — fat, ligaments, joints, bone. They saturate slowly on a long dive but also off-gas slowly afterward.

ZHL-16C uses **16 compartments**, each with separate nitrogen and helium half-times. At every moment, the model computes how much dissolved inert gas each compartment holds, based on the gas you're breathing and the depth pressure.

## M-values

For each compartment at each depth, there's an **M-value** — the maximum tissue tension that compartment can hold without forming bubbles on direct ascent to the next stop. The M-value is depth-dependent (higher allowed at depth, lower near the surface).

Diving "right at the M-value" means using the entire available margin. Most divers want to stay well under it — hence gradient factors.

## GF99 — the dashboard number

**GF99** is the live percentage of M-value currently being used by the leading (most-saturated) compartment.

- **GF99 = 0 %** — your tissues match ambient pressure; you're at equilibrium.
- **GF99 = negative** — you're **on-gassing**; pressure is higher than tissue tension, so gas is flowing in.
- **GF99 = positive** — you're **off-gassing**; tissue tension exceeds ambient pressure, so gas is flowing out.
- **GF99 > GF Hi** — you've exceeded your chosen ceiling; mandatory stop.
- **GF99 = 100 %** — raw Bühlmann limit; bubbling likely.

A useful target during deco stops is **GF99 ≈ GF Hi / 2** (e.g. 42 % when running GF Hi = 85). That's roughly the "half-way decompressing" point — efficient but not panicky.

## The GF99 chart

In the Deco plan card, below the depth profile, the **GF99 chart** shows tissue saturation across the dive:

- **Green areas** — off-gassing (positive GF99); you're decompressing
- **Red areas** — on-gassing (negative GF99); gas flowing into tissues
- **Solid green line** — GF99 over time
- **Blue dashed line** — target GF99 (= GF Hi / 2)
- **Red dashed line** — GF Hi limit (the surface ceiling)

A well-shaped ascent has GF99 rising into the green zone shortly after leaving the bottom, hovering near the target during stops, and approaching GF Hi just before surface.

## Deepest ceiling

The **deepest ceiling** value at the top of the Deco plan card is the deepest depth your tissue compartment ceilings allow. It's the depth where GF Lo is reached on the leading compartment — the first decompression stop in raw model terms. Stop intervals (e.g. 3 m) snap it to a valid stop depth.

## Practical consequences

- **Faster ascent rates** raise GF99 sharply during the ascent itself. AeroPlus Deco models ascent at 10 m/min by default (configurable in Settings → Ascent speed) and 3 m/min between deco stops (Settings → Deco ascent speed).
- **Slower ascent** keeps the GF99 curve smoother but adds runtime.
- **Skipping a stop** spikes GF99 above GF Hi — this is what dive computers warn about as "ceiling violation."

## Why the model can be wrong

Bühlmann is dissolved-gas only — it assumes inert gas stays dissolved unless it bubbles outright. Reality includes silent micro-bubbles, venous gas emboli (VGE), and tissue-specific factors no model captures. The GF system is one way to add a margin; another is post-dive Doppler monitoring (which most divers never do). Always treat the planner's output as a *plan*, not a guarantee.
