# Best mix

The **Best mix** calculator derives the optimal gas percentages for a target depth and PPO₂ limit. Two modes: **OC** (for cylinders you'll breathe directly) and **CCR** (best diluent for a loop setpoint).

Open via **App menu → Tools → Best mix**.

## Inputs

| Field | What it controls |
|---|---|
| **Depth (m)** | Target depth. Pre-filled with the deepest segment of your active plan, if any. |
| **PPO₂ (ata)** | Maximum allowed PPO₂ at the target depth. Default: 1.40 ata. |
| **Trimix** (toggle) | Include helium in the mix. When on, also asks for Target EAD. |
| **Target EAD (m)** | Equivalent air depth — controls how narcotic the mix is. Typical: 30 m for deep dives. |
| **Limit gas density** (toggle) | Cap gas density at 5.2 g/ℓ as a second constraint. May add more helium than EAD alone requires. |

## Outputs

The Best mix and analysis results:

| Result | Meaning |
|---|---|
| **Best mix** | The recommended O₂/He percentages (e.g. `16/57`). |
| **MOD** | Max operating depth at the requested PPO₂. |
| **N₂ fraction** (OC) | Balance gas; can show density warning if relevant. |

If you've requested trimix, the Best mix shows both numbers (e.g. `16/57` = 16 % O₂, 57 % He, 27 % N₂).

## How it works (OC)

For nitrox (no helium):

```
Best O₂ % = PPO₂ ÷ absolute pressure at depth
```

For example, at 40 m (Pabs ≈ 5 ata) with PPO₂ 1.4 → O₂ = 28 %, so the recommended mix is EAN28.

The MOD is then the depth where this O₂ % hits the PPO₂ limit again — confirming where you can still safely breathe the mix.

For **trimix** (helium added):

```
Best O₂ % = PPO₂ ÷ absolute pressure at depth
Best He %, given target EAD, satisfies:
   N₂ fraction at depth = N₂ fraction of air at EAD
   → N₂ = 0.79 × (EAD + 10) / (depth + 10)
   → He = 1 − O₂ − N₂
```

If **Limit gas density** is on, an additional constraint:

```
Loop density at depth ≤ 5.2 g/ℓ
```

The helium is increased until both EAD and density requirements are satisfied. Whichever requires more helium wins; the EAD ends up shallower than requested.

## How it works (CCR — best diluent)

CCR mode is more complex because the loop mix depends on the bottom setpoint, not the diluent.

The optimum diluent has:

- **10 % O₂** (normoxic) when possible — so it's breathable as bailout from at least the surface
- **He %** adjusted so the **loop** at the bottom setpoint achieves the target EAD and density

If 10 % O₂ produces a diluent PPO₂ > 1.6 ata at depth (i.e., the diluent would be over-rich during a flush), the algorithm reduces the O₂ fraction below 10 % — making the diluent **hypoxic**. A hypoxic diluent requires a travel/bailout gas to descend safely through the surface phase.

The result is displayed as the diluent O₂/He (what you'd actually have in the cylinder), along with:

- **Loop composition at bottom** — the actual mix being breathed (e.g. "32 % O₂ / 37 % He / 31 % N₂")
- **Loop density** at depth
- **Bailout range** — the depth range where this diluent can be safely breathed as OC bailout (typically 0–MOD of diluent)
- **Hypoxic warning** if the diluent's O₂ < 10 %

## Reading the warnings

Below the result, depth-specific information appears:

- **PPO₂ at depth** — what the *raw* mix will deliver
- **MOD** — at the configured limit
- **Gas density** — color-coded as green/orange/red

If the density warning is yellow or red and **Limit gas density** is off, toggle it on and re-derive; the resulting mix will satisfy both constraints (if mathematically possible).

## Practical examples

### Typical 40 m tech dive

| Field | Value |
|---|---|
| Depth | 40 |
| PPO₂ | 1.40 |
| Trimix | off |

Result: **EAN28** (28 % O₂). MOD 40 m. Suitable for relatively narcosis-tolerant dives; consider EAN26 or trimix for less narcosis.

### Deep tech (75 m)

| Field | Value |
|---|---|
| Depth | 75 |
| PPO₂ | 1.40 |
| Trimix | on |
| Target EAD | 30 |
| Limit gas density | on |

Result: **16/58 trimix** (16 % O₂, 58 % He). Density and narcosis both within limits.

### CCR diluent for 60 m, SP 1.3

| Field | Value |
|---|---|
| Depth | 60 |
| Trimix | on |
| Target EAD | 30 |
| Limit gas density | on |

Result: **10/45** (10 % O₂ normoxic, 45 % He). Loop at depth: 19 % O₂ / 36 % He / 45 % N₂. Density 4.8 g/ℓ. Diluent is fine for OC bailout from 0 m down to MOD (with MOD calculated for raw diluent at 1.6 PPO₂).

## When to use Best mix vs MOD/END

- **Best mix** — you know the depth, you need the mix
- **MOD/END** — you have a mix, you want to know where to breathe it

The two are inverses of each other. Best mix derives a mix from a depth. MOD/END derives depths/limits from a mix.
