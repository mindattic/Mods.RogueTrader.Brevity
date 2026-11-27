---
layer: bible
status: living
---
# RogueTrader.Brevity — Project Bible

> Single source of truth for what Brevity IS, is NOT, and the rules that keep it coherent.
> README says how to build and run it; this says how to think about it. The finish line lives in
> `docs/RELEASE.md`.

## 1. The one sentence {#RTB-§1}
Brevity makes Warhammer 40,000: Rogue Trader's dialogue shorter by swapping in LLM-shortened English text at
runtime, without touching the game's files.

## 2. The product promise {#RTB-§2}
- Every NPC line, narration and answer option of the base game and all three story DLCs has a shorter version.
- Lines keep their meaning, the speaker's voice and in-setting words; markup tokens survive.
- Turning the mod off restores the original text at once, even mid-conversation.

## 3. What it is NOT {#RTB-§3}
- Not a translation: English only.
- Not a content or story change: no blueprints, no save data.
- Not voice-over editing: voiced lines keep their audio.

## 4. Architecture canon {#RTB-§4}
```
WhRtModificationTemplate.tar + enGB.json
        | tools/DialogueExport            -> dialogue.jsonl
        | tools/DialogueSimplify (Claude) -> .brevity/cache.jsonl -> .brevity/simplified.json
        | src/BrevityMod (UMM mod)        -> overlays LocalizationManager's text pack in memory
```
### 4.1 Modules
- `tools/DialogueExport`: blueprints and English strings to one JSONL row per cue or answer.
- `tools/DialogueSimplify`: batches per conversation to Claude (Batches API or `--sync`, or `--export`/`--import`
  for subagents), validates, caches by text hash plus prompt version.
- `src/BrevityMod`: Unity Mod Manager mod; uses Shared's `LocalizationOverlay`.
- `tools/release_changes.py`, `tools/releases.json`: per-release changed-line lists.
- `tools/capture_dialogue.py`, `tools/pair_screenshots.py`: before/after screenshots for the Nexus page.
### 4.2 Domain model
Cue, answer, dialog, speaker, string key, markup token, cache entry, reject.
### 4.3 Key services
Export, simplify, validate, overlay, restore.

## 5. The Laws {#RTB-§5}
Inherits `MindAttic.HouseRules.md` by reference.
1. {#RTB-LAW-1} `enGB.json` on disk is never modified; everything happens in memory.
2. {#RTB-LAW-2} A simplified line must keep exactly the original's set of markup tokens, or it is rejected.
3. {#RTB-LAW-3} The cache is append-only; reruns send only lines whose text or prompt version changed.
4. {#RTB-LAW-4} Each release gets `docs/dialogue-polish-changes-v<major>.md`, generated from the cache.

## 6. Verified state {#RTB-§6}
- 3.0.0 live on Nexus mod 651 (`.publish-state.json`), published through `.github/workflows/publish.yml`.
- 1.0.0 (2026-10-25) shortened every line; 2.0.0 restored over-cut lines; 3.0.0 polished 5,633 stilted lines.

## 7. Active frontier {#RTB-§7}
See `docs/RELEASE.md`: retake the page's before/after screenshots for the 3.0.0 text.

## 8. Quality bar {#RTB-§8}
A change is done when the mod builds, the overlay shows the new text in game, disabling restores the original,
and a release has its changed-lines list.

## 9. Glossary {#RTB-§9}
- **Cue**: an NPC or narrator line. **Answer**: a player reply option.
- **UMM**: Unity Mod Manager, which Rogue Trader starts itself (Ctrl+F10).
