# Disclaimer

## Planning calculator only

AeroPlus Deco is a planning calculator. It performs decompression and gas calculations to help you prepare a dive plan **before entering the water**. It is **not a dive computer** and cannot be used during the dive itself — divers must use a certified dive computer for in-water decompression management.

**Always verify calculations against a second planning source** — another planning tool, a dive computer simulation, or a qualified instructor — before relying on them. If the second source disagrees, find out why before you dive.

## What the software does

AeroPlus Deco implements the **Bühlmann ZHL-16C** algorithm with gradient factors — a well-established, widely used dissolved-gas decompression model. The calculations cover:

- Decompression schedules for open-circuit and closed-circuit rebreather profiles
- Gas mix planning (best mix, MOD/EAD/END, density)
- Gas consumption, reserves, and rock-bottom calculations
- CNS and OTU oxygen-exposure totals
- Partial-pressure gas blending

All calculations are based on standard published formulas and inputs you provide. The accuracy of the output depends entirely on the accuracy of those inputs.

## What the software does not do

- It does not measure depth, time, or pressure during a dive
- It does not provide live decompression guidance underwater
- It does not communicate with diving equipment
- It does not diagnose, monitor, treat, or compensate for any medical condition
- It is not a substitute for diver training, certification, or professional instruction

## No warranty

AeroPlus Deco is provided "as is", without warranty of any kind — express or implied — including without limitation any warranty of merchantability, fitness for a particular purpose, or non-infringement. The authors and publisher disclaim all liability for any damages arising from the use or misuse of the software.

By using this software you accept full responsibility for your own diving decisions and acknowledge that the planning output is one input into your decision-making, not a substitute for proper training, equipment, and judgement.

## Not a substitute for training

This documentation explains what the calculator does and how to use it. It does not teach you to dive. Technical diving — including decompression diving, trimix, and rebreather diving — requires:

- Certification by a recognised training agency (TDI, IANTD, GUE, PSAI, NAUI Tec, RAID, etc.)
- Supervised, progressive in-water training
- Mentored experience under qualified instructors
- Ongoing skill maintenance and currency

If you don't hold the certifications appropriate to the dive you're planning, *don't dive it*. Use AeroPlus Deco for study, comparison, or to prepare for training — not to enable diving you aren't qualified for.

## Garbage in, garbage out

The gas calculations in AeroPlus Deco — rock bottom, gas plan, bailout sufficiency — are based on **inputs you provide** (SAC rates, cylinder sizes, fills, emergency rates). Wrong inputs produce wrong outputs. Confirm:

- Cylinder size matches your physical tank (steel vs aluminium, nominal vs actual volume)
- Fill pressure matches the actual gauge reading
- SAC rate reflects your real-world consumption on the dive type you're planning
- Mix percentages match what was analyzed in the cylinder

**Always analyze your gas with a calibrated O₂ analyzer (and helium analyzer for trimix) before diving.** Label cylinders, and follow your team's gas-matching protocol before the dive.

## CCR specifics

Closed-circuit rebreather diving is significantly more complex than open circuit. The CCR planning features assume:

- Correct setpoint values entered for your unit
- Realistic O₂ metabolic rate
- Honest scrubber capacity (typically derated 25–40 % from the manufacturer's figure)
- Bailout cylinders appropriate for your unit and dive plan
- A trained, current CCR diver operating the unit

The bailout sufficiency check is a calculation, not a complete validation — it does not verify that you have the right *type* of gas for the depth ranges involved, only that the volume is sufficient. Verify mix compatibility manually.

## Model conservatism

Gradient factors are personal. The defaults (GF 30/85) are widely cited but not universally appropriate. Choose conservatism based on:

- Your training and your agency's guidance
- Your personal history and physical factors
- Conditions (water temperature, current, exertion expected)
- Time since last dive and recent fatigue
- Hydration, sleep, and general fitness on the day

If in doubt, be more conservative, not less.

## Updates and version stability

This software is under active development. Algorithms, defaults, and UI may change between versions. The version displayed in the app header is your reference for any issue report. Plans saved from older versions should re-import into newer versions, but always verify the output looks correct after an update.

## Reporting issues

If you find a bug, an incorrect calculation, or a regression:

- Use **Help & feedback** in the app to email **support@aeroplus.nl**
- Include the plan share link, browser, version, and a description of what you observed vs expected

Issues affecting calculation correctness are triaged with priority.

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
