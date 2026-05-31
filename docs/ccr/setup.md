# CCR setup

## Activating CCR mode

In **Settings → CCR mode**, toggle the switch to on. The app does several things:

1. **Saves your OC cylinder configuration** so you can switch back
2. **Loads or creates CCR cylinders** — diluent, O₂, and a default bailout
3. **Shows the Closed Circuit Setup card** on the main plan page with setpoints, switch depth, and bailout mode
4. **Disables Auto-set GF Low** (the Andy Davis method doesn't apply to CCR — see the [method article](../concepts/andy-davis-method.md))
5. **Marks the result as stale** so you'll recalculate with the new mode

If CCR was previously configured for this plan, your saved cylinders and setpoints are restored. Otherwise, sensible defaults are created.

## Default CCR setup

If this is the first time you've enabled CCR for a plan, you get:

| Role | Default mix | Size | Fill |
|---|---|---|---|
| Diluent (bottom) | 18/60 hypoxic trimix | 3.0 ℓ | 232 bar |
| Oxygen | 100/0 | 3.0 ℓ | 200 bar |
| Bailout | 21/35 trimix | 11.1 ℓ | 232 bar |

These are starting points — adjust to your actual unit, mix, and bailout configuration.

## Cylinder roles in CCR

### Diluent

Has the **bottom** role in CCR. The diluent fills the loop above water and supplements during descent when the loop volume falls. Its mix determines:

- **Maximum depth** — the diluent's O₂ % limits CCR max depth (at any depth, the loop PPO₂ ≤ raw diluent PPO₂ × 1.0 = the diluent partial pressure during a flush)
- **Bailout EAD** — if you bail out to OC on the diluent, your immediate gas at that depth is the raw diluent
- **Loop density** — denser diluent means denser loop

The "best diluent" calculator can compute a diluent that satisfies both narcosis and density constraints at your max planned depth. Its oxygen fraction follows the **diluent O₂ strategy** you choose — a fixed 10 %, or one set so the diluent PPO₂ at depth is 1.0 ata — see the [Best mix calculator](../tools/best-mix.md).

### Oxygen

Pure O₂ (1.00 / 0). Used by the loop solenoid to maintain setpoint. The app tracks **O₂ used in litres** based on metabolic consumption and setpoint-driven flushes, and **remaining O₂ duration**.

You can adjust:

- **Cylinder size** (Settings → typically 1.5 or 3.0 ℓ for CCR)
- **Fill pressure** (typically 200 bar)
- **O₂ metabolic rate** (Settings → CCR section; default 1.5 ℓ/min STPD)

### Bailout

OC gas carried in case of a loop failure. The deco algorithm does **not** use bailout in normal operation — only displays it for reference and sufficiency-check purposes. Multiple bailout cylinders are common (e.g., 21/35 deeper, 50/0 mid, 100/0 final).

Bailout sufficiency is checked separately — see [Bailout planning](bailout-planning.md).

## CCR setup card on the main page

When CCR mode is active, a dedicated card appears between Cylinders and the Dive profile:

### Setpoints

Four input fields:

- **Surface SetPoint** — used surface → switch depth on descent, and from switch depth → surface on ascent (typical: 0.7)
- **SP switch depth** — depth at which descent switches from surface SP to bottom SP (typical: 20 m)
- **Bottom SetPoint** — used below the switch depth during the bottom phase (typical: 1.3)
- **Deco SetPoint** — used at all decompression stops (typical: 1.3 or 1.5)

A per-segment SP override is possible from the segment editor.

### Bailout mode

Two options:

- **Independent** — each diver carries enough bailout to ascend solo on OC from max depth. The app validates this.
- **Group** — bailout is the team's collective gas; sufficiency is the team's responsibility. The app **does not** validate group totals — that's a planning step done outside the app.

If you select **Group**, a warning banner reminds you that gas validation is your responsibility.

## Switching between OC and CCR

Each plan has both an OC and a CCR cylinder configuration, preserved separately:

- Switch OC → CCR — your OC cylinders are saved; CCR cylinders restored or initialized
- Switch CCR → OC — your CCR cylinders are saved; OC cylinders restored

This lets you compare the same dive on OC vs CCR easily. Switching does **not** auto-recalculate — you'll see "Press Calculate" until you re-trigger the algorithm.

## Settings specific to CCR

In **Settings → CCR**:

| Setting | Default | Range | What it controls |
|---|---|---|---|
| O₂ metabolic rate | 1.5 ℓ/min | 0.1–3.0 | Per-minute O₂ consumption (STPD) |
| Scrubber capacity | 180 min | 30–480 | Total scrubber endurance before replacement |
| Bailout switch time | 2 min | 0–5 | Mandatory pause when switching to bailout |
| Diluent O₂ from target PPO₂ | Off | On / Off | Best-diluent O₂ strategy. Off = fixed 10 %; on = diluent O₂ set so its PPO₂ at depth is 1.0 ata (≈ 9 % at 100 m) |

Plus the standard algorithm settings (GFs, ascent rates, stop interval) all still apply.
