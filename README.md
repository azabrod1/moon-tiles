# moon-tiles

Sector surface tiles for **Moon**, a Three.js planetarium — the streamed
detail its hero bodies (Earth, the Moon, Mars) draw close up. Data only:
no code, nothing to build or run here. Written by `tools/publish-tiles.mjs`
in the app repo; not edited by hand.

## The rule: a published path never moves

A set lives at `textures/tiles/<key>/<tier>.<setHash8>/<c>_<r>.webp`, and that
folder name is a hash over the set's own bytes. The app is built against a
stable ref — `VITE_TILE_ORIGIN=https://cdn.jsdelivr.net/gh/azabrod1/moon-tiles@<ref>` — and every layer
between it and here (jsDelivr, the app's service worker, the browser cache)
keeps a tile forever without revalidating it. That is only safe while a
pathname means those exact bytes or a 404.

So: never edit, move or overwrite a set folder that is already here — a re-cut
set has a different hash and arrives as a new folder beside the old one; never
rewrite the history of the ref the app is built against; and leave old sets in
place after the app stops naming them, because a browser still running the
older build keeps asking for them. Pruning is deliberate and by hand, and a
pruned set 404s those clients (the app falls back to its whole-body map).

`textures/tiles/sets.v1.json` is the table of what is here: every <key>/<tier> a
publish has named, at the latest cut of each, merged in from each root that was
published (older cuts stay on disk under their own hashes).
