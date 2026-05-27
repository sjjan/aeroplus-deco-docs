# Gradient factors

Gradient factors (GFs) are the conservatism controls layered on top of the Bühlmann ZHL-16C decompression algorithm. They're how you tell the planner "be more conservative" or "less conservative" without changing the underlying tissue model.

## The two numbers: GF Low and GF High

The Bühlmann algorithm tracks 16 hypothetical tissue compartments and computes, at any moment, the **maximum tolerated tissue pressure** (the *M-value*) for each compartment at the current depth. The raw model would let you ascend until any compartment hits exactly its M-value — that's 100 % of allowable.

Most divers want a safety margin under that. Gradient factors give you two:

- **GF High (GF Hi)** — the percentage of the M-value tolerated **at the surface**. A GF Hi of 85 means "at the surface, stop ascending if any tissue is at 85 % of its M-value." Lower = more conservative.
- **GF Low (GF Lo)** — the percentage tolerated **at the first decompression stop** (the deepest tissue saturation point of the dive). A GF Lo of 30 means "at the first stop, you may be up to 30 % of the way to the M-value of the leading compartment."

Between the first stop and the surface, the allowed percentage interpolates linearly. Lower GF Lo pushes the first stop deeper; higher GF Lo brings it shallower.

## How to read "GF X/Y"

The conventional notation is `GF Low / GF High`:

- **GF 30/85** — moderately conservative, the default in many computers
- **GF 30/70** — more conservative, often used as a fitter/older diver baseline
- **GF 40/85** — slightly more aggressive deep, same shallow
- **GF 50/80** — common Andy Davis-style setting for typical tech dives
- **GF 100/100** — raw Bühlmann, no extra conservatism (do not dive this)

## Defaults in AeroPlus Deco

The app ships with **GF 30/85** on a fresh plan — a reasonable starting point. You can change them in **Settings → Gradient factor** or via the **Auto-set GF Low** toggle.

## Auto-set GF Low

For OC tech diving, the app can derive GF Lo automatically using the [Andy Davis method](andy-davis-method.md): set GF Lo such that the first decompression stop coincides with the depth where your richest enabled deco gas becomes breathable. This maximises off-gassing efficiency on the deco gas rather than wasting time on back-gas deep stops.

Toggle it on in **Settings → Auto-set GF Low**. The label shows the computed value and the resulting first stop depth.

!!! info "Why not for CCR?"
    Andy Davis explicitly notes the method doesn't apply to CCR — rebreather divers breathe an optimal loop mix throughout, so there's no off-gassing-jump benefit to time. The toggle is greyed out in CCR mode. See the [Andy Davis method](andy-davis-method.md) page.

## Conservatism is personal

There's no universally correct GF setting. DCS susceptibility varies between divers and between days. Cold water, hard work, dehydration, age, and patent foramen ovale all push the curve. Experienced tech divers track how they feel after each dive and tune their GFs gradually.

The Andy Davis article puts it simply: *"Start with a low GFhi and slowly throttle back your conservatism over many, many repeated dives."*

## Practical limits in AeroPlus Deco

- **GF Lo minimum**: 10 (any lower and the model will mandate impractically deep stops)
- **GF Hi maximum**: 100 (raw Bühlmann — strongly discouraged)
- **Minimum delta between GF Lo and GF Hi**: 10. The app enforces this on Auto-set GF Low because a delta below 10 (e.g. 70/75) is theoretical — no tech diver runs that close in practice.

## Further reading

- Andy Davis — [A Logical Application of Gradient Factors for OC Tech Divers](https://scubatechphilippines.com/scuba_blog/gradient-factors-application-use-settings-open-circuit-tech/)
- Erik Baker — *Clearing up the confusion about deep stops* (the original gradient factors paper)
