# Krom FM v3

A kid's pretend radio station: Spotify songs, jingles, news and DJ talk in one running order.
Live at **https://arcuscapital.github.io/djraf2/**. Earlier versions stay live for comparison:
v2 at https://arcuscapital.github.io/djraf/ (repo arcuscapital/djraf) and the original at
https://arcuscapital.github.io/raf-radio-station/.

v3 changes: songs only from "Use what's playing" (big red button, green once loaded); one
background music (Raf's song, bundled in `src/assets/`, played at 20% volume and looped);
blocks are just Talk or Record, each with a Background music button that's off until tapped;
recordings have no time limit.

## How it avoids repeated songs
Each "Play N Songs" block hands Spotify an exact list of tracks (`PUT /me/player/play {uris}`).
Spotify plays them back to back and stops by itself after the last one — no playlist, no repeat
mode, nothing to race. `src/runWatch.ts` notices the stop and the show moves on.

## Setup (once)
- Spotify developer dashboard → the Krom FM app → Redirect URIs → add `https://arcuscapital.github.io/djraf2/`.
- Spotify Premium is required for playback control.

## Develop
```
npm install
npm run dev     # http://localhost:5058/djraf2/
npm test
npm run build
```
Every push to `main` builds, tests and deploys via GitHub Actions. Built files get unique names and
`version.json` lets an open copy of the app reload itself when a newer build is live.
