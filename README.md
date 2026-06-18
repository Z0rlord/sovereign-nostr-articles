# Nostr kind:30023 Article Reader

Single-page HTML app for the [Sovereign Engineering](https://sovereignengineering.io) YOLO:8 cohort.

Fetches **21** long-form Nostr articles (`kind:30023`, [NIP-23](https://github.com/nostr-protocol/nips/blob/master/23.md)) from public relays, displays title, author profile (name + picture), and timestamp, with hashtag filtering from `t` tags.

## Live demo

https://z0rlord.github.io/sovereign-nostr-articles/

## Features

- Fetches 21 `kind:30023` articles from multiple public relays
- Hashtag sidebar with counts (from `t` tags) and checkboxes
- **AND / OR** filter toggle
- Author metadata from `kind:0` profile events (name, picture)
- Timestamps from `published_at` tag or `created_at`

## Run locally

No build step. Serve the file with any static server:

```bash
python3 -m http.server 8080
# open http://localhost:8080
```

Or open `index.html` directly in a browser (some browsers block module imports from `file://`; a local server is recommended).

## Stack

- Vanilla HTML/CSS/JS
- [nostr-tools](https://github.com/nbd-wtf/nostr-tools) via esm.sh
- GitHub Pages for deployment

## Relays

- `wss://relay.dojopop.live` — DojoPop relay (primary; profiles + connectivity)
- `wss://relay.damus.io`
- `wss://nos.lol`
- `wss://relay.primal.net`
- `wss://relay.nostr.band`

Each relay is queried independently so one failure does not block the rest. Relay chips in the UI show green (connected), red (failed), or gray (pending).

Note: DojoPop relay allowlists specific event kinds for publishing; `kind:30023` articles are fetched from public relays, while DojoPop helps with author profiles (`kind:0`) and reliable connectivity.
