# The Andy Davis method for GF Low

The **Andy Davis method** is a published, systematic way to choose GF Low for open-circuit tech dives. AeroPlus Deco's **Auto-set GF Low** toggle implements it.

## The core idea

Andy Davis ([article](https://scubatechphilippines.com/scuba_blog/gradient-factors-application-use-settings-open-circuit-tech/)) argues that on open-circuit:

1. **Deep stops on back gas waste time** — slow tissues continue to on-gas while you sit there breathing the same mix you breathed at depth.
2. **The biggest off-gassing acceleration happens when you switch to a richer deco gas** — typically 50 % nitrox with an MOD of 21 m, or oxygen-enriched trimix as a travel mix on hypoxic dives.
3. **Therefore, the first decompression stop should coincide with the MOD of your first gas switch on ascent.** You arrive at the first stop, switch to the rich mix, and start off-gassing fast — no wasted time deeper.

So the procedure is:

1. Identify the gas you'll switch to first on ascent (almost always the deepest deco gas, or a travel/intermediate gas if you carry one).
2. Compute its MOD at your max-deco PPO₂ (1.6 ata for most agencies).
3. Tune GF Low until the planner produces a first stop at that depth.

## Worked examples from the article

| Scenario | Bottom gas | Deco gas | Target stop | GF Lo / Hi |
|---|---|---|---|---|
| 40 m × 20 min | air | EAN50 (MOD 21 m) | 21 m | **25 / 70** |
| 50 m × 20 min | air | EAN50 (MOD 21 m) | 21 m | **40 / 70** |

Note how *different* the two GF Lo values are for the same target depth — 25 versus 40. The relationship between GF Lo and first-stop depth is **not** a simple ratio; it depends on the actual tissue saturation, which depends on the dive's depth, time, and gases. The article explicitly says to iterate: tweak GF Lo, recalculate, repeat until the first stop lands where you want it.

## How AeroPlus Deco implements it

When **Auto-set GF Low** is toggled on, the app:

1. **Collects ascent gas switches.** All cylinders with role `deco` or `travel` that are switched on.
2. **Computes their MODs** at the configured max-deco PPO₂ (default 1.6 ata).
3. **Picks the deepest MOD** — that's the first gas you'd switch to on ascent.
4. **Snaps to a valid stop depth** (e.g. 22 m → 21 m at 3 m stop intervals).
5. **Iteratively searches** for the largest GF Lo in `[10, GFHi − 10]`, in 5 % steps, such that the resulting first decompression stop is **at or below** the switch depth.
6. **Sets GF Lo** to the value found.

The search uses real `planDive` calls — same code path as the regular calculation — so it reflects the actual dive profile, gases, ascent rates, and stop interval.

## Reading the label

The settings row shows what was decided:

> GF Low set to 40 % (first stop 21 m)

Plain success: target reached. The first stop will be at the gas switch depth.

> GF Low set to 65 % (first stop 30 m — target switch depth 21 m not reached)

This means the dive is heavy enough (deep, long, lots of helium) that even at the most aggressive practical GF Lo, the model still wants a stop deeper than your richest deco gas's MOD. **Add an intermediate travel gas** — e.g. EAN30 with MOD ~30 m — so the natural first stop coincides with a switch. Or accept a back-gas stop deeper than the deco gas MOD and tune GF Lo manually.

## Why this doesn't apply to CCR

The article directly addresses this:

> *"Rebreather divers use constant set-points that continuously deliver an optimal breathing gas mix throughout the bottom and deco phases of a dive. As they are unconstrained by carrying only a few pre-set mixes, their choice of gradient factors doesn't need to consider off-gassing efficiency or slow-tissue on-gassing as major controlling factors."*

On a CCR, you're breathing your setpoint-controlled loop mix throughout. There's no "switch to richer gas" event with a sudden off-gassing benefit to time. CCR divers pick GF Low based on personal preference and agency guidance — typically 30, 35, or 40.

AeroPlus Deco greys out **Auto-set GF Low** in CCR mode and shows a "not applicable in CCR" note. The toggle remains visible so you can read the method link, but you can't activate it.

## When to override

The Andy Davis method is a starting point, not gospel. Override it when:

- You have **gas-density concerns** — sometimes a slightly deeper first stop on a denser bottom gas reduces work-of-breathing risk at the cost of slow-tissue on-gassing.
- You're following a **specific agency curriculum** — some agencies teach fixed GF settings as part of certification.
- You're **building tolerance** to a more aggressive profile gradually — the method's result might be more aggressive than your current experience supports.

Switch off the toggle and set GF Low manually whenever you want different conservatism than the method gives you.

## References

- Andy Davis — [A Logical Application of Gradient Factors for OC Tech Divers](https://scubatechphilippines.com/scuba_blog/gradient-factors-application-use-settings-open-circuit-tech/)
- Andy Davis — [Gradient Factor Comparison: 60m Trimix Case-Study](https://scubatechphilippines.com/scuba_blog/gradient-factor-comparison-60m-trimix-decompression-dive/)
