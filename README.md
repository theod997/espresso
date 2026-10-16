# Espresso 1:2

*[Version française](README.fr.md)*

A tiny, free web app (PWA) to log your espresso shots and get one clear piece of advice for the next one — aiming for a **1:2 ratio in 25–30 s**.

Built around a Gaggia Classic Pro and a Kingrinder K6 hand grinder, but the dialing-in logic works with any machine.

**▶ Try it: https://theod997.github.io/espresso/**

> The interface is currently in French only.

---

## Features

- **Fast shot logging** with big +/- buttons: coffee, dose, grinder clicks, time, yield, taste (sour / balanced / bitter), notes
- **Shot diagnosis**: ratio and time vs. target, with targets adjusted to roast level (light 1:1.8–2.5, medium 1:1.8–2.2, dark 1:1.8–2.0)
- **One change at a time**: the app tells you which single variable to adjust (grind, yield, temperature or puck prep) and suggests a **next recipe** you can apply in one tap
- **Smart checks**:
  - detects choked shots
  - estimates how long the shot would have taken at the target yield, so a long or short pull still gives a useful grind hint
  - sour/bitter with good time and ratio → temperature hints (warm-up, flush, purge after steaming)
  - inconsistent times at the same setting → puck prep hints (WDT, distribution, level tamp)
- **Per-coffee dashboard**: best setting so far, % of shots on target, sparklines for clicks and ratio
- **Freshness warnings** based on roast date (best 7–30 days after roasting)
- **History** with edit/delete, **CSV export** (opens in Excel or Google Sheets) and **CSV import** (restore or move to a new phone)
- Grinder settings shown in clicks, turns and µm (K6: 16 µm per click)

## Privacy & offline

- No account, no server, no tracking: everything is stored **locally on your device** (browser storage).
- Works offline once installed.
- Every user gets their own empty app — nothing is shared between users.

## Install on your phone

**Android (Chrome):** open the link → menu **⋮** → **Add to Home screen** → **Install**.
**iPhone (Safari):** open the link → **Share** → **Add to Home Screen**.

## Back up your data

Shots live in your browser only. They are lost if you uninstall the app, clear browser data or switch phones.
Export regularly: **History → Export CSV**. To restore or move to a new phone: **History → Import CSV** (existing shots are not duplicated).

## Tech

Plain HTML/CSS/JavaScript in a single `index.html` — no framework, no build step.

| File | Purpose |
|---|---|
| `index.html` | the whole app |
| `manifest.json` | PWA manifest |
| `service-worker.js` | offline cache |
| `icon-192.png`, `icon-512.png` | app icons |

### Run your own copy

1. Fork this repo.
2. **Settings → Pages → Deploy from a branch → `main` / (root) → Save**.
3. Your copy is live at `https://<your-username>.github.io/espresso/` after a minute or two.

To push an update to installed apps, bump the cache name (`espresso-v3`) in `service-worker.js`.

## Feedback

Issues and suggestions are welcome — especially if a piece of advice looks wrong for your setup.
