# Game Night Menu

A single-file board game catalog for game night.

**Live:** <https://mrrlexy.github.io/boardgame/> ·
Part of [The Brain](https://mrrlexy.github.io/The-Brain/)

**Features:**
- Browse, search, and filter your collection by players, time, and complexity
- Filter by owned / want-to-play / wishlist status
- Cover art, descriptions, categories and mechanics from BoardGameGeek
- Random game picker ("Pick for me")
- Print catalog — one card per page with full art and stats
- Dark mode toggle
- No build step — `index.html` is self-contained

## How the data works

Two separate things:

- **The collection itself** is inlined in `index.html` as JSON, in
  `<script id="games-data">`. 146 games. Edit there to add or remove one.
- **Cover art and descriptions** come from
  [boardgame-assets](https://github.com/MrrLexy/boardgame-assets), loaded over
  jsDelivr's CDN in a single request at page load.

It did originally fetch from BoardGameGeek live, through a public CORS proxy.
That no longer works — BGG's `xmlapi2` returns `401 Unauthorized` to
unauthenticated requests. The pre-fetched assets repo replaced it, which also
made the page load faster and removed the rate-limit failures.

### After adding games

Refresh the assets so new games get covers:

```bash
cd ../boardgame-assets
node scripts/fetch-bgg-assets.mjs
git add covers data && git commit -m "Add covers for new games" && git push
```

The script reads the game list straight out of this repo's `index.html`, so both
repos need to be checked out side by side. jsDelivr may cache for a few minutes.

## Styling

Warm "cozy café" palette — cream/latte background, terracotta/sage/honey
accents, soft shadows, Fraunces for display type. Dark mode is a deep warm
brown, not black. All theming is CSS custom properties in `:root` and
`[data-theme="dark"]` at the top of the file.
