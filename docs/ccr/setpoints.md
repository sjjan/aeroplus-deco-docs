# Setpoints

A **setpoint** is the loop oxygen partial pressure (PPO₂) the rebreather electronics aim to maintain. AeroPlus Deco uses up to three setpoints plus a switch depth, plus optional per-segment overrides.

## The four configuration fields

In the **Closed Circuit Setup** card on the main plan page:

| Field | What it controls |
|---|---|
| **Surface SetPoint** | Loop PPO₂ when shallower than the switch depth (surface → switch depth on descent; switch depth → surface on ascent). Typical: **0.7 ata** |
| **SP switch depth** | The depth at which the dive moves from surface SP to bottom SP. Typical: **20 m** |
| **Bottom SetPoint** | Loop PPO₂ during the bottom phase, used below the switch depth. Typical: **1.3 ata** |
| **Deco SetPoint** | Loop PPO₂ at all decompression stops. Typical: **1.3 or 1.5 ata** |

## How the setpoints behave during the dive

A typical descent → bottom → ascent → deco profile uses them in this order:

```
Surface (0 m) ─── Surface SP 0.7 ───→ Switch depth (20 m)
                  ↓ algorithm uses 0.7 ata for tissue saturation
                  
Switch depth (20 m) ─── Bottom SP 1.3 ───→ Bottom (e.g. 60 m)
                       ↓ algorithm uses 1.3 ata throughout this phase
                       
Bottom → Ascent → First stop
                       
First deco stop ─── Deco SP 1.3 (or 1.5) ───→ Last stop (6 m)
                                            ↓ algorithm uses deco SP
                                            
Last stop ─── Surface SP 0.7 ───→ Surface
```

The Surface SP is used during the surface phase and final ascent. The Bottom SP covers the deep portion. The Deco SP covers stops.

## What loop PPO₂ does to the diver

The loop is a mixture of oxygen and diluent inert. At any depth:

- **Loop O₂ fraction** = setpoint ÷ absolute pressure
- **Loop inert fraction** = 1 − O₂ fraction = (1 − SP/Pabs) of whatever inert mix the diluent provides

For example, at 30 m (Pabs ≈ 4 ata):

| Setpoint | Loop O₂ | Loop inert |
|---|---|---|
| 0.7 ata | 18 % | 82 % |
| 1.0 ata | 25 % | 75 % |
| 1.3 ata | 33 % | 67 % |
| 1.5 ata | 38 % | 62 % |

Higher setpoint = more O₂ in the loop = less inert gas = faster off-gassing on ascent.

## Typical setpoint choices

### Recreational CCR
- Surface 0.7, switch 6–10 m, bottom 1.0, deco 1.0
- Conservative; the lower bottom SP keeps CNS low

### Sport tech CCR (40–60 m)
- Surface 0.7, switch 20 m, bottom 1.3, deco 1.3
- Standard for most tech curricula

### Aggressive tech CCR (60 m+)
- Surface 0.7, switch 30 m, bottom 1.3, deco 1.5
- Slightly deeper switch and higher deco SP for faster off-gassing
- CNS accumulates faster — watch the warning

### Hypoxic / cave / wreck penetration
- Sometimes Bottom SP 1.2 to extend scrubber duration and reduce CNS
- Always coordinate with team practice

## Per-segment setpoint override

For multi-level dives or unusual profiles, you can override the bottom SP per segment. In the segment editor (when CCR mode is on), an **SP** field appears:

| Field | Range | What it does |
|---|---|---|
| SP | 0.40–1.60 ata | Overrides the bottom SP for this segment only |

The segment-level SP only applies *during* that segment. Descents into / ascents out of the segment use the standard setpoint logic.

Use cases:

- A "drift down" segment where you want a lower SP to extend scrubber
- A short bounce within a long shallower dive where 1.5 makes sense temporarily
- Mixed-team dives where some divers run different setpoints than the algorithm assumes

## Reading setpoints in the output

The runtime schedule's **Loop SP** column shows the active setpoint at each row:

```
↘ 75.0   4   +3:03   SP 1.30   1.51
→ 75.0  15   +11     SP 1.30   1.51
↗ 33.0  19   +4:12   SP 1.30   0.76
→ 33.0  20   +2      SP 1.50   0.76
```

The fourth column is **Loop SP** (the planned loop PPO₂). The fifth column is **Diluent PPO₂** — the raw diluent's PPO₂ at that depth (what you'd see on a diluent flush or OC bailout to diluent). Diluent PPO₂ is colored red if it exceeds 1.6 ata — a hypoxic-incompatible situation requiring travel/bailout gas to descend safely.

## Common questions

### Why is Surface SP 0.7 and not 0.21 (air)?

A surface PPO₂ of 0.7 means the loop has more O₂ than ambient air. It maintains a healthy loop oxygenation during descent before reaching the switch depth. Going *too* low risks hypoxic loop conditions if the diver swims down with the loop closed.

### What about pre-breathe?

Most rebreather drills include a 3–5 min pre-breathe to verify the loop and scrubber. AeroPlus Deco doesn't model the pre-breathe explicitly — it starts the calculation from the first segment.

### Can I set the bottom SP higher than 1.4?

Yes, but be aware of CNS. Bottom SP 1.5 for a long dive accumulates CNS very fast. 1.3 is the practical sweet spot for most tech CCR work.
