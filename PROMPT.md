# Prompt: build Crate Dial Radio

Paste this into Claude (or another coding assistant) to rebuild or extend the radio from scratch.

---

I have a static site, Crate Dial (repo `shauhn/cratedial`, GitHub Pages at https://shauhn.github.io/cratedial/). `index.html` is a playlist builder. Its track pool covers 7 sources: KCRW Eclectic24, Gilles Peterson on Worldwide FM, Somewhere Soul New Music Friday, Club Carter Radio, Mark Torkington's Mixcloud sets, Oleg Tsoy's Rare Samples & Songs, and Mayer Hawthorne's Wine & Vinyl Hour. Each track is stored as `source|show|artist|title|genre tags`. The genre tags are jazz, soul, brazil, global, electronic, hiphop, indie and folk.

Build **Crate Dial Radio** as `radio.html`. It must be one self-contained page, with no build step, that works well on a phone.

**Data**
- Move the track pool into a shared `tracks.js` (`window.CRATE = {updated, span, raw}`). Both pages should read it.

**Playback**
- Play full songs through the YouTube IFrame Player API.
- To find each song, search the YouTube Data API v3 for `artist + title` with `type=video`, `videoEmbeddable=true` and `videoSyndicated=true`.
- The user pastes their own API key into the page. Store the key only in localStorage, and cache video IDs per song so each song costs one lookup at most.
- If a video won't embed (errors 101/150/100), try the next search result, then skip the song.
- When the daily quota runs out, keep playing only songs that are already cached.
- Play non-stop. Rotate evenly across the enabled stations. Don't repeat a song until everything that fits has been heard. Keep the same artist out of the last ~8 songs.
- Show "Up next" (5 songs), with Play and Remove on each.

**Live controls while playing**
- Station toggles and genre toggles, multi-select, with counts. Changes rebuild the upcoming queue right away.
- If the song that's playing no longer fits, skip it immediately.
- Add a "Mute <station>" button on the now-playing song.
- Remember the settings between visits.

**Transport**
- Play/pause, back, next, and a seek bar.
- Back restarts the song if you're more than 4 s in; otherwise it goes to the previous song. Going back then next returns to where you were.
- Wire up Media Session for lock-screen controls.
- Keyboard: Space, ←/→, T, 2, 4, 0.

**Loops**
- 2-bar and 4-bar loop buttons, assuming 4/4. Loop length = bars × 4 × 60/BPM.
- Tap tempo (4+ taps). Also add BPM −/+, ½× and 2×. Save the BPM per song.
- The first tap anchors a beat grid, and the loop start snaps to it.
- Buttons to nudge the loop by a beat and shift it by a bar.
- Show the loop region on the seek bar.
- Use a ~20 ms watcher that seeks back to the loop start at the loop end.

**Weekly refresh**
- Set up a weekly scheduled task. It should re-pull the newest tracklists from all 7 sources and update `tracks.js` (add new songs, drop episodic shows older than ~8 weeks, never invent tracks).
- It should then verify the file parses and push to main.

Match the existing visual style (Unbounded / IBM Plex, the station colors, light and dark mode). Test the logic headlessly with a mocked YouTube player before pushing.
