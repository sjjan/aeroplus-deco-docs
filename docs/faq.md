# FAQ

Common questions and answers. If your question isn't here, try the relevant concept or planning page, or use **Help & feedback** in the app to email support.

## General

### Is AeroPlus Deco a substitute for a dive computer?

**No.** AeroPlus Deco is a planning tool. Your dive computer is the live decision-maker during the dive. Always cross-check both, and trust the computer (and your training) when they disagree mid-dive.

### Which decompression algorithm does it use?

**Bühlmann ZHL-16C** with gradient factors (GF). This is the same model used by Shearwater (their default), Liquivision, OSTC, and many other tech computers, so AeroPlus Deco's output should align closely with what your computer shows.

### Why doesn't AeroPlus Deco support VPM-B or RGBM?

ZHL-16C-GF is the most validated, most reviewed, and most widely understood tech model. Adding alternative models introduces complexity, more places to disagree with other planners, and more diver confusion. We may add VPM-B in the future but it's not a near-term priority.

### Does the app collect any data?

**No.** No analytics, no tracking, no telemetry. The only network traffic is:

- Loading the app (sjjan.github.io)
- License activation/deactivation (Polar API)
- Clicking external links you initiate

Your plans, settings, and license details stay in your browser's localStorage.

---

## Planning

### Why does my first deco stop appear deeper than I'd expect?

The default GF 50/75 already produces a relatively shallow first stop — in line with modern post-NEDU tech practice. If you still want it shallower (so it coincides exactly with your first deco gas switch), use the **Auto-set GF Low** toggle, which derives the optimal value for your specific gas plan via the [Andy Davis method](concepts/andy-davis-method.md). Going below GF Low ~35 mandates a deep stop without scientific justification — see [Gradient factors](concepts/gradient-factors.md#why-deep-stops-fell-out-of-favor).

### What's the difference between "Total deco time" and "TTS at ascent start"?

- **Total deco time** is just the sum of stop durations (excluding ascent time between stops).
- **TTS at ascent start** is the entire time from leaving the deepest point to the surface, including all ascents.

TTS is the more practically relevant number — it's what your dive computer shows you on ascent.

### The Auto-set GF Low setting moved my first stop to 30 m, but my gas switch is at 21 m. Why?

The dive is heavy enough (deep, long, helium-rich) that even at the most aggressive practical GF Low, the model still wants a stop deeper than your richest deco gas's MOD. The fix per Andy Davis is to add an **intermediate travel gas** (e.g., EAN30 with MOD ~30 m) so the natural first stop coincides with a switch.

See the [Andy Davis method](concepts/andy-davis-method.md) page.

### Can I set GF Low higher than 70?

Yes — manually, in Settings → Gradient factor. The Auto-set GF Low feature caps at GF Hi − 10 to enforce a minimum 10% delta (a practical safety floor), but you can override manually if you have a specific reason.

### Why is my gas plan showing the dive eats into the reserve?

The **red Reserve** bar in the gas plan card shows what's left of the rock-bottom reserve after the dive. If it's smaller than the calculated rock-bottom value, your dive consumes more than the cylinder can safely hold while preserving the reserve. Options:

- Bigger cylinder
- Higher fill pressure
- Shorter dive time
- Add a stage cylinder of the same mix

---

## Multi-dive / surface intervals

### Does the app track repetitive dives?

Yes. The **Surface interval card** lets you tell the app how long you've been on the surface since the previous dive. Tissue saturation, CNS, OTU, and scrubber/O₂ tracking all carry over.

### Where do I enter the surface interval?

When a previous dive in the same plans-bar exists, the Surface interval card appears at the top of the plan. Enter hours and minutes since surfacing.

### Can I plan back-to-back dives across days?

Yes — long surface intervals are supported. The tissue model will return to baseline within ~24 hours, but CNS, OTU, and scrubber use take longer.

---

## CCR

### Why is Auto-set GF Low greyed out in CCR mode?

Andy Davis's method explicitly doesn't apply to CCR — rebreather divers breathe an optimal mix throughout, so there's no "off-gassing jump" at gas switches that need to be matched to a first stop. See [Andy Davis method → Why this doesn't apply to CCR](concepts/andy-davis-method.md#why-this-doesnt-apply-to-ccr).

### How do I set up bailout cylinders?

Add cylinders with the **bailout** role in the Gas & cylinders card. Choose between Independent and Group bailout modes in the Closed Circuit Setup card. See [Bailout planning](ccr/bailout-planning.md).

### Why doesn't the runtime schedule show bailout gases?

Bailout is contingency only — the planned dive uses the loop. The runtime schedule shows what you'll actually breathe; bailout is in the gas plan card for reference and sufficiency checks.

---

## Tools

### Best mix shows a different result than I expected — why?

Common reasons:

- **Limit gas density is on** — adds more helium than narcosis alone requires
- **Trimix is off** — only an O₂ % is computed, no helium
- **Salinity or altitude differs** — affects absolute pressure at depth

Double-check the toggles and settings at the top of the calculator.

### What's the difference between EAD and END?

- **EAD** treats only nitrogen as narcotic (most agencies' standard)
- **END** treats both nitrogen and oxygen as narcotic (GUE method)

EAD is always deeper than END for the same mix. Use whichever your training prescribes.

---

## Sharing & backup

### My buddy can't open my shared link

Make sure:

1. They have a recent browser (Safari 14+, Chrome/Edge 90+)
2. The link is complete (no truncation in messaging apps; the `#p=...` portion should be very long)
3. If pasting, the link is uninterrupted (no line breaks)

Try the **Import from link** option in their app — paste the URL into the input there.

### Can I edit a buddy's plan and send it back?

Yes. Import their link, modify the plan (cylinders, segments, settings), then share your modified version. The original sender's plan isn't affected.

### How do I export/import all my plans at once?

Use the JSON backup feature: **App menu → Share or back up → Save data** generates a complete JSON of all plans. **App menu → Import or restore → Load data** restores from JSON. See [Sharing & backup](planning/sharing-and-backup.md).

---

## Errors and bugs

### A calculation crashes or shows weird numbers

Use **Help & feedback** in the app to email support@aeroplus-deco.com with:

- A description of what you did
- The plan share link (you can toggle "Include current plan" when you email)
- Your browser and OS

Most issues are reproducible from the share link.

### The app feels stuck or won't recalculate

Try:

1. Tap **Calculate** again to retry
2. Switch to another plan tab and back
3. Refresh the browser tab
4. If installed as PWA, force-quit and reopen

If the issue persists, file a feedback email — include the plan link.

### I lost my plans after updating the browser

This shouldn't happen normally, but browser data clearing or updates can occasionally wipe localStorage. **Always keep a JSON backup** of critical plans (Share or back up → Save data).

---

## Other

### Can I use the app on multiple devices?

Yes — your license activates up to 3 devices. Plans don't sync automatically between devices; use share links or JSON export/import to move them.

### Does the app work in Imperial units (feet, psi)?

Not currently. AeroPlus Deco uses metric throughout. If demand is significant, an imperial option may be added — file feedback.

### Where can I see what changed in the latest version?

Check the **[GitHub Issues](https://github.com/sjjan/aeroplus-deco/issues)** page (linked from Help & feedback) for the roadmap and resolved issues.
