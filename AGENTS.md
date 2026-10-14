# Instructions for AI agents and contributors

This is a static Astro site. Keep changes small and data-driven.

- **Content changes go in `src/data/*.json` only.** Do not hard-code events, videos or links in `src/pages/index.astro`.
- **New event:** append an object to `src/data/events.json` with `date` (YYYY-MM-DD), `time`, `name`, `venue`, `address`, `image` (put the flyer in `public/images/`, kebab-case filename), `tickets` (URL). `image` and `tickets` are optional (e.g. for past events). Past events stay listed under EVENTOS, marked JÁ ROLOU. Set `"featured": true` on at most one event; remove it from the previous one.
- **Videos:** `src/data/videos.json` must keep exactly 7 entries (`url` = full YouTube video URL, `title`); the video ID is derived from the URL at build time.
- **Crew:** `links.json → crew` is a list of Instagram handles, with or without `@`.
- Copy on the site is in Brazilian Portuguese.
- Run `npm run build` before committing; it must finish without errors.
