# Cylinders & gases

The **Gas & cylinders** card holds every gas the algorithm can use. Each cylinder has a role, a mix, a physical size, and a fill pressure.

## Adding a cylinder

Tap **+ Add** in the Gas & cylinders card. The modal opens with **Bottom gas** selected by default.

### Fields

| Field | What it controls |
|---|---|
| **Role** | How the algorithm uses the cylinder — see roles below |
| **O₂ %** | Oxygen fraction, 0–100 |
| **He %** | Helium fraction, 0–95 |
| **Size (ℓ)** | Cylinder internal volume in litres (e.g. 12.0 for a steel 12, 11.1 for an AL80) |
| **Fill (bar)** | Starting pressure |

The mix is shown as `O₂/He` (e.g. `21/0` for air, `50/0` for EAN50, `16/58` for 16/58 trimix). Nitrogen is computed as `100 − O₂ − He`.

## Roles

A cylinder's role tells the algorithm when (and whether) to use it.

### Bottom gas

The gas you breathe during the deepest portion of the dive. Used until the deeper deco gas becomes breathable on ascent.

- **Multiple bottom gases** are allowed — the algorithm will choose the richest one within PPO₂ limits at each depth
- Used for **rock-bottom reserve** calculation (the others are not)

### Travel gas

An intermediate mix used to bridge the gap when your bottom gas is hypoxic at shallow depths. Typical example: 21/35 trimix to descend through the 0–30 m range before switching to a hypoxic 16/58.

- Has a small reserve (configurable, default 50 bar)
- Counts as an ascent-switch gas for Auto-set GF Low

### Deco gas

A rich nitrox or oxygen mix used during decompression. Examples: 50/0, 80/0, 100/0.

- The algorithm switches to the richest available deco gas as soon as its MOD is reached on ascent
- Multiple deco gases stack — the algorithm progressively switches as MODs become available
- Must be **switched on** (checkbox ✓) to be used
- Counts as an ascent-switch gas for Auto-set GF Low

### Bailout (CCR only)

OC gas carried in case of rebreather failure. Not used by the deco algorithm in normal CCR operation — only displayed for reference and gas-sufficiency checks.

### Oxygen (CCR only)

Pure O₂ in the rebreather's O₂ cylinder, used by the loop for setpoint maintenance. Tracked for O₂ consumption and remaining duration.

## Enabling / disabling gases

Each non-bottom cylinder has a checkbox. Only **checked** gases are considered by the algorithm. Use this to:

- Temporarily disable a deco gas to see how the plan changes without it
- Run "what-if" scenarios for missing gas at the dive site
- Compare CCR bailout sufficiency with different mixes available

Bottom gases are always considered (the dive can't happen without them).

## Editing a cylinder

Tap the cylinder row to re-open the editor. Save updates the existing entry.

## Deleting

Tap the trash icon. If a dive segment references this cylinder, the segment is **auto-healed** on the next render — it gets reassigned to the first available bottom gas, and the deco recalculation triggers automatically.

## Practical recommendations

### Typical tech dive (40–60 m, OC)

| Role | Mix | Size | Fill |
|---|---|---|---|
| Bottom | 21/0 (air) or 30/30 (mod-trimix for narcosis) | 2 × 12 ℓ | 200 bar |
| Deco | 50/0 | 11 ℓ | 232 bar |
| Deco | 100/0 (optional) | 5.5 ℓ | 200 bar |

### Heavy trimix (75 m+)

| Role | Mix | Size | Fill |
|---|---|---|---|
| Bottom | 16/58 (or similar hypoxic trimix) | 2 × 16 ℓ | 270 bar |
| Travel | 21/35 | 11 ℓ | 232 bar |
| Deco | 50/0 | 11 ℓ | 232 bar |
| Deco | 100/0 | 5.5 ℓ | 232 bar |

The travel gas is what lets you set GF Low low enough to do a meaningful first deco stop without back-gas deep stops — see the [Andy Davis method](../concepts/andy-davis-method.md).

### CCR

| Role | Mix | Size | Fill |
|---|---|---|---|
| Diluent (bottom) | 18/45 trimix or 21/0 — matched to depth | 3 ℓ | 232 bar |
| Oxygen | 100/0 | 3 ℓ | 200 bar |
| Bailout | 21/35 + 50/0 + 100/0 (independent bailout) | varies | 232 bar |

The diluent's MOD limits your CCR maximum depth (loop PPO₂ at high setpoint must stay ≤ 1.6 even on diluent flush).

## Gas density check

After saving cylinders, the **Limits** table in the Gas plan card shows gas density at the deepest segment depth. If any value goes over 5.2 g/ℓ (orange) or 6.2 g/ℓ (red), use the [Best mix calculator](../tools/best-mix.md) to derive an appropriately heliumed mix.
