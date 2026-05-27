# Dive profile

The **Dive profile** card defines the actual dive — what depths you're going to, how long at each, and which gas you'll breathe on the way.

## Single-level dive

Most tech dives are square-profile: descend, hold at depth, ascend. Add one segment:

| Field | Value |
|---|---|
| Depth (m) | the deepest depth |
| Bottom time (min) | total dive time *from leaving the surface to leaving the bottom* |

!!! note "Bottom time includes descent"
    The bottom time you enter includes descent time to that depth. If you want exactly 20 min on the bottom after a 4-min descent, enter 24 min. The runtime schedule will show descent and hold separately.

The gas selector defaults to your first bottom-role cylinder. If you have multiple bottom gases, you can override.

## Multi-level dive

For a dive that visits multiple depths, add a segment for each. Segments are processed in order, top to bottom.

Example: a wreck dive that visits 45 m for 20 min, then 35 m for 10 min, then 25 m for 5 min before ascending:

| # | Depth | Time | Gas |
|---|---|---|---|
| 1 | 45 | 20 | 21/35 trimix |
| 2 | 35 | 10 | 21/35 trimix |
| 3 | 25 | 5 | 21/35 trimix |

The algorithm tracks tissue saturation across all segments before computing the final ascent.

### Going deeper later in the dive

Multi-level dives can also go *deeper* after a shallow start — useful for cavern/cave divers and certain wreck profiles. Just add the segments in the order you'll dive them.

The algorithm handles the depth transitions, but be aware:

- Re-descent after off-gassing reloads slow tissues
- Plan output reflects this; the GF99 chart will show on-gassing dips
- Deco obligation grows more than a square profile of the same maximum depth

## Segment ordering

Segments are dived in the order they appear in the list. To re-order, you currently need to delete and re-add. (Future feature: drag handles.)

## Multiple bottom gases

If you have multiple bottom-role cylinders, you can choose which one each segment uses via the Gas dropdown. This is unusual for OC tech (most dives use a single bottom mix) but useful for:

- Multi-bottle setups with different mixes for different depths
- "Bailout to OC" comparisons during plan validation
- Comparing how the deco changes with a richer / leaner bottom mix

## Deco gas between sections

In multi-level dives, between sections you might ascend — and during that ascent, the algorithm could theoretically switch to a deco gas if its MOD is reached. Whether to allow this is controlled by **Settings → Use deco gas between sections**:

- **On (default)** — auto-switch to deco gas on inter-section ascents when MOD is reached
- **Off** — stay on bottom gas across all sections; deco gas only used during the final ascent

Most tech plans leave this on. Turn it off only if you have a specific reason (e.g., conserving deco gas for the final ascent).

## Auto-assigned gas IDs

When a segment's referenced gas is deleted, the segment is **auto-healed** on the next render — it gets reassigned to the first available bottom gas. The plan is saved and the calculated result is invalidated, so you'll be prompted to recalculate.

If no cylinders exist at all, the segment row shows "no gas — tap to assign" in orange. Add a cylinder first, then re-edit the segment.

## Editing a segment

Tap the segment row to re-open the editor. Save updates the existing entry.

## Deleting a segment

Tap the trash icon to the right of the row. The action is immediate (no confirmation) — re-add if needed.

## Practical patterns

### Reef tech dive

```
40 m for 25 min on 21/0
```

Single segment, deco on 50/0 + 100/0. The simplest, cleanest plan.

### Wreck penetration

```
35 m for 20 min on 21/0      (descent + penetration time)
35 m for 5 min on 21/0       (exit + reserve time)
```

Splitting the dive into "in" and "out" lets you check gas usage at the split. (Functionally the same as a single 25-min segment, but more visible in the runtime schedule.)

### Drift dive with mid-depth stop

```
60 m for 18 min on 18/45
40 m for 12 min on 18/45
```

A two-stage drift where you spend time at depth, then move up to a shallower part of the wall.
