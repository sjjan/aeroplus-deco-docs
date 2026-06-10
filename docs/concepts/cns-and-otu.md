# CNS & OTU

Oxygen at elevated partial pressures is toxic to the body in two distinct ways. AeroPlus Deco tracks both.

## CNS — central nervous system toxicity

**CNS oxygen toxicity** is the acute risk — it scales with **PPO₂ at depth** and time exposed, and is the reason why deco gases have maximum operating depths.

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

CNS recovers exponentially during the surface interval — see [Surface recovery](#surface-recovery-the-90-minute-half-time) below. AeroPlus Deco accounts for this when chaining repetitive plans.

### Surface recovery — the 90-minute half-time

Once you leave the water and breathe normal air, your CNS loading begins to fall. The convention used throughout technical diving is an **exponential decay with a half-time of about 90 minutes**: every 90 minutes on the surface, the CNS figure roughly halves.

| Time on surface | CNS, starting from 80 % |
|---|---|
| 0 min (surfacing) | 80 % |
| 90 min | 40 % |
| 180 min | 20 % |
| 270 min | 10 % |

After roughly 24 hours the residual loading is treated as fully cleared (reset to zero).

!!! note "A convention, not hard science"
    The 90-minute half-time is widely used — Shearwater computers, the Erik Baker oxygen-toxicity equations, and most planners all apply it — but, like the CNS clock itself, it rests on a thin experimental basis rather than direct evidence. Treat the recovered figure as a planning estimate, in the same spirit as the rest of this page.

**In AeroPlus Deco.** When you chain repetitive plans, the **Previous dive** card lets you enter your surface interval. The app decays the previous dive's surfacing CNS by the 90-minute half-time and carries the reduced value into the next plan as its starting CNS — and now also **shows that recovery on the card** (e.g. *"CNS recovery: 80 % → 40 % after this surface interval"*), so you can see the drop directly. OTU is handled separately and recovers far more slowly (see below).

### How strict are these limits? (2025 revision)

The CNS percentages above derive from NOAA's 1991 exposure tables. It's worth understanding how those numbers came about, because the field's thinking has moved on.

The 1991 limits were conservative guidelines, not values derived from direct empirical evidence of seizure risk. In practice, technical divers have routinely exceeded them without apparent ill effect — which prompted a formal re-examination.

In March 2025, a NOAA-convened expert workshop (held at the AAUS Annual Meeting, ~60 technical and scientific divers participating) reviewed the evidence and published revised guidance. The key conclusions, **specifically for an inspired PO₂ of 1.3 atm**:

- Dives at PO₂ 1.3 atm of up to **240 minutes of working activity followed by up to 240 minutes of resting decompression** carry an acceptably low risk of cerebral oxygen toxicity — substantially more permissive than the old 180 min/dive figure.
- For very long exposures, **pulmonary (OTU) toxicity becomes the controlling factor** rather than CNS — but pulmonary toxicity is generally reversible.
- NOAA has indicated it intends to adopt these revised limits in future editions of its Diving Manual.

!!! note "Important scope limitation"
    The 2025 revision applies **specifically to PO₂ 1.3 atm** — the common CCR bottom setpoint. The authors deliberately did not extend it to other PO₂ values, because the supporting evidence exists only at 1.3 atm. The general observation that CNS toxicity is rare below 1.6 atm is a separate, older finding and should not be conflated with the 2025 guideline. At higher PO₂ (e.g. 1.6 on a rich deco gas), treat the classic NOAA limits as still applicable.

The practical takeaway: the CNS clock is a useful planning indicator, not a hard physiological cliff. Assess your exposure in context of your actual PO₂, dive history, and individual risk factors — and don't treat a CNS figure approaching 100 % at a 1.3 setpoint as the emergency the 1991 tables once implied.

### Choosing which limits the app uses

AeroPlus Deco lets you pick which limits drive the CNS calculation, in **Settings → Use 2025 revised CNS limits**:

- **Off (default)** — the conservative 1991 NOAA tables. CNS accumulates at the classic rates (1.3 ata → 180 min to 100 %).
- **On** — the 2025 revised limits. At PO₂ **1.3 ata and below**, the single-exposure limit becomes **240 minutes** (1.3 ata → 240 min to 100 %). PO₂ **above 1.3** keeps the conservative 1991 values, matching the scope of the research.

Switching the toggle recalculates the active plan immediately. The CNS note shown in the plan output always states which set of limits produced the figure, so the two never disagree.

A worked comparison at a constant 1.3 ata CCR setpoint:

| Time at 1.3 ata | CNS (1991) | CNS (2025 revised) |
|---|---|---|
| 180 min | 100 % | 75 % |
| 240 min | 133 % | 100 % |

Note that rich deco gases (e.g. 1.6 ata) produce identical CNS in both modes — the revision only relaxes the 1.3 ata region.

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

## How to read the CNS % and OTU figures

AeroPlus Deco always shows your CNS % and OTU, and these values can't be turned off. They're useful situational awareness — but, as the [2025 revision](#how-strict-are-these-limits-2025-revision) above makes clear, they are **planning estimates rather than exact, science-based hard limits** — especially the CNS percentage.

!!! note 'The CNS "clock" may not rest on hard science'
    The cumulative CNS % derives from a small, old and highly variable body of data, and there is a growing view in technical diving that the way it is calculated is not well validated — so the number may be telling you less than it appears to. For a clear first-hand discussion, see *"Oxygen CNS Calculations: Are They Worth It?"* (Deep Wreck Diver): [https://youtu.be/TT9sN4JxNcE](https://youtu.be/TT9sN4JxNcE). The short version: many experienced divers treat the CNS figure as background information and instead manage the thing that actually drives the risk — their **PO₂**.

To put the numbers in perspective, divers doing very long closed-circuit dives routinely record figures far beyond the conventional limits with no acute problems. On a typical **12–14 hour** cave dive, one diver reported:

| Quantity | On the dive | Conventional "limit" |
|---|---|---|
| CNS oxygen toxicity | **200–300 %** | 100 % |
| OTU (pulmonary dose) | **over 1,000** | ~300 / day |
| Symptoms | none acute; occasional mild chest "tenderness" | — |

Such dives are made workable with a modest setpoint, redundant rebreathers, and an in-water habitat for the long decompression. The CNS figure (2–3× the "limit", no event) is the clearest reason the cumulative clock is seen as conservative and weakly predictive. The OTU figure behaves more as expected — a high dose produced a measurable but reversible, low-stakes effect — which makes OTU the better-grounded of the two.

**What does not change.** Oxygen toxicity itself is real and serious: a CNS hit is an underwater convulsion, usually fatal, and individual susceptibility varies widely, so no number makes the risk zero. The takeaway is not to ignore oxygen — it is to manage your **working PO₂** directly: keep it modest, avoid spikes, and don't let a comfortable (or an alarming) CNS % make the decision for you.

**Bottom line in this app.** The CNS % and OTU values are always on screen and cannot be hidden — but you can treat them as guidance and situational awareness rather than an exact, science-based hard ceiling. Watch your PO₂, accept that people differ, and use the CNS % as one soft input among several.

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

- Hoyt, J. T., Murphy, F. G., Pollock, N. W., Kernagis, D., Bird, N., Menduno, M., Bright, J., & Mitchell, S. J. (2025). *Revised guideline for central nervous system oxygen toxicity exposure limits when using an inspired PO₂ of 1.3 atmospheres.* Diving and Hyperbaric Medicine, 55(3), 262–270.
- NOAA — *Diving Manual* (CNS and OTU tables)
- Deep Wreck Diver — *Oxygen CNS Calculations: Are They Worth It?* ([https://youtu.be/TT9sN4JxNcE](https://youtu.be/TT9sN4JxNcE)) — first-hand discussion of why the CNS clock is treated as soft guidance
- IANTD — *Encyclopedia of Technical Diving*
