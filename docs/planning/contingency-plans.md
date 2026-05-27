# Contingency plans

Every tech dive needs a backup plan for the most common failure modes: going deeper than planned, or staying longer than planned. AeroPlus Deco's contingency toggles re-run the calculation with adjusted parameters so you can see what happens *before* it happens.

## The toggles

At the top of the **Deco plan** card, two buttons appear once a plan is calculated:

- **Deeper +N m** — re-runs the plan with every segment N metres deeper
- **Longer +N min** — re-runs the plan with every segment N minutes longer

Tap either to activate it. The plan card updates to show the contingency profile in place of the original. Tap again to deactivate. The deeper and longer toggles can be combined.

## Configuring the increments

The defaults are 3 m and 3 min — useful for normal tech ops. You can adjust them in **Settings → Contingency plan**:

| Setting | Range | Default |
|---|---|---|
| Deeper | 1–20 m | 3 m |
| Longer | 1–30 min | 3 min |

For instructors planning student dives, larger increments (5 m and 10 min) give a more conservative buffer. For technical exploration, smaller increments give finer resolution.

## What the contingency profile shows

Once a contingency is active, the standard plan output (charts, runtime schedule, gas plan, rock bottom) all show the adjusted profile. Compare:

- **Deco time** — usually 30–80 % longer for a +3 m / +3 min contingency on a typical tech dive
- **TTS** — the bigger number; this is what you'd actually run if the contingency hit
- **Gas usage** — does the dive still fit in your cylinder fills with extra gas required?
- **Rock bottom** — the reserve grows because emergency ascent is from a deeper point

If the contingency plan exceeds your gas budget, increase cylinder fill or reduce planned bottom time.

## When to use which

**Deeper +N m** — when you might overshoot the planned depth:
- Wreck dives where the bottom is uncertain
- Wall dives where you can fall off the edge
- Cavern/cave where depth varies

**Longer +N min** — when you might stay longer:
- Searches or photography
- First-time site visits
- Conditions allow longer than estimated

**Both combined** — for the worst case:
- Penetration dives where the unknown could be deeper *and* longer than planned
- Critical missions where you want to know "what's the absolute upper bound on this dive?"

## Practical workflow

1. Build your **primary plan** as normal
2. Toggle **Deeper +3 m** — verify the dive still works (gas, deco time, CNS)
3. Toggle off Deeper, toggle on **Longer +3 min** — verify again
4. Toggle on both — the *combined* contingency is the worst case
5. Mentally cap your dive at the boundary where the contingency *still* works

If the +3/+3 contingency overshoots your CNS limit or gas budget, you should reduce the primary plan, not just dive without a contingency.

## Saving multiple plans

The Plans bar at the top of the app lets you keep multiple plans side by side. A common pattern:

- **Plan 1** — primary
- **Plan 2** — alternative (different deco gas selection)
- **Plan 3** — contingency / "what if" — manually edit segments

Switch between them with the chips. Each plan has its own settings, gases, and segments.
