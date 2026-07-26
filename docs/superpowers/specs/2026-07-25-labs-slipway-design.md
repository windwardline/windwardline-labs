# labs.windwardline.com — design spec

Date: 2026-07-25. Direction approved by owner: **The Slipway** (of Slipway /
Hoist / Bench). Proof artifact:
https://claude.ai/code/artifact/7a85ba01-4ce0-464e-a2ff-f26eec13cb97

## Identity

- Division mark system (approved 2026-07-25): the house flies a swallowtail;
  divisions fly rectangular signal flags. **Labs flies the Blue Peter** — navy
  field, paper square; the signal for departure ("all hands aboard, sailing
  imminent"): a studio that ships. Approved forms: flag, halyard hoist,
  wordmark lockup, fleet hoist, app tile, favicon small cut (square grows
  below 32px). The triangular pennant is rejected — it breaks division grammar.
- Renditions: solid on paper; outline in dark theme; the theme, not the
  markup, selects the rendition (CSS variables on inline SVG).
- The house swallowtail appears exactly once, in the footer plate — the only
  gold on the page, plus the plate diamond and lamp dots.

## Page

One page. Top bar: Labs flag + WINDWARD LABS (EB Garamond 600, tracked), the
lamp, and "A division of Windward Line ↗". Hero: the division statement as
headline — "Product software, built end-to-end and run in production." with
"Four products in service under the Windward flag." Fleet: 2×2 hairline grid,
one cell per product (flag chip, IN SERVICE status, name ↗, one-liner, domain),
whole cell links out. Footer: house plate — swallowtail, A DIVISION OF WINDWARD
LINE, gold diamond separator, windwardline.com ↗ — and the copyright.

Product one-liners are drawn from each product's own live meta description.

## Type and palette

- Instrument Sans (variable 400–600, self-hosted latin subset) for everything;
  EB Garamond (variable roman) only for the brand name and plate.
- Light: ground #f6f5f0, ink #16213a, muted #5a6478, line #dcd9cf, signal blue
  #2b59c9 (fills/dots) with #1e4098 for blue text; cells #fbfaf6.
- Dark: ground #0f141e, ink #e7e9ee, muted #98a2b6, blue #8aa5f2/#a9bcf6,
  cells white at 3.5%; Labs flag renders outline; house flag outline gold
  #d9bd85. All text AA in both themes.
- The lamp (family pattern): three states, Labs phrasing DAY SHIFT / NIGHT
  SHIFT / SHIP'S TIME; default ship's time (OS); stored choice via
  localStorage + data-theme, applied pre-paint by blocking self-hosted
  script.js. Hidden in print; print forces daylight tokens.

## Engineering

Static, no build step. CSP: default/style/font/script all 'self', img 'self'
data:, everything else 'none' (mirrors apex vercel.json). All http(s) links
target="_blank" rel="noopener"; mailto exempt (none on this page). CI:
html-validate@9 + vercel.json parse. Repo conventions mirror windwardline-com
(LICENSE notice, SECURITY.md, Dependabot-ready workflows).
