<!-- GitHub Copilot / AI assistant guidance for contributors -->
# Project snapshot

This is a small, static personal portfolio site (HTML/CSS, no build step). Key files:

- `index.html` — single-page portfolio with inlined scripts at the bottom for navigation, tabs and simple UI behaviours (see `opentab`, `showMoreProjects`, `openmenu/closemenu`).
- `portfolio1.html` — example project detail page styled by `style.css`.
- `style.css` — the site's central stylesheet (responsive rules at the bottom). Many selectors are id/class based (e.g. `#header`, `.container`, `.tab-links`, `.work`, `.KI-img`).
- `.github/workflows/static.yml` — GitHub Actions workflow that deploys the repository to GitHub Pages on push to `main`.

## High-level guidance for AI coding agents

- This is a static site without a JavaScript build toolchain. Avoid introducing Node, bundlers, or transpilers unless the user explicitly asks.
- Preserve the current file layout and relative asset paths (images live in `Bilder/`). Use forward/backslashes consistently with existing HTML (the repo currently mixes `Bilder\` and `Bilder/` in paths; prefer `/` for web).
- JavaScript behaviors are small and DOM-focused and live inline at the bottom of `index.html`. When adding scripts, prefer a new file (e.g. `scripts.js`) and update `index.html` to include it, keeping changes minimal and clearly documented.

## Conventions and patterns to follow

- UI/structure: The page is organized into sections by id (`#about`, `#services`, `#portfolio`, `#contact`) — maintain these anchors when editing navigation or adding sections.
- Tabs: `opentab(tabname)` toggles `.active-link` and `.active-tab` on `.tab-links` / `.tab-contents`. Use those classes exactly when adding new tab content.
- Show-more: `showMoreProjects()` toggles `.hidden` on `.more-projects` and updates the `#seeMoreBtn` text. Keep the `.hidden` class in CSS for show/hide semantics.
- Responsive: mobile rules are in `style.css` below the media query for max-width 600px — add mobile adjustments there.

## Safe edits and examples

- To add a new project card in the Portfolio grid, copy one `.work` node in `index.html`, update its image path to `Bilder/your-image.ext`, and keep the `.layer` structure for hover overlay.
- To extract inline scripts: create `scripts.js` in repo root, move the two <script> blocks from `index.html` into it, wrap with an IIFE or `DOMContentLoaded` handler, then replace them with a single `<script src="scripts.js"></script>` before `</body>`.

## CI / Deployment notes

- The repo uses GitHub Pages via `.github/workflows/static.yml`. Pushing to `main` triggers Pages deployment and publishes the repository root contents. Don't rely on any build artifacts.

## Examples of file edits an assistant may perform

- Fix broken image path: update `Bilder\coming soon.png` → `Bilder/coming\ soon.png` (note spaces) or better: rename images to lowercase-without-spaces and update references.
- Make the tab-switching code robust: add `event` parameter to `opentab` instead of relying on global `event`, e.g. `function opentab(tabname, e) { e = e || window.event; ... }` and update callers `onclick="opentab('skills', event)"`.

## What not to change without permission

- Do not replace the font or CSS framework (Poppins + custom CSS) with external frameworks (Bootstrap/Tailwind) unless requested.
- Avoid adding package.json / node_modules; this repo intentionally has no build tooling.

If anything here is unclear or you want the instructions to include more details (e.g. coding style, automated previews, or image naming conventions) tell me which area to expand and I'll iterate.
