# Crate Dial — working rules

- **Keep PROMPT.md in sync.** PROMPT.md is the reusable prompt that rebuilds Crate Dial Radio. Any change to the radio, the builder, `tracks.js`, the sources, genres, controls, loops or the weekly refresh must update PROMPT.md in the same commit. It should always describe the site as it is now.
- Keep README.md accurate too.
- `tracks.js` is the one shared track pool (`window.CRATE = {updated, span, raw}`). Both `index.html` and `radio.html` read it.
- No build step: each page is a single self-contained HTML file served by GitHub Pages from `main`.
