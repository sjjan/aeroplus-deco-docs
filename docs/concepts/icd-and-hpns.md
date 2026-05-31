# Isobaric counterdiffusion & HPNS

Once you are diving on helium and switching gases on the way up, two deep-diving phenomena come up that a Bühlmann model **cannot** calculate for you: isobaric counterdiffusion (ICD) and high-pressure nervous syndrome (HPNS). This page explains what they are, how settled (or unsettled) the science is, and exactly what AeroPlus Deco does — and deliberately does not do — about each.

## Isobaric counterdiffusion (ICD)

### What it is

"Isobaric" means *at constant pressure*. ICD is what happens when two different inert gases move in **opposite** directions across your tissues without any change in depth. The case that matters for planning is a decompression gas switch from a helium-rich mix to a nitrogen-rich one — for example leaving a trimix bottom gas for a nitrox deco gas.

When you make that switch, helium starts washing **out** of a tissue while nitrogen washes **in**. Because the two gases have different solubilities and diffusion rates, the nitrogen can load in faster than the helium clears. For a short period the *sum* of dissolved inert-gas tensions in the tissue can rise **above** the ambient pressure — transient supersaturation, and potentially bubbles, with no ascent at all. This is sometimes called a **"nitrogen slam."**

The inner ear is thought to be especially vulnerable, which is why the clinical concern is **inner-ear decompression sickness (IEDCS)** — vertigo, nausea, hearing changes — sometimes appearing during or shortly after a deep gas switch.

### How settled is the science?

Less than you might expect, and it is worth being honest about that:

- The mechanism is plausible and has been modelled. Doolette & Mitchell built a compartmental model of the inner ear and showed that a helium-to-nitrogen switch *can* produce transient supersaturation in inner-ear tissue even without decompression.
- But the same line of work also shows the inner ear is **not well described by the standard whole-body algorithms** (Bühlmann included). So the model your planner runs on does not "see" the inner ear at all.
- The real-world *contribution* of the gas switch itself is debated. More recent commentary from the same researchers suggests helium-to-nitrogen switches may play only a **minor** role in IEDCS, with factors such as a right-to-left shunt (e.g. a PFO) and overall decompression stress mattering more.
- There is **no single agreed numerical rule**. Various heuristics circulate (limit the size of the nitrogen jump; make nitrogen-rich switches shallower; the so-called "rule of fifths"), but none is authoritative, and different agencies treat ICD as anything from a core operational concern to a minor footnote.

!!! note "The bottom line on ICD"
    A real phenomenon, an uncertain magnitude, and **not** something a decompression model can compute. Treat any ICD guidance — including this app's — as an advisory prompt to think, not a calculated risk.

### How AeroPlus Deco handles it

AeroPlus Deco cannot *calculate* ICD risk, so it does not pretend to. What it can do is recognise a **switch profile** that the literature associates with ICD and prompt you to look at it. Because the underlying ZHL-16C model tracks helium and nitrogen **separately** in every compartment, the planner already has the numbers it needs.

The app raises a **Note** (the soft blue "Notes for this plan" panel — *not* a red/amber warning) when an open-circuit gas switch meets **all** of the following:

- you are leaving a **helium-containing** mix;
- the switch **increases** the nitrogen fraction;
- it happens **deeper than 24 m**; and
- the resulting rise in inspired nitrogen partial pressure **at that depth** is roughly **0.5 ata or more**.

That last condition is the important one: it scales the trigger by depth automatically, so a big nitrogen jump is judged by its actual pressure swing rather than by the percentage change alone.

!!! info "What it will *not* flag"
    The standard tech deco switches — **EAN50 at 21 m** and **100 % O₂ at 6 m** — are accepted, near-universal practice. They sit shallower than the 24 m gate, so they will **never** trigger the note, even from a helium-rich bottom mix like 15/55. The note is reserved for genuinely unusual choices, such as dropping to an intermediate nitrogen-rich trimix, or toward air, at a deep stop (e.g. 35–45 m).

The note names the switch and the computed nitrogen jump, e.g. *"switching from 10/70 to 21/35 at 45 m raises inspired N₂ by about 1.33 ata… consider a smaller nitrogen step or a shallower switch."*

