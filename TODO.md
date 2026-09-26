# TODO — 翡翠接龍 (Klondike solitaire)

## Current

**Doing (done, committed):** v2 — modern visual redesign after v1 felt "too old school".
- Look: deep jade-teal gradient table with slow drifting light (no felt texture), white rounded
  cards with Outfit numerals, big single suit instead of pips, J/Q/K as gradient panels,
  gradient card backs with ripple lines + sheen, glass stat pill and dock, white bottom sheets.
  Chinese UI font: Chiron GoRound TC.
- Feel: cards tilt while dragged and land with a slight overshoot, foundation ring burst,
  floating "+10" score text, chime when a suit is completed.
- Themes are now 翡翠 / 深海 / 莓果 tables and 珊瑚 / 靛藍 / 石墨 backs
  (old saved prefs fall back to the defaults).
- Game logic unchanged from v1 (Klondike, draw 1/3, undo, hints, auto-complete, cascade,
  seeded deals + 今日挑戰, stats in localStorage).
- Published as an Artifact (same URL as v1): https://claude.ai/artifact/1AgUn3kLQ76rbdYHPRZLWK

**Next (ideas):**
- Get the user's reaction to the v2 look; tweak colours/fonts from there.
- Only deal solvable games (needs a solver, ideally in a Web Worker).
- Cycle through destinations when a tapped card has more than one legal spot.
- Left-hand layout option (stock on the right).
- Other variants (Spider / FreeCell) reusing the card rendering.

**Blockers:** none.

## Notes

- Play locally: just open `index.html` in a browser (Google Fonts loads over the network).
- Republish the Artifact after edits: strip the document wrapper, then publish to the same URL:
  `grep -v -x -E '<!doctype html>|<html lang="zh-Hant">|<head>|</head>|<body>|</body>|</html>|<meta charset="utf-8">|<meta name="viewport".*>' index.html > /tmp/jade-solitaire.html`
  then publish that file with `url` = the Artifact link above.
- The whole game lives in the one `<script>` block: state (`G`, `history`), layout (`measure`,
  `fan`, `computePositions`, `render`), moves (`doMove`, `drawStock`, `smartTarget`),
  hints (`findHints`), win (`win`, `cascade`). Themes are CSS `[data-felt]` / `[data-back]` blocks.
