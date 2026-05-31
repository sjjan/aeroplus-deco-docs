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

CCR mode is more complex because the loop mix at the bottom is set by your **setpoint**, not by the diluent. So the calculator solves for the **diluent** — the gas in the offboard cylinder that fills the loop and doubles as open-circuit bailout. Two parts are derived:

- **Diluent O₂ %** — picked by the *diluent O₂ strategy* you have chosen (see below).
- **Diluent He %** — adjusted so the **loop** at the bottom setpoint meets your target EAD, and (if **Limit gas density** is on) the ≤ 5.2 g/ℓ density target. Both strategies feed this same helium logic — only the oxygen fraction differs.

### Diluent O₂ strategy

How the diluent's oxygen fraction is chosen is controlled under **App menu → Settings → CCR**, by the **Diluent O₂ from target PPO₂** toggle:

=== "Fixed 10 % (default)"

    The diluent holds a flat **10 % O₂**. It only drops below 10 % when — very deep — that 10 % would push the diluent's PPO₂ above 1.6 ata if breathed as open-circuit bailout, at which point the calculator lowers it automatically.

    This is the conventional "standard hypoxic diluent": one familiar number, carrying the richest practical O₂ fraction while still leaving a usable bailout margin at depth.

=== "Target diluent PPO₂"

    The diluent O₂ is set so its **partial pressure at the target depth equals a fixed target of 1.0 ata** — the value that keeps a small open-circuit PPO₂ margin at the bottom and a sensible loop O₂ floor during a diluent flush:

    ```
    Diluent O₂ % = 1.0 ÷ absolute pressure at depth
    ```

    For example, at 100 m (P~abs~ ≈ 11 ata) this gives **≈ 9 % O₂**; shallower depths get a correspondingly richer diluent. The result is clamped to 4–40 % O₂.

!!! note "Default is unchanged"
    Out of the box the strategy is **Fixed 10 %**, so existing CCR plans produce the same numbers until you turn the toggle on.

### Choosing a strategy

Both give a hypoxic diluent on a deep dive — the difference is *how* the oxygen fraction is chosen, and what that buys you.

**Fixed 10 %**

- *Advantages* — one standard blend to remember, analyse and label; being lean it has a deep open-circuit MOD (breathable as OC bailout to roughly 150 m), so the same diluent can double as emergency gas across most of the dive; nothing to decide per dive.
- *Disadvantages* — on a shallower "deep" dive it is more hypoxic than it needs to be, so its shallow breathable limit sits deeper and a diluent flush lands the loop at a lower PO₂; it does not adapt to the dive.

**Target diluent PPO₂ (1.0 ata)**

- *Advantages* — the diluent's PO₂ at the bottom is a known ~1.0 ata, so a diluent flush leaves the loop at a predictable PO₂ (a handy sanity-check against the cells) and never drives it too low; it adapts to depth, giving a richer, more surface-friendly diluent on shallower dives; it matches common field practice.
- *Disadvantages* — the diluent O₂ changes with planned depth, so you may blend, analyse and label a different diluent for each dive; on a shallower dive the richer diluent has a shallower OC MOD, so it covers a narrower band as bailout and you may need extra bailout cylinders.

!!! tip "Rule of thumb"
    Want one do-everything diluent that also serves as deep bailout? Keep **Fixed 10 %**. Prefer to tune diluent to each dive — and like a flush to read back a known loop PO₂? Use **Target diluent PPO₂**.

### Hypoxic diluent: fine on the loop, not on open circuit

A diluent under about **16 % O₂** is **hypoxic** — at the surface its PO₂ is below ~0.16 ata. That includes the default 10 % diluent (surface PO₂ ≈ 0.10).

**On the loop this is normal and safe.** The solenoid holds your setpoint, so the loop PO₂ — what you actually breathe — does not depend on the diluent's oxygen fraction. Deep CCR dives *require* a hypoxic diluent so the loop (and any diluent flush) does not become hyperoxic at depth.

It only matters if you come **off** the loop. Breathed on **open circuit** — a bailout, or a diluent flush in the shallows — a hypoxic diluent is unsafe near the surface: it is breathable only from the depth where its PO₂ reaches ~0.16 ata down to its MOD. The calculator reports that breathable/bailout depth range and flags the diluent as hypoxic, so you can plan a normoxic travel or bailout gas for any open-circuit use in the shallow zone.

### What's displayed

The result shows the diluent O₂/He (what is actually in the cylinder), plus:

- **Loop composition at bottom** — the mix actually breathed at the setpoint (e.g. "32 % O₂ / 37 % He / 31 % N₂")
- **Loop density** at depth
- **Breathable / bailout range** — the depth band where the diluent is safe as OC bailout (from its shallow hypoxic limit down to its MOD)
- **Hypoxic-diluent flag** when the diluent O₂ falls below 10 %

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

With the default **Fixed 10 %** strategy:

| Field | Value |
|---|---|
| Depth | 60 |
| Trimix | on |
| Target EAD | 30 |
| Limit gas density | on |

Result: **10/45** (10 % O₂, 45 % He). Loop at depth: 19 % O₂ / 36 % He / 45 % N₂. Density 4.8 g/ℓ. The 10 % diluent is hypoxic — fine to breathe on the loop, but as open-circuit bailout it is usable only from roughly 6 m down to its MOD, so carry a normoxic travel gas for any OC use in the shallows.

### Deep CCR with a Target-PPO₂ diluent (100 m)

With **Diluent O₂ from target PPO₂** turned on and a 1.0 ata target:

| Field | Value |
|---|---|
| Depth | 100 |
| Trimix | on |
| Target EAD | 30 |

Result: diluent O₂ ≈ **9 %** (1.0 ÷ 11 ata), with helium set to satisfy the EAD/density targets.

## When to use Best mix vs MOD/END

- **Best mix** — you know the depth, you need the mix
- **MOD/END** — you have a mix, you want to know where to breathe it

The two are inverses of each other. Best mix derives a mix from a depth. MOD/END derives depths/limits from a mix.
