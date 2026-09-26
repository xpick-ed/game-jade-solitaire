# TODO — 翡翠接龍 (Klondike solitaire)

## Current

**Doing (done, committed):** v1 of the game — a single file, `index.html`, no build step.
- Klondike rules, draw 1 or draw 3, unlimited passes through the stock, Windows-style scoring
  (+time bonus on a win).
- Drag to move cards, or tap a card to send it to the best spot. Undo, hints (cycle through them),
  auto-complete once everything is face up, and the bouncing-card cascade when you win.
- Seeded deals: every deal has a number (#123456); "重玩這一局" replays it, and "今日挑戰"
  gives everyone the same deal for the day.
- 3 felt colours × 3 card backs, synthesised sound effects (WebAudio), stats and the
  in-progress game saved in localStorage.
- Published as an Artifact: https://claude.ai/artifact/1AgUn3kLQ76rbdYHPRZLWK

**Next (ideas):**
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