**Scope:** the check is **open-circuit only**. On a closed-circuit rebreather you stay on the loop and the loop's inert content changes gradually with setpoint and diluent — there is no abrupt breathing-gas swap to counter-diffuse. (CCR *bailout* switches are a possible future extension.)

### Practical guidance

- Keep using the standard switches (50 % at 21 m, O₂ at 6 m). Nothing here changes that.
- If you are planning an intermediate deco gas at a deep stop, prefer a **smaller** step up in nitrogen, or make the nitrogen-rich switch **shallower** where it is safe to do so.
- If you have a known PFO or a history of inner-ear symptoms, this is a topic to discuss with a diving physician rather than a planner.

## High-pressure nervous syndrome (HPNS)

### What it is

HPNS (also "high-pressure neurological syndrome") is a direct effect of high ambient **pressure** on the central nervous system — not a gas-loading or decompression effect. Below roughly **150 m** on helium-based mixes, hydrostatic pressure begins to interfere with nerve-cell membranes and signalling, producing fine tremors (classically of the hands), dizziness, nausea, drowsiness, and measurable drops in performance, along with characteristic EEG changes. First described as "helium tremors" in the 1960s.

Two things drive it: the **absolute depth** and the **rate of compression** — faster descents bring on symptoms shallower and more severely. The effects are reversible on ascent. Mitigations are operational, not algorithmic: slow, staged compression with holds, and adding a little nitrogen back into the helium mix (its mild narcotic effect partially offsets HPNS — one reason very deep mixes are trimix rather than pure heliox).

### How AeroPlus Deco handles it

**Nothing — by design.** HPNS is outside the scope of this planner, for two reasons:

1. It is **not a decompression quantity**. It is a pressure-on-nerves effect, so there is nothing for a Bühlmann-based model to compute and nothing meaningful to display.
2. It only becomes relevant **below ~150 m on helium**, which is exploration / saturation territory well beyond the range of essentially all of this app's users.

If you are genuinely planning beyond ~150 m, HPNS and compression-rate management become real considerations — but they belong to a class of diving (with its own team, gases, and procedures) that a single-diver planner like AeroPlus Deco is not designed to support.

## Further reading

- Doolette, D. J., & Mitchell, S. J. (2003). *Biophysical basis for inner ear decompression sickness.* J Appl Physiol 94(6): 2145–2150. [PubMed](https://pubmed.ncbi.nlm.nih.gov/12562679/) · [full text](https://journals.physiology.org/doi/full/10.1152/japplphysiol.01090.2002)
- Wikipedia — [Isobaric counterdiffusion](https://en.wikipedia.org/wiki/Isobaric_counterdiffusion) and [Inner ear decompression sickness](https://en.wikipedia.org/wiki/Inner_ear_decompression_sickness)
- StatPearls (NCBI) — [Inner Ear Decompression Sickness](https://www.ncbi.nlm.nih.gov/books/NBK557694/)
- InDEPTH — [How two tech agencies address isobaric counterdiffusion](https://indepthmag.com/how-two-tech-agencies-address-isobaric-counterdiffusion/) and [Isobaric counterdiffusion in the real world](https://indepthmag.com/isobaric-counterdiffusion-in-the-real-world/)
- The Theoretical Diver — [Isobaric counter-diffusion criteria](https://thetheoreticaldiver.org/wordpress/index.php/2018/01/24/isobaric-counter-diffusion-criteria/)
- Wikipedia — [High-pressure nervous syndrome](https://en.wikipedia.org/wiki/High-pressure_nervous_syndrome) · StatPearls (NCBI) — [High-Pressure Neurological Syndrome](https://www.ncbi.nlm.nih.gov/books/NBK513359/)
- InDEPTH — [High pressure problems on über-deep dives: dealing with HPNS](https://indepthmag.com/high-pressure-problems-on-uber-deep-dives-dealing-with-hpns/)

!!! warning "Not medical or dive-planning advice"
    This page summarises a contested area of diving physiology for context. It is not medical advice, and AeroPlus Deco's ICD note is an advisory prompt, not a validated risk calculation. Always plan within your training and consult a diving physician for medical questions.
