# CLAUDE.md — RRLsite

## SESSION BOOTSTRAP — Read This First

Before doing any work:

1. Read this file in full.
2. Run `git branch --show-current` and `git status`.
3. If resuming a task, read the relevant `.md` source files (don't trust memory).
4. If the user references content that lives in the **app repo** (RetirementRiskLab), open it from disk at `../RetirementRiskScenario/` rather than guessing from memory.

This is the **public website** for Retirement Risk Lab. The product (app, engine, schemas, canonical docs) lives in the **separate, private** repo `ether-ore/RetirementRiskLab`. This repo holds *only* the marketing site and a copy of the user-facing documentation.

---

## Non-negotiable rules

**On marketing copy:**
- **Do not make claims about the app that aren't verifiable in the app's source.** Before writing that the app does X, check the app source at `../RetirementRiskScenario/ios/RRLApp/RRLApp/`.
- Prices, feature lists, and platform support must match what the user sees in the app's own PaywallSheet, FeatureGates, and Info.plist. Don't paraphrase from memory.
- The Lifetime Unlock price comes from StoreKit at runtime, but the page can quote it. Verify against `ios/RRLApp/RRLApp/PaywallSheet.swift` and the `Configuration.storekit` fixture.
- The app is **not yet on the App Store** as of the last edit of this file. Buttons must say "Coming soon to the App Store" — not "Download on the App Store" — until the developer updates this file to confirm a live URL exists.

**On the canonical User Guide:**
- The User Guide lives in **two** places: the canonical at `../RetirementRiskScenario/docs/user-guides/RetirementRiskLab_UserGuide.md`, and a mirror inside the app subtree at `../RetirementRiskScenario/ios/RRLApp/docs/user-guides/RetirementRiskLab_UserGuide.md`.
- This site holds a **third** copy at `docs/manual.md` so users can read it on the web without having the app installed.
- **When the canonical guide changes, the site copy needs to be refreshed.** Don't edit `docs/manual.md` independently — the only correct workflow is: edit canonical → mirror to app subtree → copy to this site's `docs/manual.md`.

**On the privacy statement:**
- `docs/privacy.md` describes what the app actually does. Before changing it, verify the app behavior in source. Don't promise behaviors that aren't implemented (e.g. don't add "no third-party analytics" if a third-party SDK is in fact present in the app build).

**On the build pipeline:**
- This site uses **MkDocs with the Material theme**, mirroring the BJW site. Build with `mkdocs build` locally; CI runs `mkdocs build` and deploys to GitHub Pages on push to `main`.
- The custom domain `retirementrisklab.app` is configured via `docs/CNAME`. Do not remove or modify that file without a deliberate domain change.
- The deploy workflow at `.github/workflows/deploy.yml` is the source of truth for build commands. Keep the local build aligned (same Python version, same `pip install -r requirements.txt`).

**On scope:**
- This is a **marketing + docs site**, not a product. Don't add client-side JS frameworks, analytics, comment systems, or other moving parts without a clear reason.
- Don't add tracking pixels, fingerprinting, or any analytics that contradict the privacy statement.

---

## Architecture

```
RRLsite/
├── docs/                  All markdown sources for the site
│   ├── index.md           Home page (product landing)
│   ├── manual.md          User Guide, COPIED FROM canonical
│   ├── privacy.md         Privacy statement
│   ├── CNAME              Custom domain — retirementrisklab.app
│   └── assets/
│       ├── macos/         App Store screenshots (5)
│       ├── ipad/          iPad simulator captures (4)
│       └── iphone/        iPhone simulator captures (4)
├── archive/               Previous hand-built site (preserved for reference)
├── mkdocs.yml             MkDocs config
├── requirements.txt       Python deps (mkdocs-material)
└── .github/workflows/
    └── deploy.yml         GitHub Pages build + deploy
```

---

## Canonical locations

When a file lives in the app repo, edit it there first and copy here. Do not edit copies independently.

| What | Canonical | This site |
|---|---|---|
| User Guide | `../RetirementRiskScenario/docs/user-guides/RetirementRiskLab_UserGuide.md` | `docs/manual.md` |
| App screenshots (macOS) | `../RetirementRiskScenario/marketing/app-store/macos/appstore_*.png` | `docs/assets/macos/0?_*.png` |
| App screenshots (iPad) | `../RetirementRiskScenario/marketing/app-store/ipad/raw/0?_*.png` | `docs/assets/ipad/` |
| App screenshots (iPhone) | `../RetirementRiskScenario/marketing/app-store/iphone/raw/0?_*.png` | `docs/assets/iphone/` |
| App icon / branding | `../RetirementRiskScenario/ios/RRLApp/RRLApp/Assets.xcassets/AppIcon.appiconset/` | (not yet pulled in) |

---

## Local build

```bash
pip install -r requirements.txt
mkdocs build              # build into ./site
mkdocs serve              # live-reload preview on http://127.0.0.1:8000
```

`mkdocs build --strict` fails on any link or asset warning. Run it before pushing.

---

## Operational notes

- **The custom domain `retirementrisklab.app` is live.** Whatever lands on `main` will be the public face of the product. Don't merge half-finished content; use feature branches and PRs.
- The previous hand-built site under `archive/` documents the pre-App-Store messaging (Lemon Squeezy, $29 price, Windows builds, 30-day trial). All of that is **obsolete** — do not echo any of it in the current site.
- The "Coming soon to the App Store" placeholder will be replaced by a real `https://apps.apple.com/...` URL once the app is approved. When that day comes, update `docs/index.md` in two places: the hero CTA and the Lifetime-Unlock-section CTA. Also update the FAQ "When will it be available?" answer.

---

## Source-of-truth hierarchy

1. Explicit user instruction in the current task
2. This file (CLAUDE.md)
3. The canonical app User Guide
4. The app's own source (`../RetirementRiskScenario/ios/RRLApp/RRLApp/*.swift`)
5. Pre-existing site conventions

If two sources at the same level conflict, surface the conflict and ask. Do not silently resolve it.
