# CCR diving

CCR (Closed Circuit Rebreather) mode in AeroPlus Deco supports setpoint-based dive planning, scrubber endurance tracking, O₂ consumption monitoring, and bailout sufficiency checks.

When CCR mode is active:

- The deco algorithm uses a **constant loop O₂ partial pressure** (the setpoint) instead of a fixed gas mix
- Cylinder roles change to **diluent**, **oxygen**, and **bailout**
- A second card appears for **setpoints, scrubber, and bailout configuration**
- Many gas-related warnings and calculations adjust accordingly

## In this section

- **[Setup](setup.md)** — activating CCR mode and configuring cylinders
- **[Setpoints](setpoints.md)** — surface SP, switch depth, bottom SP, deco SP, per-segment override
- **[Bailout planning](bailout-planning.md)** — independent vs group bailout, sufficiency check
- **[Oxygen & scrubber](oxygen-and-scrubber.md)** — O₂ consumption tracking and scrubber endurance

## Key differences from OC

| Aspect | OC | CCR |
|---|---|---|
| Breathing gas at depth | Bottom-gas cylinder mix | Loop mix (varies with setpoint and depth) |
| Deco gas switches | Yes — at MOD of each deco gas | No — setpoint changes only |
| Gradient factor strategy | Andy Davis method recommended | Personal/agency preference |
| Auto-set GF Low | Available | Disabled (greyed out) |
| Bailout consideration | N/A | Critical — independent or group |
| Scrubber tracking | N/A | Per-dive duration on scrubber |
| O₂ tracking | N/A | Cylinder fill and metabolic consumption |

## Switching modes

In **Settings → CCR mode**, toggle the switch. The app:

1. Saves your current OC cylinder configuration
2. Restores your previous CCR cylinders (or creates default diluent + O₂ + bailout if first time)
3. Re-renders the cylinders list with CCR roles
4. Shows the CCR setup card on the main plan page
5. Recalculates if a plan already existed

Toggling back to OC reverses this. Both configurations are preserved per plan, so you can compare OC and CCR profiles for the same dive site.
