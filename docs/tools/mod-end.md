# MOD / EAD / END

The **MOD / EAD / END** calculator analyzes an existing gas mix: how deep it's safe, how narcotic it is, and how dense it gets.

Open via **App menu → Tools → MOD / EAD**.

## Inputs

| Field | What it controls |
|---|---|
| **O₂ %** | Oxygen percent of the mix (5–100) |
| **He %** | Helium percent (0–95). N₂ is the balance. |
| **Depth (m)** | Target depth. Pre-filled with the deepest segment of your active plan. |
| **PPO₂ limit (ata)** | Max allowed PPO₂ for the calculation. Default 1.40. |

The **Mix** display shows the combined `O₂/He` notation for clarity.

## Outputs

| Result | Meaning | Color logic |
|---|---|---|
| **MOD** | Max operating depth at the configured PPO₂ limit | Red if < target depth, neutral otherwise |
| **PPO₂ at depth** | The actual PPO₂ this mix delivers at the target depth | Yellow > limit, red > 1.6 |
| **EAD** | Equivalent Air Depth — N₂ narcotic only, He treated as inert (most agencies' planning standard) | Yellow > 40 m |
| **END** | Equivalent Narcotic Depth — N₂ + O₂ both narcotic (GUE method) | Yellow > 40 m |
| **EADD** | Equivalent Air *Density* Depth — at what air depth the same density would occur | Informational |
| **Gas density** | At the target depth (15 °C reference) | Yellow ≥ 5.2 g/ℓ, red ≥ 6.2 g/ℓ |

## Definitions

### MOD (Max Operating Depth)

```
MOD = (PPO₂_limit ÷ fO₂ − 1) × 10
```

At MOD, the PPO₂ exactly equals the configured limit. Going deeper exceeds it.

For 21 % O₂ at PPO₂ 1.4: MOD = (1.4 / 0.21 − 1) × 10 ≈ 57 m.

### EAD (Equivalent Air Depth — N₂ only)

```
EAD = (fN₂ × (depth + 10)) / 0.79 − 10
```

The depth at which **air alone** would deliver the same N₂ partial pressure as your mix at the current depth. The standard planning measure for narcosis on agencies that treat O₂ as non-narcotic (most: PADI, TDI, SDI, IANTD, RAID).

### END (Equivalent Narcotic Depth — N₂ + O₂)

```
END = (1 − fHe) × (depth + 10) − 10
```

Treats both N₂ and O₂ as narcotic, helium as inert. Used by GUE and a few other agencies. Always shallower than EAD for the same mix (because O₂ adds to the narcotic load in this model).

### EADD (Equivalent Air Density Depth)

```
EADD = ((P_eq − 1) × 10)
where P_eq = depth_pressure × (mix_MW / air_MW)
```

The air depth that produces the same gas density. Useful for density-conscious planning: if your mix's EADD is 50 m, it's as dense as air at 50 m, regardless of its narcotic equivalent.

### Gas density

```
density = (mix_MW ÷ 22.4) × (Pabs ÷ 1.01325)
where mix_MW = 32 × fO₂ + 4 × fHe + 28 × fN₂
```

The mass per litre of the mix at the target depth, computed at 15 °C reference.

## Worked example

Mix: **16/58 trimix** at **75 m**, PPO₂ limit 1.40

| Result | Value |
|---|---|
| MOD | 77 m (1.4 / 0.16 − 1) × 10 |
| PPO₂ at depth | 1.36 ata (0.16 × 8.5) |
| EAD | 13 m ((1−0.16−0.58) × 8.5 − 10) |
| END | 26 m ((1−0.58) × 8.5 − 10) |
| EADD | ~50 m |
| Gas density | 5.06 g/ℓ |

Reading this:

- MOD 77 m at 1.4 → fine, you're at 75 m so well within
- EAD 13 m → minimal narcosis (vs air at 13 m), excellent
- END 26 m → if you follow GUE method, still acceptable
- Density 5.06 g/ℓ → green (just under 5.2 guideline)

## Practical use

- **Verify a bottom gas** before plugging it into a plan. If MOD < target depth, change the mix.
- **Compare narcosis between mixes.** Two trimix options for the same depth can have noticeably different EADs.
- **Density sanity check.** Especially relevant when the dive depth approaches 50+ m and you're using nitrox-heavy trimix.
- **PPO₂ alarm.** If the PPO₂ at depth turns red (>1.6), the mix is acutely dangerous at this depth.

## Comparing EAD vs END

For a 16/58 trimix at 75 m:

- EAD = 13 m (treating O₂ as non-narcotic)
- END = 26 m (treating O₂ as narcotic)

The 13 m difference (the contribution of O₂ to narcotic load in the END model) is significant on paper but smaller in practice. Most agencies don't differentiate. Pick the one matching your training and stick to it.
