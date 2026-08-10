# Units — metric & imperial

AeroPlus Deco works in either **metric** or **imperial**. Set it in **Settings → Units**; the choice applies everywhere in the app at once — the plan page, the runtime schedule, the calculators, the warnings, the checklists and every export.

| Quantity | Metric | Imperial |
|---|---|---|
| Depth | m | ft |
| Pressure | bar | psi |
| Cylinder size / volume | ℓ | cu ft |
| Gas consumption (SAC/RMV) | ℓ/min | cu ft/min |
| Ascent & descent rates | m/min | ft/min |
| Gas density | g/ℓ | g/ℓ (unchanged) |

Gas density stays in g/ℓ in both systems, because the 5.2 / 6.2 g/ℓ thresholds are quoted that way throughout the technical diving literature. Times, percentages, PPO₂ in ata, CNS % and OTU are unit-independent.

## How the conversion works

The decompression model itself is always metric internally — depths in metres, pressures in bar, volumes in litres. Imperial is a **display layer** on top of it: values are converted on the way out to the screen and converted back on the way in when you type them. Switching units never re-runs the physics differently, so a plan does not become more or less conservative because you changed the display.

Two consequences are worth knowing about.

### Your entered values are preserved, not re-rounded

If you enter a 12 ℓ cylinder at 232 bar and switch to imperial, you will see the cu ft and psi equivalents of exactly those numbers, not a tidied-up nearby value. Switch back and you get 12 ℓ / 232 bar again.

### Round-number conventions do get snapped

A handful of settings have a conventional round value in each system rather than an exact conversion. When you switch units, AeroPlus Deco moves these to the target system's convention — but **only if they are still sitting at the other system's convention**. If you have set your own value, it is left alone.

| Setting | Metric convention | Imperial convention |
|---|---|---|
| Ascent speed | 10 m/min | 33 ft/min |
| Deco ascent speed | 3 m/min | 10 ft/min |
| Descent speed | 18 m/min | 60 ft/min |
| Last deco stop | 6 m | 20 ft |
| Contingency deeper | +3 m | +10 ft |

!!! note "Ascent speed is a true conversion, not a different rate"
    33 ft/min is 10 m/min. Earlier versions snapped the imperial ascent speed to 30 ft/min, which is a genuinely slower ascent (about 8.6 % slower) and therefore quietly increased the calculated [rock-bottom reserve](concepts/rock-bottom.md) when you switched units. That is fixed: the physical ascent rate is now the same in both systems. If you prefer 30 ft/min as your working ascent rate, set it explicitly in **Settings → Ascent speed** — it will then be respected and not overwritten.

## Why the two systems can differ by a minute or a bar

Run the same dive in metric and imperial and the schedules will agree closely, but not always to the digit. The reason is the **decompression stop grid**, which follows the convention of the system you are in:

- Metric stops fall on a **3 m** grid — 3, 6, 9, 12 m …
- Imperial stops fall on a **10 ft** grid — 10, 20, 30, 40 ft …

10 ft is 3.048 m, so an imperial stop sits fractionally deeper than its metric counterpart, and the last stop is 20 ft (6.096 m) rather than 6.00 m. Slightly deeper stops mean slightly slower off-gassing, so you may see a stop time differ by a minute, a gas switch land at 70 ft instead of 21 m, or CNS and OTU come out a point higher. Differences of this size are expected and correct — they reflect the grid you asked for, not a disagreement in the model.

If you are cross-checking AeroPlus Deco against another planner, compare like with like: set both tools to the same unit system before reading anything into a discrepancy.

## Entering decimals

Number fields accept both the point and the comma as a decimal separator, so `11,1` and `11.1` are the same value. This matters most in the [gas blending calculator](tools/gas-blending.md), where fractional pressures are common.
