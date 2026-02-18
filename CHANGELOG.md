# Changelog

All notable changes to this project will be documented in this file.

### Fixed

- **HTML UI centering incorrectly applied when `showCover: false`** — `HTMLUI.update()` unconditionally called `firstPageCenter()` / `firstPageEndCenter()` when the current page index was at position 0 or the last position, regardless of the `showCover` setting. This shifted the two-page spread left (or right) by a quarter of the container width when `showCover` was `false`. Both branches are now guarded by `this.app.getSettings().showCover`. ([src/UI/HTMLUI.ts](src/UI/HTMLUI.ts))
- **Same centering bug in flip animation callback** — The animation-end callback in `Flip.ts` had the same unconditional calls to `firstPageCenter()` (on BACK flip to index 1) and `firstPageEndCenter()` (on FORWARD flip to `pageCount - 3`). Both are now guarded by `this.app.getSettings().showCover`. ([src/Flip/Flip.ts](src/Flip/Flip.ts))
