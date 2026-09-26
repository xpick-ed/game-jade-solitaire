# TODO — 翡翠接龍 (Klondike solitaire)

## Current

**Doing (done, committed):** v4 — rebuilt the whole game in the 漫畫 (comic) style the user picked
from the direction board (https://claude.ai/artifact/QkbRrtFhRXihB4MFnPeHMX). The old
翡翠 / 糖果 / 極簡 looks and the 風格 picker are gone.
- Look: halftone yellow page with sun rays, white cards with thick ink outlines and hard offset
  shadows, Bangers numerals, inked suits with a white glint, J/Q/K in starbursts captioned
  騎士 / 皇后 / 國王, aces on a cyan burst, dotted card backs with a yellow star. Speech-bubble toasts,
  chunky buttons, comic sheets. Fonts: Bangers + Noto Sans TC.
- Settings: 背景 (檸檬黃 / 汽水藍 / 草莓粉) and 牌背 (桃紅 / 天藍 / 番茄紅); old saved prefs fall back to defaults.
- New layout: foundations + a 已收 N/52 progress panel along the top, tableau in the middle,
  buttons bottom-left, waste + stock bottom-right (waste fans leftward). The deal flies out of the stock.
- 連擊 (combo): a foundation move or turning over a hidden card within 6 s of the last one grows the
  combo; its points are multiplied by the combo (max ×5). Pink chip in the progress panel with a
  draining strip, rising arpeggio sound. Undo and new game end the combo; 自動收牌 doesn't count.
- Pops: 「啪！/咚！/好耶！」 on foundation drops, 「連擊×N！」 in pink, 「讚啦！/收齊！」 when a suit
  completes, a huge 「贏啦！」 on a win; the canvas win cascade paints comic cards.
- Fixed the old bug: `newGame` now cancels a running auto-complete and the previous deal's timer.
- Checked in the browser: desktop 1100×760 and phone 390×780, a 4-move combo (score 15+30+45+60),
  undo, the pop sizes, settings, and the win cascade + dialog. No console errors.
- Published as an Artifact (same URL as before): https://claude.ai/artifact/1AgUn3kLQ76rbdYHPRZLWK

**Next (ideas):**
- Get the user's reaction after playing; tune combo timing (6 s) and multiplier cap (×5) by feel.
- Only deal solvable games (needs a solver, ideally in a Web Worker).
- Cycle through destinations when a tapped card has more than one legal spot.
- Left-hand layout option (mirror: stock bottom-left, buttons bottom-right).
- Other variants (Spider / FreeCell) reusing the card rendering.

**Blockers:** none.

## Notes

- Repo: https://github.com/xpick-ed/game-jade-solitaire (folder `games/game-jade-solitaire`, was `games/poker`).
- Play locally: just open `index.html` in a browser (Google Fonts loads over the network).
- Republish the Artifact after edits: strip the document wrapper, then publish to the same URL:
  `grep -v -x -E '<!doctype html>|<html lang="zh-Hant">|<head>|</head>|<body>|</body>|</html>|<meta charset="utf-8">|<meta name="viewport".*>' index.html > /tmp/jade-solitaire.html`
  then publish that file with `url` = the Artifact link above.
- The whole game lives in the one `<script>` block: state (`G`, `history`), layout (`measure`,
  `fan`, `computePositions`, `render`), moves (`doMove`, `drawStock`, `smartTarget`), combo
  (`bumpCombo`, `endCombo`), pops (`boom`, `fxEl`), hints (`findHints`), win (`win`, `cascade`,
  `cardImage`). Background / back colours are CSS `[data-felt]` / `[data-back]` blocks.
- Design history: v1 classic felt, v2 jade glass, v3 翡翠/糖果/極簡, then two proposal boards; the
  user rejected everything card-on-felt and chose 漫畫.
