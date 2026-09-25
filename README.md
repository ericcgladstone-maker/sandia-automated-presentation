# AI credibility in networked systems · automated presentation

Eric Gladstone · Sandia National Laboratories · Center for Computing Research ·
AI & Data Science Research · September 2026 (virtual panel, 17 September 2026).

A self-running web version of the 15-minute talk. The real v13 deck plays in a
16:9 frame and advances itself on a timeline. Beside it, the passage being spoken
is shown one paragraph at a time. The complete spoken text is available below,
collapsed. **13:05 at 1×.**

**Status: COMPLETE and LIVE.** Build complete 23 September 2026, approved by Eric.
Pushed live 25 September 2026.

- **Live:** https://sandiaautomated.eric-c-gladstone.workers.dev
- **Repo:** https://github.com/ericcgladstone-maker/sandia-automated-presentation

Do not change the build files listed in `CHECKSUMS.sha256` without a new decision
from Eric; any change should be verified with both checks and the manifest regenerated.
A change to the build files means redeploying the Worker and pushing the repo, or the
three copies drift apart.

Deployed 25 September 2026 to its own Cloudflare Worker, `sandiaautomated`, at
https://sandiaautomated.eric-c-gladstone.workers.dev. Build files are also on GitHub at
`ericcgladstone-maker/sandia-automated-presentation`. Nothing here touches the live
presentation (`sandiapresentation` Worker) or the Graystone website, both unchanged. The
dedicated talks page is still decided but not yet built.

### To embed

Copy `deck/`, `player.js`, `player.css` and `timeline.js` to one folder on the host
site (same origin as the page). On the host page, link `player.css` in the head and paste
the block between `PLAYER START` and `PLAYER END` from `index.html`, adjusting the four
paths. `tools/build-prototype.mjs` shows exactly those substitutions for Graystone.

## See it

```bash
cd "Website Automated Sandia 15 Minute Presentation"

# on its own
python3 -m http.server 8000 --bind 127.0.0.1
# open http://127.0.0.1:8000

# inside a local copy of the Graystone /systems/ page
python3 -m http.server 8080 --bind 127.0.0.1 --directory local-prototype/site
# open http://127.0.0.1:8080/systems/#research-presentation
```

Both need a web server, because the player talks to the deck inside its iframe.

## Files

| | |
|---|---|
| `deck/index.html` | byte-identical copy of v13 `dist/index.html`, the build the live URL serves. **Never edit.** |
| `PROSE.md` | prose, per-state duration and paragraph cues for all 23 states. Prose is final as supplied, less the opening stutter note (removed at Eric's request). |
| `timeline.js` | generated from `PROSE.md` by `node tools/build-timeline.mjs` |
| `index.html`, `player.js`, `player.css` | the standalone page and player. The block between `PLAYER START` / `PLAYER END` is what an embedding page uses. |
| `CHECKSUMS.sha256` | hashes of the final build files. `shasum -c CHECKSUMS.sha256` should print only OK. |
| `local-prototype/` | disposable local copy of the built Graystone site with the player in `/systems/`. Rebuild with `node tools/build-prototype.mjs`. |
| `tools/player-check.mjs` | 51 behaviour and layout checks in headless Chrome, standalone or embedded |
| `tools/full-run.mjs` | watches a complete 1× run in real time and checks every state change and highlight |

After editing `PROSE.md`: `node tools/build-timeline.mjs && node tools/build-prototype.mjs`,
then re-run both checks and regenerate `CHECKSUMS.sha256`.

## Timing

Durations follow spoken length: 150 words per minute plus a 3 s settle at the
start of each state, with 8 s minimum on question states. Paragraph cues fall
where the preceding spoken text ends. Edit any `m:ss` in `PROSE.md` to adjust.

## What a visitor can do

- **Watch.** Nothing plays until Play is pressed. Speed (0.75× to 1.5×) changes how
  long each page is held, not the deck's own animations.
- **Move around.** ‹ › beside Play change page. The page menu and Restart sit in a
  quieter row below. Clicking or keying inside the deck works as in the live talk,
  and the player follows and pauses.
- **Read along.** The column beside the deck shows only the current passage. On
  pages with several passages, ‹ n / m › steps among them without changing the
  deck. Stepping pauses playback and Play resumes from that passage. "Full spoken
  text" opens the whole talk, and clicking any paragraph jumps there.

## How it works

The deck needs no changes. Every click in it is one state advance, and all
animation within a state runs on the deck's own timers. The deck already exposes
`window.__seek(i)` and `window.__state()`. The player calls those, which works
because deck and player share an origin.

- **1920×1080 viewport.** The deck is always rendered in a true 1920×1080 iframe
  and scaled as a whole. Rendered into a smaller window, v13's own fit logic places
  the stage off-centre, which never showed at the full-screen size it was presented at.
- **Layout.** Side by side (deck ~69%, passage ~31%) when the player is at least
  1040px wide, a CSS container query on the player itself. Narrower, it stacks:
  deck, controls, current passage, full text.
- **Steady page height.** The passage area and full-text panel have fixed heights
  per width. Graystone's background network regenerates whenever the document height
  changes by more than 120px, so text that grew and shrank would redraw it constantly.
- **Scoping.** All CSS lives under `.sp`, parts are found by `data-sp` names, and
  keyboard shortcuts act only while focus is inside the player. On the prototype,
  every element outside the player has computed styles identical to the untouched page.
