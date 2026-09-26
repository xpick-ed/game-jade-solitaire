# TODO — 翡翠接龍 (Klondike solitaire)

## Current

**Doing (done, committed):** v3 — three switchable looks (user asked for "cuter or more modern").
Settings → 風格 picks one; it's saved in prefs as `style` and set as `data-style` on `<html>`.
- 翡翠 (default): the v2 look, unchanged.
- 糖果 (cute): pastel polka-dot table, chunky cream cards with a raised bottom edge, a face on
  every suit, J/Q/K = bunny / cat with a bow / bear with a crown, heart-with-face card back,
  bouncier easing, confetti dots on foundation drops. Fonts: Fredoka + Chiron GoRound TC.
- 極簡 (modern): flat table, sharp white cards with huge thin Outfit-200 numerals, J/Q/K as a
  solid colour block, solid backs with one ring, electric-blue highlight. Font: Noto Sans TC.
- Each look renames and recolours the same 3 table and 3 back options (e.g. 極簡's 墨黑 table is dark).
- Card faces are rebuilt when the look changes (`cardHTML` switches on `look`); the win
  cascade has a canvas painter per look (`PAINT`). Candy art is `[fill, path]` lists (`FACES`,
  `PETS`) so the same shapes draw as SVG and on canvas.
- Checked in the browser: all three looks at desktop and 390px width, settings sheet, and the
  win cascade in candy and mono.
- Published as an Artifact (same URL as v1/v2): https://claude.ai/artifact/1AgUn3kLQ76rbdYHPRZLWK

**Next (ideas):**
- Get the user's reaction to 糖果 / 極簡; tweak from there.
- Bug found by reading (not fixed): starting a new game while auto-complete runs lets the old
  `autoComplete` timer keep moving cards in the new deal. `newGame` should cancel it; the menu's
  重玩/今日挑戰 buttons also skip the `busy` check.
- Only deal solvable games (needs a solver, ideally in a Web Worker).
- Cycle through destinations when a tapped card has more than one legal spot.
- Left-hand layout option (stock on the right).
- Other variants (Spider / FreeCell) reusing the card rendering.

**Blockers:** none.

## Notes

- Repo: https://github.com/xpick-ed/game-jade-solitaire (folder `games/game-jade-solitaire`, was `games/poker`).
- Play locally: just open `index.html` in a browser (Google Fonts loads over the network).
- Republish the Artifact after edits: strip the document wrapper, then publish to the same URL:
  `grep -v -x -E '<!doctype html>|<html lang="zh-Hant">|<head>|</head>|<body>|</body>|</html>|<meta charset="utf-8">|<meta name="viewport".*>' index.html > /tmp/jade-solitaire.html`
  then publish that file with `url` = the Artifact link above.
- The whole game lives in the one `<script>` block: state (`G`, `history`), layout (`measure`,
  `fan`, `computePositions`, `render`), moves (`doMove`, `drawStock`, `smartTarget`),
  hints (`findHints`), win (`win`, `cascade`). Themes are CSS `[data-felt]` / `[data-back]` blocks;
  looks are `[data-style="candy"]` / `[data-style="mono"]` blocks that re-point the `:root` tokens.
