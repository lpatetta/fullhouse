# Full House Label — site

Static site for **fullhouselabel.com**, built with [Astro](https://astro.build) and hosted free on Cloudflare.

## Run locally

```bash
npm install
npm run dev      # http://localhost:4321
npm run build    # outputs to dist/
```

## Editing content

All content lives in `src/data/` — no layout changes needed for day-to-day updates.

| File | What it controls |
|---|---|
| `src/data/videos.json` | The 7 videos. On every page load one is picked at random and shown full width; the other 6 show as thumbnails below. Clicking a thumbnail swaps it in. |
| `src/data/events.json` | Events list. Past events disappear automatically on the next build. The event with `"featured": true` (or the next one) fills the top hero with its flyer. |
| `src/data/links.json` | Listen links, follow links, the crew `@users` list, contact email. Links with an empty `url` are hidden. |
| `public/images/` | Flyers and other images. Reference them as `/images/<file>`. |

### Adding a video
Paste the full YouTube link into the `url` field of an entry in `videos.json`, e.g. `{ "url": "https://www.youtube.com/watch?v=AbC123xYz", "title": "..." }`. `youtu.be/`, `shorts/` and `embed/` links also work. The build fails if a link has no recognizable video ID.

## Deploy to Cloudflare

1. Push this folder to a GitHub repository.
2. Cloudflare dashboard → **Workers & Pages → Create → Import a repository** → pick the repo.
3. Build command: `npm run build` · Output directory: `dist`.
4. After the first deploy: **Custom domains → Set up a custom domain** → `fullhouselabel.com` (and `www`).

Every push to `main` redeploys the site.
