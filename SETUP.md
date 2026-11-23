# Living Scene GitHub Profile README — Setup & Documentation

**Repository:** `Aashrith-Ganesh/Aashrith-Ganesh`  
**Author:** Aashrith Ganesh (@Aashrith-Ganesh)  
**Status:** Prepared Locally (Unpublished)

---

## 1. Overview

This project implements an original, 100% free **Living Scene GitHub Profile README** inspired by dynamic landscape profiles. It generates an animated SVG header reflecting real-time weather and solar daylight conditions over **Bengaluru, Karnataka, India**, paired with a botanical foreground garden where **52 distinct plants** grow dynamically based on verified weekly GitHub contributions.

### Key Highlights
- **Zero Paid Dependencies:** Uses Open-Meteo's free, unmetered public API for live weather data.
- **Graceful Fallback:** If weather networks or APIs are unreachable, the generator automatically calculates solar time from local system clocks and renders a clean celestial sky without failing.
- **Pure SVG & CSS Animation:** Uses CSS keyframes (`.sway`, `.tw`, `.drift`, `.walk`, `.smoke`) that render reliably in GitHub's sanitized image proxy (Camo) without JavaScript security restrictions.
- **Accessibility:** Embedded `@media (prefers-reduced-motion: reduce)` rules disable all animations for users with motion sensitivities.
- **Zero Token Leakage:** Never embeds GitHub tokens, auth headers, or external secrets inside public SVGs or Markdown.

---

## 2. Directory Layout

```
Aashrith-Ganesh/
├── .github/
│   └── workflows/
│       └── update-scene.yml     # Automated scheduled workflow (every 4 hours)
├── assets/
│   ├── living-scene.svg         # Primary 880x420 animated sky & contribution garden
│   ├── garden-stack.svg         # 880x260 terraced language distribution beds
│   └── garden-log.svg           # 880x240 botanical activity ledger & metrics
├── scripts/
│   └── generate_scene.py        # Python SVG generation & weather ingestion engine
├── README.md                    # Profile README with developer intro & showcases
└── SETUP.md                     # Setup, testing, and deployment instructions
```

---

## 3. Local Testing & SVG Generation

### Basic Run (Live Weather & Commits)
To regenerate all assets using the current real weather and contribution data:
```bash
python3 scripts/generate_scene.py
```

### Visual Simulation & Testing Flags
The generation script supports simulation flags to preview different times of day and weather conditions:

```bash
# Preview Sunrise over Bengaluru
python3 scripts/generate_scene.py --phase sunrise --temp 21

# Preview Sunny Daytime
python3 scripts/generate_scene.py --phase day --temp 29 --condition CLEAR

# Preview Golden Hour Sunset
python3 scripts/generate_scene.py --phase sunset --temp 26

# Preview Starry Night
python3 scripts/generate_scene.py --phase night --temp 22

# Preview Rainy Monsoon Weather
python3 scripts/generate_scene.py --condition RAIN --temp 23
```

---

## 4. How the GitHub Actions Workflow Operates

The workflow at `.github/workflows/update-scene.yml` handles fully autonomous regeneration:

1. **Schedule:** Triggers every 4 hours via cron (`0 */4 * * *`).
2. **Environment:** Runs on standard `ubuntu-latest` with Python 3.12.
3. **Execution:** Executes `python scripts/generate_scene.py` using GitHub's built-in `GITHUB_TOKEN`.
4. **Clean Commits:** If the weather or sky phase changed the SVG, it commits the updated assets under `github-actions[bot]` with `[skip ci]` to prevent infinite loops. If nothing changed, it exits silently.

---

## 5. Publishing to GitHub (When Approved)

*Note: Per project instructions, this repository has been prepared locally and has NOT been published.*

When you are ready to publish your profile README:

### Step 1: Create the Special Profile Repository
On GitHub, a repository named exactly `<username>/<username>` serves as the special profile repository.
Run:
```bash
cd /Users/aashrith/Projects/Aashrith-Ganesh
gh repo create Aashrith-Ganesh/Aashrith-Ganesh --public --source=. --remote=origin --push
```

### Step 2: Verify Workflow Permissions
1. Navigate to `https://github.com/Aashrith-Ganesh/Aashrith-Ganesh/settings/actions`.
2. Under **Workflow permissions**, verify that **Read and write permissions** is selected (this allows the bot to commit updated SVGs).
3. Under the **Actions** tab, trigger a manual test run of the `Living Scene Atmosphere Update` workflow.

### Step 3: Inspect Profile
Visit `https://github.com/Aashrith-Ganesh` to view your living sky and botanical garden in action!
