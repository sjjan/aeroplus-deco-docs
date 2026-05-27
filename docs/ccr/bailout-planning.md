# Bailout planning

A rebreather has more failure modes than open circuit. The single most important contingency is **bailing out to OC** — switching to a backup regulator on a known-good OC gas and ascending without the loop. Bailout planning is non-optional.

AeroPlus Deco supports two bailout modes:

## Independent vs group bailout

### Independent bailout

Each diver carries enough OC gas to ascend solo, from maximum depth, all the way to the surface, including full decompression. The app **validates** this — checking that the bailout cylinders cover the gas required for an OC ascent profile.

**Use when:**

- Solo diving
- Conservative team practice
- Cave or wreck where buddy contact during bailout cannot be guaranteed

**Trade-off:** more gas carried per diver. For deep tech dives this can mean two or three stage cylinders per diver.

### Group bailout

The team carries enough OC bailout collectively to cover any one diver's bailout. Individual divers carry less; the team shares stage drops along the ascent line. The app **does not validate** group totals — that's a planning step done outside the app, usually in a spreadsheet or by manual calculation.

**Use when:**

- Multi-diver teams with team cohesion training
- Long-stage decompression dives where independent bailout is impractical
- Diving with surface support (boats with deco stations)

**Trade-off:** lower individual load but planning is more complex and requires team discipline.

A yellow warning banner appears when Group is selected to remind you: *"AeroPlus Deco does not validate group gas totals. Ensure surface support and pre-staged deco stations are confirmed before the dive."*

## Configuring bailout

In the **Closed Circuit Setup** card on the main plan page, the bailout mode selector switches between Independent and Group. Below it, the bailout cylinders are listed (from the Gas & cylinders card, role = `bailout`).

Add bailout cylinders just like any other gas: tap **+ Add** in the Gas & cylinders card and choose **Bailout gas** as the role.

## What the bailout sufficiency check covers

When **Independent** mode is active, the algorithm:

1. Constructs a hypothetical bailout OC profile — same depths, same segments, but the diver is on OC gas throughout
2. Picks the richest available bailout gas at each depth (respecting MOD)
3. Computes the gas required by each bailout cylinder for the planned profile
4. Adds the rock-bottom reserve for two divers at max depth (same as bottom-gas rock bottom)
5. Compares to the fill in each cylinder
6. If short, raises a "**Bailout shortfall**" warning

If the warning appears, your bailout cylinders are not large enough for an independent OC ascent. Options:

- **Larger bailout cylinders** (12 ℓ instead of 11 ℓ, for example)
- **Higher fill pressures** (300 bar twins for the deepest bailout)
- **More bailout cylinders** (add a deeper bailout mix to reduce the depth range each cylinder must cover)
- **Switch to group mode** if team practice supports it

## Bailout switch time

In **Settings → CCR → Bailout switch time** (default 2 min), this is the mandatory pause when bailing out from the loop to OC. The 2 min adds to:

- The bailout gas requirement (you breathe OC at higher SAC during the pause)
- The runtime if the algorithm is computing a bailout scenario

Most agencies teach a 1–2 minute switch sequence (close DSV, switch to BOV or alternate regulator, verify, begin breathing OC). Tune to your team's practice.

## Reading the bailout output

The **Gas plan** card lists bailout cylinders alongside others. Bailout-role cylinders are labeled and the bars show:

- **Used** (blue) — gas the algorithm expects you'd use during a bailout from max depth
- **Reserve** (red) — minimum gas to keep at end of bailout (matches rock-bottom logic)
- **Unused** (grey) — surplus

In group mode, the Used and Reserve are computed as if you bailed out independently from max depth — even though in practice the team's collective gas absorbs the requirement.

## Practical CCR bailout configurations

### Recreational CCR (40 m max)

- 1 × 11 ℓ AL with 32/0 or 50/0 (covers entire ascent)

### Sport tech CCR (60–80 m)

- 1 × 11 ℓ AL with 21/35 (bottom phase + travel)
- 1 × 11 ℓ AL with 50/0 (deco 21 m up)
- Optional: 1 × 5.5 ℓ AL with 100/0 (deco 6 m)

### Heavy tech CCR (100 m+)

- 1 × 11 ℓ AL with 16/55 hypoxic trimix (bottom phase, matches loop)
- 1 × 11 ℓ AL with 21/35 travel
- 1 × 11 ℓ AL with 50/0
- 1 × 5.5 ℓ AL with 100/0
- Or some combination using doubles and stages

## CCR bailout in the runtime schedule

The runtime schedule doesn't show bailout gases in the normal **Gas** column — the planned dive is on the loop. Bailout details are visible only in:

- The **Gas plan card → bailout cylinder bars**
- The **Critical warnings** if a shortfall is detected
- An informational note if Group mode is selected
