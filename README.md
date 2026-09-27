# Krom FM v4

A kid's pretend radio station: Spotify songs, jingles, news and DJ talk in one running order.
Live at **https://arcuscapital.github.io/djraf3/**. Earlier versions stay live for comparison:
v3 at https://arcuscapital.github.io/djraf2/, v2 at https://arcuscapital.github.io/djraf/, and the
original at https://arcuscapital.github.io/raf-radio-station/.

v4 = v3 plus ☰ song order: a ☰ on the Songs box (before the show) and on the live screen lists
the playlist in play order; press and hold a song (or grab its ≡) and drag it. Mid-show, songs
already played and the one playing are locked; if the songs block that's on now changes, Spotify
is handed the new list and carries on with the current song from where it was.

## How it avoids repeated songs
Each "Play N Songs" block hands Spotify an exact list of tracks (`PUT /me/player/play {uris}`).
Spotify plays them back to back and stops by itself after the last one — no playlist, no repeat
mode, nothing to race. `src/runWatch.ts` notices the stop and the show moves on.

## Setup (once)
- Spotify developer dashboard → the Krom FM app → Redirect URIs → add `https://arcuscapital.github.io/djraf3/`.
- Spotify Premium is required for playback control.

## Develop
```
npm install
npm run dev     # http://localhost:5064/djraf3/
npm test
npm run build
```
Every push to `main` builds, tests and deploys via GitHub Actions. Built files get unique names and
`version.json` lets an open copy of the app reload itself when a newer build is live.
