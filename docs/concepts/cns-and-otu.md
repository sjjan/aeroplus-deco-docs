# CNS & OTU

Oxygen at elevated partial pressures is toxic to the body in two distinct ways. AeroPlus Deco tracks both.

## CNS — central nervous system toxicity

**CNS oxygen toxicity** is the acute risk — a sudden seizure underwater, almost always fatal because the diver loses consciousness and the regulator. It scales with **PPO₂ at depth** and time exposed.

The standard NOAA CNS clock tracks fractional exposure:

| PPO₂ (ata) | Single-exposure limit (min) |
|---|---|
| 1.6 | 45 |
| 1.5 | 120 |
| 1.4 | 150 |
| 1.3 | 180 |
| 1.2 | 210 |
| 1.0 | 300 |

Time at each PPO₂ adds a fraction of that limit to your CNS clock. AeroPlus Deco computes the cumulative CNS percentage and shows it in the **Deco plan card → top-line metric** and in the **Critical warnings** banner if it gets high.

### Practical limits

- **100 % CNS** — recommended single-dive maximum; some agencies cap at 80 %
- **80 % CNS** — typical aggressive ceiling for tech operations
- **40–50 % CNS** — recreational tech ceiling

CNS recovers exponentially during the surface interval — roughly halving every 90 minutes. AeroPlus Deco accounts for this when chaining repetitive plans.

## OTU — Oxygen Tolerance Units

**OTU** is the pulmonary toxicity measure — the slower, lower-acuity risk that builds up over hours and days of oxygen-rich diving. It manifests as lung irritation, reduced vital capacity, and eventually persistent chest pain.

OTU loading is computed as a function of PPO₂ (above ~0.5 ata) and time. Limits depend on the duration of activity:

| Activity | OTU limit |
|---|---|
| Single dive | 850 |
| Daily | 700–800 |
| Long expedition (multi-week, multi-dive) | 300/day average |

OTUs decay much slower than CNS — roughly **300 OTU/day** recovery — so they accumulate across a dive trip.

The Deco plan card shows the OTU total for the planned dive; if you're running repetitive plans, the surface interval card lets you tell the app how long you've been on the surface.

## How AeroPlus Deco handles them

- **CNS and OTU** are computed continuously throughout the dive (during descent, bottom, and ascent — including deco gas use)
- The **gas-switch model** assumes you switch to the richest available gas at its MOD on ascent
- The values shown are *for this dive only*; repetitive dive series tracking requires re-entering surface intervals
- High CNS or OTU triggers a warning in the **Critical warnings** banner

## Reducing oxygen exposure

If a plan triggers a CNS or OTU warning, the usual remedies are:

- **Use less aggressive deco gases.** EAN80 instead of pure O₂ at 6 m cuts both CNS and OTU significantly, at modest cost in deco time.
- **Shorten time at deco gas MOD.** A 1.6 PPO₂ ceiling for the rich deco gas is more conservative than running at 1.6 for the entire shallow phase.
- **Spread the exposure over multiple days.** Plan high-O₂ tech days non-consecutive.
- **Lower max deco PPO₂.** Set Max deco PPO₂ to 1.5 (in Settings) instead of 1.6 to push deco gas switches deeper.

## CCR considerations

On a CCR running setpoint 1.3 with a 1.5 deco SP, CNS and OTU accumulate steadily across the entire dive. Long-duration CCR diving (3+ hour tech dives) usually approaches OTU limits before CNS limits.

If you're planning multi-hour or multi-day CCR ops, consider:

- A lower deco SP (e.g. 1.4)
- A lower bottom SP for non-deco-driven portions of the dive
- Surface-side oxygen breaks limited or eliminated on heavy days

## Further reading

- NOAA — *Diving Manual* (CNS and OTU tables)
- IANTD — *Encyclopedia of Technical Diving*
