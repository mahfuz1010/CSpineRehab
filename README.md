# CSpineRehab

A single-page, browser-based guided rehabilitation tool for cervical spine (C5/C6/C7 disc herniation) recovery. No dependencies, no build step — open `index.html` in any modern browser.

---

## Features

- **Guided session timer** with prep → work → rest → between-exercise phase management
- **Circular progress ring** and colour-coded phase badges (blue = prepare, green = work, amber = rest)
- **Animated SVG illustrations** for every exercise, rendered inline — no image files needed
- **5- or 10-minute session modes** that automatically fit as many exercises as possible within the time budget
- **Drag-and-drop exercise reordering** (mouse and touch) so you can prioritise movements that matter most to you
- **Exercise info modal** with full instructions, coaching cues, and set/rep stats
- **Session summary screen** showing elapsed time, exercises completed, and total sets
- Safety disclaimer reminding the user to stop if neurological symptoms appear

---

## Screens

| Screen | Description |
|--------|-------------|
| **Setup** | Choose session length (5 or 10 min), reorder exercises, start session |
| **Session** | Active timer with phase indicator, illustration, rep/set tracker, queue, pause/skip/end controls |
| **Done** | Summary of time spent, exercises and sets completed, list of finished exercises |

---

## Exercise Library

15 exercises across four categories:

| Category | Exercises |
|----------|-----------|
| **Stabilization** | Chin tuck, Isometric neck hold, Bird-dog, Dead bug |
| **Mobility** | Shoulder blade squeeze, Seated neck rotation, Seated neck flexion, Nerve glide (median) |
| **Stretch** | Seated side bend, Upper trapezius stretch, Levator scapulae stretch, Pectoral stretch, Doorway chest opener |
| **Posture** | Seated scapular retraction, Wall angels |

Exercises marked **seated** can be performed in a chair — useful for desk-based sessions.

Each exercise defines:
- `type`: `hold` (timed hold × reps × sets) or `dynamic` (timed set duration × sets)
- `holdSec` / `setDuration`: work interval in seconds
- `repsPerSet`, `sets`: repetition and set counts
- `restBetweenSets`, `restBetweenEx`: rest intervals in seconds
- `instruction`: step-by-step description
- `cue`: single coaching cue shown during the work phase

---

## Session Timing Logic

Total exercise time is calculated as:

```
exerciseTime = (holdSec × repsPerSet OR setDuration) × sets
             + restBetweenSets × (sets − 1)
             + restBetweenEx
             + 5s prep
```

The planner iterates exercises in the current drag order and greedily adds each one until the time budget is exhausted.

---

## Project Structure

```
index.html   — entire application (HTML + CSS + JavaScript, self-contained)
README.md    — this file
```

All styles live in a `<style>` block, all logic in a `<script>` block. External resources are limited to Google Fonts (loaded over CDN).

---

## Usage

1. Open `index.html` in a browser (no server required).
2. Select **5 min** or **10 min**.
3. Optionally drag exercises to change their priority order.
4. Tap **?** on any exercise to read full instructions before starting.
5. Press **Begin session →**.
6. Use **Pause**, **Skip**, or **End** controls during the session.

---

## Safety Note

> Stop any exercise that causes tingling, numbness, or shooting arm pain. Consult a physiotherapist if symptoms worsen. This tool is intended as a guided aid, not a replacement for professional medical advice.

---

## Browser Support

Any modern browser with CSS custom properties and the Pointer Events API (Chrome, Firefox, Safari, Edge — all current versions).
