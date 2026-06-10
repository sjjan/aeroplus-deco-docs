# Gas blending

The **Gas blending** calculator computes the fill sequence — how much of each gas to add to a cylinder to reach a target mix at target pressure, using partial-pressure blending.

Open via **App menu → Tools → Gas blending**.

## Two modes: Partial Blending and Topping Up

The Gas blending screen has two tabs, which solve opposite problems:

- **Partial Blending** *(default)* — *"I want to end up with mix X at pressure Y."* You enter a target mix and target pressure (plus whatever is already in the cylinder) and the app returns the **fill sequence**: how much helium, then oxygen, then top-up gas to add, in order, with optional heat (cooling) compensation. This is the *inverse* problem — it solves for what to add. The rest of this page describes this mode.
- **Topping Up** — *"I'm about to add this gas to what's already in the cylinder — what will I end up with?"* You enter what's in the cylinder now and the gas you'll top up with, and the app returns the **resulting mix**. This is the *forward* problem — it predicts the result of a fill you're about to make. See [Topping up](#topping-up-predicting-the-resulting-mix) below.


## What partial-pressure blending is

Partial-pressure blending is the standard tech-fill method:

1. Start with a cylinder at known pressure and known mix
2. Add pure helium first (raises He partial pressure)
3. Add pure oxygen next (raises O₂ partial pressure)
4. Top up with a base gas (air or pre-blended nitrox) to reach final pressure

Each step is measured by **pressure added**, not by volume. The math is straightforward but easy to get wrong by hand — hence the calculator.

## Inputs

| Section | Fields |
|---|---|
| **Cylinder** | Size (ℓ), Target pressure (bar) |
| **Current fill** | Current pressure (bar), Current O₂ %, Current He % |
| **Target mix** | Target O₂ %, Target He % — or pick a preset |
| **Top-up gas** | Air, EAN32, EAN36, EAN50, or Custom |
| **Gas analysis depth** | Depth (m) for the resulting mix's properties |
| **Heat compensation** | Optional overfill for cool-down (defaults: 20°C ambient, 15°C rise) |

## Outputs

### Fill sequence

A numbered set of steps:

1. **Step 1** — Add X bar of Helium (100%); fill cylinder to Y bar
2. **Step 2** — Add X bar of Oxygen (100%); fill cylinder to Y bar
3. **Step 3** — Add X bar of Top-up gas; fill cylinder to Y bar (final)

Each step shows:

- **Gas to add** (helium, oxygen, or named top-up)
- **Amount to add** (bar)
- **Pressure to fill to** (bar) — the cylinder gauge reading at end of this step

Any step where the required addition is below 0.5 bar is omitted (i.e., if your mix already has enough of that component).

### Resulting mix

After the fill sequence, the resulting mix is computed:

- **O₂ %, He %, N₂ %** of the final mix
- **Match indicator** — green if within ±0.5 % of target, yellow otherwise

### Gas properties at depth

For the resulting mix at the analysis depth:

- **PPO₂** (ata, colored if > limits)
- **MOD** at 1.4 and 1.6
- **Gas density** at depth (colored against 5.2 / 6.2 thresholds)
- **EAD** and **END** at depth

## Heat compensation

When you compress gas into a cylinder fast, the gas heats up. As it cools to ambient temperature later, the pressure drops. If you stop filling at the target gauge pressure while the gas is hot, you'll be short on pressure once it cools.

The **Heat compensation** toggle adds an overfill factor:

- **Ambient temperature** (°C) — what the cylinder cools to after the dive shop
- **Temperature rise during fill** (°C) — typical 10–20 °C for fast fills

The calculator computes the overfill factor (e.g. 1.05× for a 15°C rise from 20°C ambient) and shows the actual fill pressure to use at the gas station. The actual mix percentages are still computed against the target pressure, so the chemistry comes out right after cool-down.

## When draining is required

If your current cylinder already has too much of some component to reach the target by addition alone (e.g., your target has 25 % O₂ but your existing fill is 50/0), the calculator detects this and shows:

> ⚠ Cylinder needs to be drained first. Drain to approximately X bar, then follow the fill sequence below.

Drain the cylinder to the indicated pressure, then the fill sequence works.

## Worked example

**Goal:** fill an empty 12 ℓ cylinder to 200 bar of EAN50.

| Input | Value |
|---|---|
| Cylinder size | 12.0 ℓ |
| Target pressure | 200 bar |
| Current pressure | 0 bar |
| Current mix | (any — doesn't matter for empty) |
| Target O₂ % | 50 |
| Target He % | 0 |
| Top-up | Air |

The calculator outputs:

1. **Step 1**: skip (no helium needed)
2. **Step 2**: Add 73.4 bar of Oxygen (fill to 73 bar)
3. **Step 3**: Add 126.6 bar of Air (fill to 200 bar)

Resulting mix: 50/0. Density at 21 m: 1.7 g/ℓ. PPO₂ at 21 m: 1.55. ✓

## Topping up — predicting the resulting mix

The **Topping Up** tab answers the forward question: given what's in the cylinder now and the gas you'll add, what mix do you finish with?

### Inputs and output

- **Start pressure** and **Start O₂ / He** — what's in the cylinder right now.
- **Top-up O₂ / He** — the gas you'll add. Free entry, so hypoxic trimix top-ups (e.g. 7/70) are fine.
- **Finish pressure** — the pressure you'll fill to.
- **Result** — the final O₂ / He / N₂. If the resulting O₂ is below 18 % the figure turns **red**, flagging a hypoxic mix that is not breathable at the surface.

### How it works

Topping up a single cylinder is pure partial-pressure addition. The gas already in the cylinder keeps its share; the added gas contributes (finish − start) bar of its own mix; the two combine in proportion to pressure. Because it's one cylinder, **cylinder size doesn't matter** (the volume cancels), and **temperature doesn't matter to the resulting fractions** (all partial pressures scale together). That's why — unlike Partial Blending — there is no heat-compensation control in this tab: you read the finish pressure off your gauge, and the mix is simply whatever the pressures make it.

### Worked example

A cylinder holding **120 bar of 18/46**, topped up to **200 bar with 7/70**, ends up at **13.6 / 55.6** (O₂ / He), with the balance N₂ ≈ 30.8 %. The 80 bar of added 7/70 dilutes the oxygen and pulls the helium fraction up toward the top-up gas; because the result is hypoxic (13.6 % O₂), the app shows it in red.

## Practical tips

- **Always drain or check existing fill.** Even residual gas changes the math.
- **Use a clean analyzer.** Confirm the resulting mix with a calibrated O₂ analyzer (and He analyzer for trimix) before diving.
- **Keep helium first.** Helium is the smallest molecule and diffuses fastest — adding it first lets it equilibrate during subsequent fills.
- **Heat compensation matters more for fast fills.** Slow fills (commercial) have less heat rise; on-site fast fills (e.g., from a fill whip) heat up significantly.

## Reference values

The calculator uses ideal-gas approximations, which are accurate to within ~1 % for pressures up to ~250 bar. Above that, compressibility effects make small differences but are usually within the analyzer's tolerance anyway.

If your facility has a fill master with established procedures, prefer those over the calculator's numbers — they encode local knowledge about specific equipment, gas quality, and historical accuracy.
