# Changelog

All notable changes to this project will be documented in this file.

### MY FIXES

- **Page-curl hover zones offset under CSS `transform: scale()`** — `getMousePos()` in `UI.ts` computed mouse coordinates using `getBoundingClientRect()` (which reflects the visual/scaled rect), but the rest of the hit-test pipeline (`calculateBoundsRect`, `convertToBook`) used `offsetWidth`/`offsetHeight` (layout rect, unaffected by scale). This mismatch shifted hover zones by `W*(1-s)/2` on X and `H*(1-s)/2` on Y, making right-page corners unreachable and left-page outer corners unresponsive. `getMousePos()` now divides the offset by `rect.width / offsetWidth` (and height equivalent), self-correcting for any active CSS scale. ([src/UI/UI.ts](src/UI/UI.ts))
- **HTML UI centering incorrectly applied when `showCover: false`** — `HTMLUI.update()` unconditionally called `firstPageCenter()` / `firstPageEndCenter()` when the current page index was at position 0 or the last position, regardless of the `showCover` setting. This shifted the two-page spread left (or right) by a quarter of the container width when `showCover` was `false`. Both branches are now guarded by `this.app.getSettings().showCover`. ([src/UI/HTMLUI.ts](src/UI/HTMLUI.ts))
- **Same centering bug in flip animation callback** — The animation-end callback in `Flip.ts` had the same unconditional calls to `firstPageCenter()` (on BACK flip to index 1) and `firstPageEndCenter()` (on FORWARD flip to `pageCount - 3`). Both are now guarded by `this.app.getSettings().showCover`. ([src/Flip/Flip.ts](src/Flip/Flip.ts))

### CHANGES From SAILgaosai/StPageFlip
**v2.1.0**
Added flag disableHardPages (default: false). If true, then the library will ignore hard pages even showCover is activated. It is recommended that you use this flag only for complex HTML.
