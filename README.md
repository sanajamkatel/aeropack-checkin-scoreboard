# AeroPack — Live Check-In Scoreboard

A live scoreboard built for **AeroPack**, Aeropay's back-to-school kit-packing
volunteer event. It runs on a shared iPad or laptop at the entrance and tracks
two separate things:

- **Check-ins (people)** — who showed up, by team. This is what the team
  competition is scored on.
- **Bags packed (kits)** — total output toward the event goal. Since one
  person can pack several bags, this is *not* the same number as check-ins,
  so it's tracked independently.

## What it is

The screen has two zones:

1. **Team leaderboard, driven by check-ins.** 12 large tappable team buttons
   (Finance, Marketing, Product, Engineering, Payment Ops, Partnerships,
   Revenue, Customer Success, People & Business Ops, Risk & Compliance,
   Revenue Ops, Solutions Engineering). Each arriving participant taps their
   own department once — one tap = one person checked in for that team. The
   leaderboard re-sorts smoothly (FLIP animation) as teams climb, with rank
   badges for the top 3, and a "People checked in" running total at the top.
2. **Bags-packed progress bar, driven by a separate staff counter.** Since
   bag output doesn't map 1-to-1 to people, it's controlled independently —
   by an intern at the packing station — via a `+` / `−` stepper, or by
   tapping the number itself to type an exact total (e.g. correcting to
   "37" after a recount). This is what feeds the goal thermometer toward 100.

- **Animated feedback on every check-in tap**: button press, a "+1" that
  floats up, a brief pulse ring, and a tasteful confetti burst in the brand's
  aqua palette.
- **Undo last check-in** — fixes an accidental team tap by reverting the most
  recent one (doesn't affect the bags counter — use `−` or edit the number
  for that).
- **A quiet Reset link** — clears both the check-ins and the bags count
  before the real event starts (asks for confirmation first).
- **State persists across refresh** via `localStorage`, with an automatic
  in-memory fallback if storage is unavailable (e.g. private browsing).

## How to run it

This is a single self-contained HTML file — no build step, no dependencies,
no backend, no internet connection required.

1. Open `index.html` directly in any modern browser (double-click it, or
   `open index.html` on macOS), **or**
2. Serve the folder with any static file server, e.g.:
   ```
   npx serve .
   ```
   and visit the printed local URL, **or**
3. Push this repo to GitHub and enable **GitHub Pages** (Settings → Pages →
   deploy from `main`) to get a shareable public link.

For the live event, open it in the iPad's browser and add it to the Home
Screen (Share → Add to Home Screen) for a full-screen, app-like kiosk feel.

## Customizing

Everything lives in `index.html`:

- **Teams** — edit the `TEAMS` array (id, display name, icon key).
- **Icons** — add/edit entries in the `ICONS` object (simple stroke-based
  24×24 SVG paths).
- **Goal** — change the `GOAL` constant (default `100`).
- **Colors** — edit the CSS custom properties at the top of `<style>`
  (`--aqua-bright`, `--aqua-deep`, `--aqua-tint`).

## Resetting between a test run and the real event

Tap the small **Reset** link in the top-right corner and confirm. This zeroes
every team's check-ins, the undo history, and the bags-packed count — do this
once right before doors open if you were testing beforehand.
