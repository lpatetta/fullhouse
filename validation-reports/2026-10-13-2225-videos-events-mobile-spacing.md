## Validation Report: Video URLs, past events, crew list, mobile spacing
**Date**: 2026-10-13 22:25
**Commit**: see the commit that adds this file
**Status**: PASSED (with a documented, pre-existing dependency issue)

### Changes
- `videos.json` entries use a full YouTube `url`; the video ID is derived at build time (build fails on an unrecognized URL).
- Video section: featured video sits inside the page gutter; thumbnail grid is 3 columns (2 below 900px, 1 below 520px).
- Crew ("A FAMÍLIA FULL HOUSE"): vertical list of text links instead of bordered cells.
- Events: past events listed after upcoming ones, dimmed and marked "JÁ ROLOU"; `image` and `tickets` optional.
- Featured event date line reads e.g. "SÁBADO 31 DE OUTUBRO".
- Mobile (≤720px): `.wrap` now sets only side padding (the previous `padding` shorthand zeroed the vertical padding of nav, hero, OUVIR, SEGUIR, EVENTOS and footer); vertical spacing scaled down for phones.
- Content: new past events in `events.json`, Drop Night tickets link.

### Phase 3: Tests
- Test suite: none in project. `npm run build` — completes without errors.
- Manual: all 7 YouTube IDs return 200 for thumbnail and oEmbed; mobile layout checked at 390px via Playwright screenshot (no horizontal overflow, vertical padding present on all sections).
- Status: PASSED

### Phase 4: Code Quality
- Dead code: none found. Duplication: none significant. Encapsulation: data helpers (`youtubeId`, `longDate`, `fmt`) in frontmatter.
- Status: PASSED

### Phase 5: Security Review
- Dependencies: `npm audit` — 3 vulnerabilities (Critical: 1 astro <=7.2.7, High: 1 sharp, Low: 1 esbuild). All are build-time dependencies; affected features (server islands, define:vars, spread props, view transitions, image optimization, dev server on Windows) are not used by this static site. Fix requires a major upgrade (astro 5 → 7); deferred to a separate change.
- OWASP: static output, no user input. Video data is embedded via `JSON.stringify` in a `<script type="application/json">`; data is owner-controlled. External links use `rel="noopener"`.
- Secrets: none in changed files.
- Status: PASSED (dependency upgrade deferred, documented above)

### Phase 5.5: Release Safety
- Change type: Code + content (static site)
- Rollback plan: `git revert <commit>` and push; the host redeploys the previous build.
- Status: PASSED

### Overall
- All gates passed: YES (dependency upgrade outstanding)
