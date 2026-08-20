# Windward Labs — operating contract

Operating contract for AI work in this repo; the global `~/AGENTS.md` still applies. Work here follows the CONVERGE cycle and delivery discipline in `FLEET.md` (windwardline/windwardline) — find → refute → verify yourself → fix → re-rank → test → update → report; enumerate the gates rather than counting them, stage explicit paths, validate before mutating, preserve standing claims, derive populations rather than curating them, and never let a harness failure read as the subject refusing. `FLEET.md` governs where it and this summary differ. The software division site — the product register. Live at labs.windwardline.com. Zero-dependency static HTML.

## Commands

Any static server for preview. CI-equivalent: `npx --yes html-validate@9 index.html` · JSON-parse `vercel.json`.

## Gates

CI is `ci.yml` — html-validate on `index.html` plus the `vercel.json` parse, on every push to `main` and every pull request into it, on Node 24 with both tools fetched per run so the site itself stays zero-dependency. `schedule.html` and `script.js` are not checked. Push to main deploys production. A parallel `security.yml` (PRs, pushes, weekly cron; a daily cron runs only the production headers probe) gates Semgrep and secret scan; a post-deploy job asserts the production security headers. An advisory Claude review runs on every same-repo PR via `claude-review.yml`, which deliberately calls the fleet reusable at `@main` — one merge updates every repo. It activates only when the `CLAUDE_CODE_OAUTH_TOKEN` secret is present — reviews bill the owner's Claude subscription, not Console credits; fork PRs never receive secrets, so they skip it by security design.

`dependabot-auto-merge.yml` merges nothing itself. It arms GitHub's native auto-merge so the repo's `main-requires-green-ci` ruleset stays the only thing that decides whether a merge happens, and it asserts that gate rather than assuming it — a repo with `allow_auto_merge` off or no required status check is a hold, because `gh pr merge --auto` would otherwise degrade to an immediate merge. It runs only for `dependabot[bot]` pull requests opened on this repo under this owner, so forks never reach it, and it holds for a human on major bumps (labelling them `deferred-major` first, so they still reach the deferred-majors issue), the `no-automerge` label, a release that changed maintainers, pre-1.0 packages, and metadata it cannot verify — withdrawing an auto-merge it armed earlier rather than merely not renewing it, since a rebase can make a compliant PR non-compliant. It mints a GitHub App token when `FLEET_AUTOMERGE_APP_ID` and `FLEET_AUTOMERGE_PRIVATE_KEY` are present as **Dependabot** secrets (Actions secrets are unreadable from a Dependabot run and resolve to empty rather than erroring) and degrades to `GITHUB_TOKEN` when they are absent; on that fallback path the merge commit creates no workflow run at all, so `security.yml`'s push-triggered `Headers live` probe does not fire for it. The file is byte-identical in every fleet repo that takes it — see `FLEET.md`; it is not edited here alone — and its check must never become a required one: the job carries no `name:`, so it renders exactly `dependabot-auto-merge`, the string the fleet conformance audit excludes. Dependabot itself watches only the `github-actions` ecosystem here, weekly and grouped into a single PR.

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
- `fonts/` is OFL 1.1 territory, carved out of the proprietary `LICENSE`. `fonts/OFL.txt` carries the copyright line for every family in the directory and the verbatim license; it ships with the fonts and is never deleted. Adding or replacing a font adds or replaces its copyright line, taken from the font's own `name` table, not from memory.
