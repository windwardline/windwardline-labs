# Windward Labs — operating contract

Operating contract for AI work in this repo; the global `~/AGENTS.md` still applies. The software division site — the product register. Live at labs.windwardline.com. Zero-dependency static HTML.

## Commands

Any static server for preview. CI-equivalent: `npx --yes html-validate@9 index.html` · JSON-parse `vercel.json`.

## Gates

CI is html-validate on `index.html` plus the `vercel.json` parse. `schedule.html` and `script.js` are not checked. Push to main deploys production.

## The register law

A product launch or retirement moves four places here in the same change set, then two sibling repos:

1. Grid cell in `index.html` (`<section class="fleet">`): `<a class="cell">` with the lflag SVG, `cell-status`, `cell-name` + ↗, `cell-desc`, `cell-domain`.
2. Hero count in `index.html` — word-spelled ("Six products in service…").
3. Meta description in `index.html` — the count word and the full name list, Oxford comma.
4. The `README.md` product list.

Then the portfolio repo and both repos' READMEs update in the same change (the standing launch-registry rule). Current order: Pathfinder, Levelflow Cloud, TimeShift, Mimic, That's Extra, Proper Form.

## Laws

- Koalendar slug `windward-labs` is hardcoded in `schedule.html`; CSP `frame-src https://koalendar.com` in `vercel.json`; change both together.
- Labs is the only division with the blue accent: `--blue #2b59c9` / `--blue-ink #1e4098` (dark `#8aa5f2` / `#a9bcf6`), alongside the shared `--gold`.
- `cleanUrls: true` maps `/schedule` → `schedule.html`. `.vercelignore` excludes `docs/`.
