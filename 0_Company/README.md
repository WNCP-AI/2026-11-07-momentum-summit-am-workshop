# 0_Company

The source of truth about your company. Skills read this so you never have to explain the basics twice.

The folder starts empty, and `onboarding` fills it in.

| File | Holds |
|---|---|
| `01_Overview.md` | One-liner, identity, stage |
| `02_Product.md` | What it is, what it does, how it works, where it is today |
| `03_Sales.md` | Who you sell to, what you sell, pricing, proof points |
| `04_Market.md` | Market, competition, positioning |
| `05_Traction.md` | Metrics, goals, fundraising status |
| `06_Team.md` | Founders, roles, key hires |
| `Z_Library.md` | Deeper detail, referred to by section |

**Keep it distilled.** Each file holds short facts, not full documents. A full document goes in `3_Library/`, and
a one-paragraph summary of it goes here. Longer detail goes in `Z_Library.md`.

The agent changes these files through the `util-company-info` skill. You can also edit them yourself at any time.

**Before you share this folder:** it's tracked by git, so it travels with the repo. Check what's in it before
pushing to anywhere public. Confidential numbers belong in `3_Library/`, which is gitignored.
