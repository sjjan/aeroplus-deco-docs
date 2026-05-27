# Disclaimer

## Plan with care, dive with judgement

AeroPlus Deco is a decompression planning aid. It is not a substitute for proper training, qualified supervision, or sound judgement underwater. Decompression diving carries serious, sometimes fatal risk. The output of this software is a *plan*, not a guarantee.

**Always cross-check every plan against a second source** — a separate planning tool, a dive computer simulation, or a qualified instructor. If the second source disagrees, find out why before you dive.

## Software limitations

AeroPlus Deco implements the **Bühlmann ZHL-16C** algorithm with gradient factors. This is a well-validated, widely used dissolved-gas model — but it is still a model. The actual physiology of decompression varies between divers and between dives for the same diver. The model:

- Does not account for individual physiology (age, fitness, PFO, dehydration, recent injury)
- Does not model micro-bubbles or venous gas emboli directly
- Assumes idealised tissue compartments and constant respiratory exchange
- Cannot predict outliers — *any* dive within model limits can still result in DCS

The app's gas density, CNS, OTU, and rock-bottom calculations are based on standard formulas and published guidelines. They are conservative starting points, not absolute safety limits.

## No warranty

AeroPlus Deco is provided "as is", without warranty of any kind — express or implied — including without limitation any warranty of merchantability, fitness for a particular purpose, or non-infringement. The authors and publisher disclaim all liability for any damages arising from the use or misuse of the software, including but not limited to:

- Decompression injuries (Type I or Type II DCS, AGE, oxygen toxicity)
- Equipment failures or gas planning errors
- Economic loss from cancelled or modified dives
- Any other direct or consequential harm

By using this software you accept full responsibility for your own diving decisions.

## Not a substitute for training

This documentation explains what the app does and how to use it. It does not teach you to dive. Technical diving — including decompression diving, trimix, and rebreather diving — requires:

- Certification by a recognised training agency (TDI, IANTD, GUE, PSAI, NAUI Tec, RAID, etc.)
- Supervised, progressive in-water training
- Mentored experience under qualified instructors
- Ongoing skill maintenance

If you don't hold the certifications appropriate to the dive you're planning, *don't dive it*. Use AeroPlus Deco for study, comparison, or to prepare for training — not to enable diving you aren't qualified for.

## Mind your gas

The gas calculations in AeroPlus Deco — rock bottom, gas plan, bailout sufficiency — are based on **input you provide** (SAC rates, cylinder sizes, fills, emergency rates). If your inputs are wrong, the outputs are wrong. Confirm:

- Cylinder size is correct for your physical tank (steel vs aluminium, common nominal vs actual volume)
- Fill pressure matches the actual gauge reading
- SAC rate reflects your real-world consumption on the dive type you're planning
- Mix percentages match what was analyzed in the cylinder

**Always analyze your gas with a calibrated O₂ analyzer (and helium analyzer for trimix) before diving.** Label cylinders, and follow your team's gas-matching protocol before the dive.

## CCR specifics

Closed-circuit rebreather diving adds significant complexity and additional failure modes beyond OC. The CCR planning features in AeroPlus Deco assume:

- Correct setpoint values entered for your unit
- Realistic O₂ metabolic rate
- Honest scrubber capacity (typically derated 25–40 % from the manufacturer's figure)
- Bailout cylinders appropriate for your unit and dive plan
- A trained, current CCR diver operating the unit

The bailout sufficiency check is a model — it does not validate that you have the right *type* of gas for the depth ranges involved, only that the volume is sufficient. Verify mix compatibility manually.

## Model conservatism

Gradient factors are personal. The defaults (GF 30/85) are widely cited but not universally appropriate. Choose conservatism based on:

- Your training and your agency's guidance
- Your personal DCS history and risk factors
- Conditions (water temperature, current, exertion expected)
- Time since last dive and recent fatigue
- Hydration, sleep, and general fitness on the day

If in doubt, be more conservative, not less. There is no decompression schedule that cannot be made safer by adding margin.

## Updates and version stability

This software is under active development. Algorithms, defaults, and UI may change between versions. The version displayed in the app header is your reference for any issue report. Plans saved from older versions should re-import into newer versions, but always verify the output looks correct after an update.

## Reporting issues

If you find a bug, an incorrect calculation, or a regression that affects safety:

- Use **Help & feedback** in the app to email **support@aeroplus.nl**
- Include the plan share link, browser, version, and a description of what you observed vs expected

Safety-relevant issues will be triaged with priority. Critical fixes get out as soon as practical.

## Privacy

AeroPlus Deco does not collect personal data, analytics, or telemetry. Your plans, settings, and license details stay on your device unless you explicitly share them via a link, PDF, or JSON export.

Network requests are made only:

- To load the app initially (sjjan.github.io)
- To activate or deactivate a license (api.polar.sh)
- When you click external links (e.g. references in the About page)

## Copyright

AeroPlus Deco © Magnolia Blossom BV, Doesburg, The Netherlands. All rights reserved.

Documentation © Magnolia Blossom BV. The source text of this documentation may be reproduced for personal study; redistribution requires permission.

The Bühlmann ZHL-16C algorithm is in the public domain (Bühlmann, *Tauchmedizin*). The gradient factor extension is attributed to Erik C. Baker.

## Contact

Email: **[support@aeroplus.nl](mailto:support@aeroplus.nl)**

Bug reports & feature requests: **[github.com/sjjan/aeroplus-deco/issues](https://github.com/sjjan/aeroplus-deco/issues)**

---

By using AeroPlus Deco, you acknowledge that you have read and understood this disclaimer and accept responsibility for your own diving decisions.
