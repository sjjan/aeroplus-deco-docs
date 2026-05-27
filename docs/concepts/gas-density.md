# Gas density

Gas density at depth is one of the limiting factors of deep tech diving — and one of the easiest to get wrong if you don't actively check it.

## Why it matters

As depth increases, the absolute pressure rises (≈ 1 ata per 10 m), and the gas you breathe gets denser proportionally. Denser gas means:

- **Higher work of breathing** — your respiratory muscles do more work per breath
- **CO₂ retention risk** — harder to ventilate adequately, especially under exertion
- **Faster onset of exhaustion** — silent and hard to detect underwater
- **Greater susceptibility to narcosis effects** — though density and narcosis are partly independent

Above a certain density, the risk profile changes from "uncomfortable" to "dangerous." Two thresholds are widely cited:

| Density | Status | Reference |
|---|---|---|
| **≤ 5.2 g/ℓ** | Recommended ceiling | Mitchell & Anthony, 2018 |
| **6.2 g/ℓ** | Hard upper limit | Same source — beyond this, performance degrades sharply |

## How AeroPlus Deco reports it

The **Gas plan card → Limits table** lists the gas density at the deepest planned depth for each gas:

| Depth (m) | Mix | Density (g/ℓ) | PPO₂ |
|---|---|---|---|
| 75 | 16/58 | 5.14 | 1.34 |

Color coding:

- **Green / black** — within the 5.2 guideline
- **Orange** — exceeds 5.2 (warning)
- **Red** — exceeds 6.2 (limit)

The same density value also appears as a warning in the **Critical warnings** banner at the top of the plan when it exceeds either threshold.

!!! note "Reference temperature"
    Densities in the app are computed at **15 °C** (a typical cold-water reference). Warm-water densities are slightly lower — the values reported are conservative.

## Managing density with helium

Helium is much less dense than nitrogen, so swapping nitrogen for helium reduces gas density at depth. This is *why* trimix exists — narcosis management is one reason, but density management is the other half.

### Rule of thumb

For every 10 m of additional depth on a nitrox-heavy trimix, you typically need ~5–10 % more helium to keep density in check. Use the [Best mix calculator](../tools/best-mix.md) with **Limit gas density** toggled on to compute the right percentages automatically.

## The Best mix density-aware option

When **Limit gas density** is enabled in the Best mix calculator:

- The optimal mix targets **both** your narcotic depth (EAD) *and* a density ≤ 5.2 g/ℓ
- Whichever requirement needs more helium wins
- The result may have a shallower EAD than your target, but the density is safe

Same logic applies for **Best diluent** in CCR mode — the loop density is computed at the bottom setpoint and used as one of the constraints.

## Density vs MOD

A common confusion: a gas can have an acceptable PPO₂ at depth (so its MOD is fine) and *still* be too dense. PPO₂ and density are separate constraints. Check both.

For example: EAN32 at 40 m has PPO₂ = 1.34 (fine) but density ~5.0 g/ℓ (also fine, just). At 45 m, density rises to 5.5 g/ℓ — already over guideline — even though the PPO₂ is still under 1.6. The MOD doesn't catch that.

## Practical implications

- **Use trimix earlier** than narcosis alone would dictate. By 40 m on air you're at 5+ g/ℓ density even though the EAD is shallow.
- **Density-check every bottom mix** before going deeper than planned.
- **CCR loop density** is calculated for the loop gas composition at depth, not raw diluent. The loop tends to have less helium than the diluent at high setpoint (because the setpoint is more O₂), so loop density can be higher than diluent density.

## Further reading

- Mitchell, S. J., & Anthony, G. (2018). *Recommendations for rescue of a submerged unresponsive compressed-gas diver.* (Includes the 5.2 / 6.2 g/ℓ recommendations.)
- GUE — *Why we use helium and where we use it.*
