---
layer: release
status: living
---
# Mods.RogueTrader.Brevity — Release charter

> The one finish line this repo is working toward. Every open ticket in this repo sits under one of the epics
> below, and every epic is part of the milestone. Work that does not fit is out of scope until this milestone is
> reached (owner, 2026-11-27, MAT-T319).

## 1. What this is
A Unity Mod Manager mod for Warhammer 40,000: Rogue Trader that swaps the game's dialogue for LLM-shortened
text at runtime, plus the export and simplify tools that produce that text.

## 2. The milestone: Brevity 3.0.0 on Nexus, page current {#milestone}
- **Milestone:** MS-74, "Brevity 3.0.0 on Nexus, working, page current"
- **Published means:** the 3.0.0 file on Nexus Mods mod 651 (already live, uploaded through
  `.github/workflows/publish.yml`), installable with Vortex or by hand.
- **The natural stopping point:** every line of the base game and its three DLCs is shortened and polished
  (3.0.0), the mod is live and working, and the page's before/after screenshots show the text players actually
  get. Only the screenshots are behind, so this is the smallest honest "done".

## 3. Done when (acceptance checks)
1. build — `dotnet build -c Release src/BrevityMod` builds clean on main and writes
   `dist/RogueTraderBrevity-3.0.0.zip`.
2. exists — https://www.nexusmods.com/warhammer40kroguetrader/mods/651 serves 3.0.0.
3. signoff — the owner sees the retaken 3.0.0 before/after screenshots on the live Nexus page.

## 4. Epics, in priority order
| Priority | Epic (ticket) | What it delivers | Features |
|---|---|---|---|
| 900 | RTB-T277 Nexus page refresh | Screenshots that show the 3.0.0 text, on the live page | RTB-T278 Before/after screenshots (990), RTB-T279 Live page images (980) |

One epic: the mod itself is finished; only the page lags.

## 5. Out of scope (not before this milestone)
- Re-running the whole simplify pass or a 4.0.0 polish — only on a new player report of broken lines.
- Open-ended "exhaustive bughunt" passes.
- Deploying the tools to R:\MindAttic\Apps (RTB-T276) — owned by the Agency rollout MAT-T318, not this charter.

## 6. Current verified state
- 3.0.0 is the published file (`.publish-state.json`, `tools/releases.json`, `src/BrevityMod/Info.json`).
- The 2026-11-04 save-load crash (RTB-T262) was investigated: Brevity only overlays localization text and cannot
  cause a blueprint-load failure; it did not reproduce.
- Capture tools for screenshots exist (`tools/capture_dialogue.py`, `tools/pair_screenshots.py`, RTB-T274/T275).

## 7. Decision record
- 2026-11-27 — charter drafted from README/NEXUS_PAGE/tickets; Legion vote: Approve, 5/5 answering (4 providers errored), Plurality quorum, no dissent.
- Triage: 4 open → done 0, duplicate 0, wont-do 2 (RTB-T272 bughunt, RTB-T262 not a Brevity bug), kept 1 (RTB-T255), left alone 1 (RTB-T276, under Agency MAT-T318); 1 new task (RTB-T280 swap Nexus page images).
