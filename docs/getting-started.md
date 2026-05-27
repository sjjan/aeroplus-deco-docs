# Getting started

This page walks you through building your first dive plan in AeroPlus Deco — from a blank app to a complete runtime schedule.

## Open the app

Visit [sjjan.github.io/aeroplus-deco](https://sjjan.github.io/aeroplus-deco/) in any modern browser. Nothing to install yet — the app runs entirely in the browser.

The first time you open it, you'll see an empty **Plan 1** with the default settings: open-circuit mode, ZHL-16C-GF, GF 30/85, fresh water, sea level.

!!! tip "Install as a home-screen app"
    Once you're using AeroPlus Deco regularly, install it to your phone or laptop so it opens like a native app and works offline. See [Install as app](installing.md).

## Build a quick plan

We'll plan a typical recreational tech dive: **40 m for 20 minutes, on air with 50 % nitrox for deco**.

### Step 1 — Add your bottom gas

In the **Gas & cylinders** card, tap **+ Add**. The cylinder modal opens with **Bottom gas** selected. Enter:

| Field | Value |
|---|---|
| O₂ % | 21 |
| He % | 0 |
| Size (ℓ) | 12.0 |
| Fill (bar) | 200 |

Tap **Save cylinder**. Air (21/0) is now your bottom gas.

### Step 2 — Add your deco gas

Tap **+ Add** again. This time, select **Deco gas** at the top, then:

| Field | Value |
|---|---|
| O₂ % | 50 |
| He % | 0 |
| Size (ℓ) | 11.1 |
| Fill (bar) | 232 |

Tap **Save cylinder**. The deco gas appears in the list with a checked box — it will be used automatically when the algorithm reaches its MOD on ascent.

### Step 3 — Add a dive segment

In the **Dive profile** card, tap **+ Add**. Enter:

| Field | Value |
|---|---|
| Depth (m) | 40 |
| Bottom time (min) | 20 |

The **Gas** dropdown will already have your bottom gas selected. Tap **Save segment**.

### Step 4 — Calculate

Tap the big blue **Calculate dive plan** button.

In a fraction of a second, the **Deco plan** card appears with:

- A **dive profile chart** showing depth, GF ceiling, and average depth over time
- A **GF99 chart** showing tissue saturation through ascent
- A **runtime schedule** listing every depth-time-gas combination
- A **gas plan** showing per-cylinder usage and rock-bottom reserves
- **CNS / OTU** oxygen-exposure totals
- Any **warnings** at the top (e.g. gas density, gas shortfall)

## Reading the output at a glance

Three numbers tell you the most about the dive at a glance:

- **Total deco time** — sum of all stop durations
- **TTS at ascent start** — how long it'll take to surface from the deepest point
- **Deepest ceiling** — the deepest depth your tissues will tolerate (the first GF Low stop)

For a full walkthrough of every card and chart, see [Reading the output](planning/reading-the-output.md).

## What to do next

- **Tune your gradient factors.** Defaults are conservative. Read [Gradient factors](concepts/gradient-factors.md) and consider the [Andy Davis method](concepts/andy-davis-method.md) for setting GF Low on OC.
- **Plan a multi-level dive.** Add more segments below the first — each can be at a different depth. See [Dive profile](planning/dive-profile.md).
- **Save a contingency plan.** Toggle **Deeper +3 m** and **Longer +3 min** to see how the deco changes if you go over.
- **Share with a buddy.** Use the share menu to send a link your buddy can open in any browser without installing anything. See [Sharing & backup](planning/sharing-and-backup.md).

!!! warning "Cross-check, every time"
    No matter how clean a plan looks in the app, always verify it against a second source — another planning tool, a dive computer simulator, or your instructor. Decompression involves real risk and a single off-by-one in your gas mix or depth entry can move the plan into dangerous territory.
