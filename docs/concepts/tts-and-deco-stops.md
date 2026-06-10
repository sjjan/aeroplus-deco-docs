# TTS & deco stops

## TTS — Time To Surface

**TTS** is the total time, in minutes, from the current moment to safe surface arrival, assuming you begin ascending immediately. It includes:

- Ascent time from the current depth to the first stop
- All decompression stop durations
- Ascent time between stops
- The final ascent from the last stop to the surface

It does **not** include any further bottom time. The clock starts when you start ascending.

### TTS at ascent start

In the Deco plan card, **TTS at ascent start** is the TTS calculated at the moment you leave the deepest segment of the planned dive. For a square-profile dive it's measured at "RT X" (runtime X), the planned end of the bottom segment.

For multi-level dives, TTS is calculated at the start of the *last* (shallowest planned) segment's ascent.

## Deco stops in the runtime schedule

The runtime schedule lists every depth-time event of the dive in chronological order, prefixed with a symbol:

| Symbol | Meaning |
|---|---|
| ↘ | Descending |
| → | Holding at depth (bottom segment or deco stop) |
| ↗ | Ascending |
| ⊙ | Gas switch event |

Deco stops are **highlighted in light green** to distinguish them from ascent or descent rows. The first deco stop is the deepest one — its depth is the *deepest ceiling* value.

### Reading a stop row

```
→  21.0   28   +3   16/58
```

This reads: **hold at 21.0 m, total runtime 28 min, stop duration +3 min, gas 16/58**.

- **Depth** — the stop depth (snapped to your stop interval, default 3 m)
- **Runtime** — total elapsed dive time at this point
- **Duration** — how long this stop lasts (with `+` prefix to distinguish from runtime)
- **Gas** (OC) — the cylinder mix used at this stop (e.g. `16/58`, `50/0`); a ⊙ prefix means a gas switch happened just before
- **Loop SP / Dil PPO₂** (CCR) — the loop setpoint and the diluent partial pressure of oxygen at this depth

### Gas switch rows

When a deco gas comes into range (its MOD is reached), a separate **gas switch row** appears with the ⊙ symbol:

```
⊙  21.0   26   +1   50/0
```

This represents the planned pause to switch regulators, verify the mix, and stabilise. The duration (default 1 min) is configurable in **Settings → Gas switch time**.

## Stop durations and rounding

The algorithm computes raw stop durations as decimals and then rounds. Two options:

- **Round stop times** (Settings → Round stop times) — rounds each stop *up* to the nearest whole minute, matching dive computers like Shearwater. On by default.
- **Off** — keeps decimal precision, useful for comparing planners.

The total deco time and total runtime adjust accordingly.

## Stop interval

The **stop interval** (Settings → Deco stop interval) controls the spacing of valid stop depths. Default is 3 m, producing stops at 3, 6, 9, 12, 15, 18, 21, 24… metres. Some agencies and computers use 1 m or 2 m intervals — set it to match your reference computer for direct comparison.

## Last stop

The **last stop** (Settings → Last deco stop) is the shallowest mandated stop, even when the algorithm allows surfacing. Default is 6 m. Most agencies recommend 6 m for OC and 3 m for CCR; some divers run 3 m as a "safety stop" regardless of obligation.

## When a stop is skipped

AeroPlus Deco follows the decompression **ceiling** as a continuous curve and lists a stop only at the depths where the model actually requires you to wait. If, by the time you reach a given depth, your tissues have already off-gassed enough that no time is owed there, that depth simply does not appear in the schedule.

This is why a plan can show a first stop at 18 m and then the next at 9 m, with nothing at 15 m or 12 m. It is not a missing stop — the obligation at those depths has genuinely fallen to zero.

The effect is clearest right after a gas switch. Moving onto a rich decompression gas (say EAN50, or oxygen) sharply lowers the inert gas you are breathing and speeds up off-gassing, so the ceiling can rise past several stop depths during a single hold. A richer gas collapses the intermediate stops to nothing. This is ordinary gradient-factor behaviour, and it is why a modern dive computer will often show its first *real* stop at 9 m or 6 m on a dive where a much deeper first stop might have been expected.

