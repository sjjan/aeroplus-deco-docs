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

## Ascent trigger

In the **Rock bottom & TTS** card, the **Target TTS** field lets you set a personal ascent trigger:

> Start your ascent when *either* your dive computer shows TTS ≤ your target, *or* your gas reaches the minimum reserve — whichever comes first.

Common settings are 10–15 min for a recreational tech dive, longer for trimix work. The number you enter is just for your reference — it doesn't change the calculation.
