# Crate Dial

A one-page playlist builder that pulls 10, 20 or 25 tracks by genre from KCRW Eclectic24, Gilles Peterson's Worldwide FM show, Somewhere Soul's New Music Friday, Club Carter Radio, Mark Torkington's Mixcloud sets, Oleg Tsoy's Rare Samples & Songs and Mayer Hawthorne's Wine & Vinyl Hour.

- `index.html` — playlist builder. Open in a browser; no build step.
- `radio.html` — Crate Dial Radio: non-stop play from every station via YouTube embeds, live station/genre toggles, back/next, tap tempo and 2- or 4-bar loops. Needs a free YouTube Data API v3 key (pasted in the page, stored only in your browser).
- `tracks.js` — the shared track pool both pages read. Refreshed weekly by a scheduled task.

Live site: https://shauhn.github.io/cratedial/ · radio: https://shauhn.github.io/cratedial/radio.html
