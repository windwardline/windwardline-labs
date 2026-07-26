# labs.windwardline.com

Windward Labs, the software division of Windward Line. Four products in
service: [Pathfinder](https://pathfinder.windwardline.com),
[LevelFlow Cloud](https://levelflow.windwardline.com),
[TimeShift](https://timeshift.windwardline.com), and
[Mimic](https://mimic.windwardline.com).

Static site, no build step: one HTML file, one stylesheet, self-hosted
Instrument Sans and EB Garamond, the division signal flag as inline SVG, and
the lamp (day shift / night shift / ship's time) for theme control. Design
spec: [docs/superpowers/specs/2026-07-25-labs-slipway-design.md](docs/superpowers/specs/2026-07-25-labs-slipway-design.md).

Deployed on Vercel; DNS on Cloudflare. Pushes to `main` deploy to production.
Security headers are set in [vercel.json](vercel.json).
