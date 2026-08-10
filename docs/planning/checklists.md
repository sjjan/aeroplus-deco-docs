# Checklists

AeroPlus Deco includes a built-in **Checklists** tool for the procedures you run before and around a dive — rebreather assembly and pre-dive checks, gear packing lists, and anything else you want to standardise. Checklists live entirely on your device, work fully offline, and can be shared with other divers as files.

Open it from the menu (**☰ → Checklists**).

!!! warning "Checklists do not replace training"
    The bundled checklists are **generic** starting points. They are not a substitute for your unit's manufacturer procedures or your training agency's standards. Always verify each checklist against the documentation for your specific rebreather and configuration, and adapt it before relying on it.

## The two checklist types

Every checklist is one of two types, which you choose in the editor:

- **Step-by-step** — you advance through one item at a time, recording values and running timers as you go. Best for procedures where order and verification matter, such as assembly or pre-dive checks.
- **Simple tick list** — a single screen of items you tick off in any order, like a gear or packing list. Best for "did I bring everything?" lists.

## Step types (step-by-step checklists)

A step-by-step checklist is made of steps. Each step can be one of the following.

### Check-off step
A step with a title and instruction that you simply confirm with **Done**. Mark a step *not skippable* to require it.

### Steps with values
A step can collect one or more **fields**. Field types are:

- **Number** — a numeric value with an optional unit (for example `O₂` in `%`, or a cell reading in `mV`).
- **Text** — free text.
- **Month / year** — a month picker, useful for things like oxygen-cell manufacture dates.
- **Toggle** — a yes/no switch with labels you choose.
- **Choice** — a list of options.

Fields can be marked **required**, in which case **Done** stays disabled until they are filled in.

### Timer step
A step with a count-down or count-up timer — for example a five-minute pre-breathe. With **must elapse** enabled, **Done** is locked until the timer reaches zero. Timers keep running accurately even if the screen locks, and request a screen wake-lock while active.

### Pressure-test step
A dedicated step for positive and negative loop tests:

1. Enter the **start** pressure.
2. Start the timer and wait the configured minimum time. The **end** field is locked until the timer completes.
3. Enter the **end** pressure.

If the start and end values differ by more than the configured tolerance, the step shows a **warning** and the result is recorded as out of tolerance. You set the start/end prompts, the unit, the minimum time and the maximum allowed difference when you build the step.

## Running a checklist and saving responses

Open a checklist and tap **Start checklist**. For a step-by-step checklist you move through each step with **Skip** (where allowed) and **Done**; a simple tick list shows everything on one screen with a **Finish** button.

When you finish, you are asked for a diver name or initials and the run is saved as a **response**: a timestamped record of what was checked, the values you entered, and any pressure-test results. Review past runs from **See my responses** on the Checklists screen.

!!! note "Your data stays on your device"
    Checklists and saved responses are stored locally in the app. They are never uploaded. Clearing your browser/app storage will remove them, so export anything you want to keep.

## Creating and editing checklists

- **+ New checklist** creates an empty checklist; choose its type, give it a title, a category, and optionally the **model / unit** it is written for (for example *JJ-CCR* or *Revo III*). The category box offers your existing categories as suggestions.
- **Duplicate** copies any checklist (including the bundled templates) into your own library so you can adapt it without changing the original.
- **Edit** (on your own checklists) opens the editor, where you can add, reorder (▲▼) and delete steps or items, configure fields and timers, and set the step type.

### Photos
Any step can carry a **photo** — handy for showing valve orientation or a handset reading. Photos are taken or chosen from your library, automatically resized, and stored with the checklist, so they travel with it when you share it.

### Categories and ordering
Each checklist has a **category** (for example *Rebreather*, *Open circuit*, *Packing*, or anything you type). The Checklists screen groups checklists by category. Use the ▲▼ arrows on each checklist to set the order within its category; the order is remembered on your device.

## Where a checklist came from

Every checklist in the list carries a small badge showing its origin, so you can tell at a glance whether you are looking at something official or something a buddy sent you:

| Badge | Meaning |
|---|---|
| **Template** | One of the generic checklists bundled with AeroPlus Deco. |
| **Manufacturer** | Imported from a file that declares itself as the unit manufacturer's procedure. |
| **Community** | Imported from another diver. Anything you import that does not declare itself as a manufacturer or template file is treated as community. |
| **Yours** | Created by you, or duplicated from any of the above. |

A checklist you have changed since it arrived also gets an **edited** badge, so a modified copy is never mistaken for the original.

!!! warning "A badge is not a verification"
    The Manufacturer badge reflects what the file claims about itself — AeroPlus Deco cannot verify it. Check any imported checklist against your unit's actual documentation before you dive it.

## Sharing checklists

Use **Export / share** to produce a self-contained file (named after the checklist) that contains the entire checklist, including any photos. On a phone this opens the share sheet (AirDrop, Messages, Files, and so on); elsewhere it downloads a `.json` file.

To bring a shared checklist in, use **Import checklist** and select the file. AeroPlus checks the file, skips it if you already have an identical copy, and otherwise adds it to your library under its category. A checklist you import and then edit is marked **edited** so you can tell it has diverged from the original. This makes it easy to distribute a checklist for a specific rebreather brand and model.

## Bundled checklists

AeroPlus Deco ships with a few generic checklists to get you started:

- **Dive equipment — packing list** — a simple tick list of gear to consider bringing.
- **Generic CCR — Assembly** — a step-by-step build checklist, including negative and positive pressure tests.
- **Generic CCR — Pre-dive** — a step-by-step pre-dive checklist covering cell age, gas analysis, calibration, batteries, bailout and a pre-breathe timer.

Duplicate any of these to build your own unit-specific version.

If you delete a bundled checklist and later want it back, use **Restore default checklists**. This adds back any built-in checklists you have deleted; it does not touch your own checklists or undo your edits.