Some other planners and computers present the same ascent differently: they print a line at **every** stop interval from the first stop to the surface and apply a **minimum stop of one minute** to any depth that carries even a few seconds of obligation — a "trapeze" ladder (18, 15, 12, 9, 6, 3 m, each at least a minute). AeroPlus Deco does not insert these one-minute placeholders, so its list is shorter and shows larger gaps between the stops it does print. The underlying decompression is identical; only the presentation differs, and the figures that matter — total decompression time and time-to-surface — come out the same either way.

## Ascent rate during decompression

AeroPlus Deco uses two ascent rates, both set in **Settings → Diver & gas**:

- **Ascent speed** — the rate used to climb from the bottom toward the first decompression stop (default 10 m/min).
- **Deco ascent speed** — the rate used between stops once decompression has begun, usually set slower (for example 3 m/min).

The slower deco rate takes effect **from the first decompression stop onward** — on the legs from the first stop up to each shallower stop and on to the surface. It does **not** start simply because you have switched to a decompression gas.

This matters whenever your first gas switch is *deeper* than your first stop. Suppose you switch to 50/0 at 21 m but the first stop is at 9 m: the whole climb from the bottom up to 9 m — including the leg through the 21 m switch — is flown at the normal ascent speed. The slower deco rate governs only the staged portion, 9 m → 6 m → 3 m → surface. The gas switch still adds its own fixed pause (**Settings → Gas switch time**), but it does not change the ascent rate.

!!! note "Tied to the first stop, not the gas"
    The deco ascent rate is keyed to the **first deco stop depth**, not to the gas you happen to be breathing. The faster rate gets you to where decompression actually begins; the slower rate then governs the decompression itself.

## Ascent trigger

In the **Rock bottom & TTS** card, the **Target TTS** field lets you set a personal ascent trigger:

> Start your ascent when *either* your dive computer shows TTS ≤ your target, *or* your gas reaches the minimum reserve — whichever comes first.

Common settings are 10–15 min for a recreational tech dive, longer for trimix work. The number you enter is just for your reference — it doesn't change the calculation.

## Maximum TTS

Beneath the Target TTS field the app also shows your **maximum TTS** — the time-to-surface you would reach if you stayed down until a gas limit binds. It is the hard ceiling that keeps you out of your reserve, and it is usually larger than your planned TTS, since most plans surface with some unused gas.

### How it's calculated

It isn't estimated from a formula. AeroPlus Deco re-runs your **entire decompression plan** repeatedly, lengthening the last bottom segment a little more on each pass (a binary search), so every trial is a complete, valid schedule for that longer bottom time. At each trial it checks whether you would still be within your gas:

- **Open circuit** — your back gas must stay above the rock-bottom reserve (recomputed for each longer profile), and the app **iterates through every enabled deco gas** to confirm none would run dry at the longer runtime — more bottom time means more decompression, and therefore more deco-gas demand. Whichever binds first — back gas reaching the reserve, or a deco gas running out — sets the limit. The readout names it and shows the deco-gas demand at that maximum, per cylinder, against the planned figure.
- **Closed circuit** — back gas isn't the limit (the loop is recirculated, not consumed), so each trial instead checks **scrubber endurance**, **onboard O₂** at your metabolic rate, and — in independent bailout mode — **bailout sufficiency**. Whichever runs out first sets the limit; in group bailout mode the team is responsible for bailout, so only scrubber and O₂ bound the maximum.

The app reports the TTS at the last bottom time that still passes every applicable check, never below your planned TTS. Plan and turn at your target TTS for margin; treat the maximum as the ceiling you should never exceed. Full detail is on the [rock bottom](rock-bottom.md#maximum-tts-and-the-ascent-trigger) and [maximum TTS on CCR](../ccr/oxygen-and-scrubber.md#maximum-tts-on-ccr) pages.

!!! warning "It depends on your assumptions"
    The maximum TTS is only as good as your inputs. It assumes you ascend at exactly the rate set in preferences and execute every decompression stop to the letter, and it is driven by your SAC (open circuit) or your metabolic O₂, SAC and scrubber settings (CCR). Double-check those and plan conservatively — real-world consumption is often higher than planned.