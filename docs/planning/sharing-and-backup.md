# Sharing & backup

AeroPlus Deco stores all plans in your browser's local storage. They live on your device only — nothing leaves unless you share or back them up explicitly.

## Share plan link

The fastest way to share a plan with a dive buddy: generate a link they can open in any browser.

1. Open the **App menu** (☰)
2. Tap **Share or back up**
3. Pick the plan you want to share
4. Tap **Share link** or **Copy link**

The link looks like:

```
https://sjjan.github.io/aeroplus-deco/#p=eyJ2IjoxLCJuIjoi...
```

The `#p=...` portion is a base64-encoded copy of the entire plan: cylinders, segments, settings, all of it. When your buddy opens the link, they see a prompt to import the plan; on import, it lands as a new plan in their plans bar — alongside whatever they already had.

### What's in the link

- Plan name
- All cylinders (mix, size, fill, role, on/off)
- All segments (depth, time, gas reference)
- All settings (GFs, ascent rates, CCR mode, setpoints if applicable)
- Surface interval and previous-dive state (if applicable)
- Scrubber freshness and O₂ refill flags (CCR)

### What's NOT in the link

- The buddy's existing plans (they don't get touched)
- Your stored license key or device label
- Any settings marked as defaults (those are per-device)

## Import from link

If a buddy sends you a link as plain text (not clicked through), import it manually:

1. Open the **App menu**
2. Tap **Import or restore**
3. Tap **Import plan from link**
4. Paste the URL or just the `#p=...` portion
5. Confirm the import

The new plan lands at the end of your plans bar.

## Print / Save as PDF

For a permanent record or a paper backup to take on the boat:

1. **Share or back up → Print / Save PDF**
2. The app opens the print dialog with a formatted plan view
3. Choose **Save as PDF** in your browser's print dialog destination
4. The PDF includes: header (name, GFs, salinity, altitude), top-line metrics, dive profile chart, runtime schedule, gas plan with bars, rock bottom, and the calculated CNS/OTU

The PDF is self-contained — no app dependencies. Print it, save to cloud storage, attach to email, etc.

## Plain-text briefing

For Messages, email, or notes apps where a link won't render properly:

1. **Share or back up → Copy plain-text briefing**
2. A formatted text block is copied to your clipboard

The briefing looks like:

```
AeroPlus Deco — Plan 1
Plan 1 · ZHL-16C-GF 50/75 · 26/05/2026 · Salinity: Fresh · Alt: 0 m

Max depth: 75 m
Run time: 66 min
TTS: 51 min @ RT 15
Total deco: 35:40 min

Cylinders:
  16/58  16.0 ℓ  270 → 35 bar (235)  3756 ℓ used
  50/0   11.1 ℓ  232 → 164 bar (68)   758 ℓ used
  100/0   5.5 ℓ  232 →  94 bar (138)  757 ℓ used

Runtime schedule:
  ↘ 75.0   4   +4:10  16/58
  → 75.0  15  +11    16/58
  ...
```

Useful for buddies who don't want to click a link, or for posting to dive-trip group chats.

## JSON backup

For a full backup of *all* plans (not just one), plus settings:

1. **Share or back up → Save data**
2. The full JSON appears in a text area
3. **Copy to clipboard** or save the text manually

You can save the JSON to a file (any text editor → save as `.json`) and back it up to cloud storage. The format is human-readable, so you can edit it if needed (carefully).

## JSON restore

To restore all plans from a backup:

1. **Import or restore → Load data**
2. Either:
    - **Choose file** — pick a saved `.json` file
    - **Paste JSON** — paste the text directly
3. Confirm — this **replaces all existing plans** with the ones in the JSON

Use restore when:

- Switching to a new device
- Reinstalling the app or clearing browser data
- Reverting to a known-good backup after experimentation

## Browser storage caveats

All data lives in `localStorage`. This means:

- **Clearing browser data wipes the app** — back up to JSON regularly
- **Private/Incognito browsing doesn't persist** — restart loses everything
- **Different browsers on the same device** don't share data
- **App installed as PWA** has its own storage separate from the regular tab

If you rely on the app for real dive planning, set up a regular JSON backup routine (e.g., before every trip, after every plan change).

## Privacy

No part of AeroPlus Deco transmits your plans, settings, or device information to any server. The only network traffic is when you:

- Initially load the page (`sjjan.github.io`)
- Activate or deactivate a license (`polar.sh` API)
- Click a link to an external resource (e.g., the Andy Davis article)

Plans and personal settings never leave your device unless *you* explicitly share them.
