# Windward Labs — operating contract

Operating contract for AI work in this repo; the global `~/AGENTS.md` still applies. Work here follows the CONVERGE cycle and delivery discipline in `FLEET.md` (windwardline/windwardline) — find → refute → verify yourself → fix → re-rank → test → update → report; enumerate the gates rather than counting them, stage explicit paths, validate before mutating, preserve standing claims, derive populations rather than curating them, and never let a harness failure read as the subject refusing. `FLEET.md` governs where it and this summary differ. The software division site — the product register. Live at labs.windwardline.com. Zero-dependency static HTML.

## Commands

Any static server for preview. CI-equivalent: `npx --yes html-validate@9 index.html` · JSON-parse `vercel.json`.

## Gates

CI is `ci.yml` — html-validate on `index.html` plus the `vercel.json` parse, on every push to `main` and every pull request into it, on Node 24 with both tools fetched per run so the site itself stays zero-dependency. `schedule.html` and `script.js` are not checked. Push to main deploys production. A parallel `security.yml` (PRs, pushes, weekly cron; a daily cron runs only the production headers probe) gates Semgrep and secret scan; a post-deploy job asserts the production security headers. The required `Secret scan` job also runs the pinned `actions/verify-action-pins` step; a mutable third-party `uses:` reference or a full-SHA/immutable-tag comment mismatch fails that required check. An advisory Claude review runs on every eligible same-repo pull-request event via `claude-review.yml` when `github.event.pull_request.user.login` — the PR author, stable across reruns — is not `dependabot[bot]` and the base equals the repository's dynamic default branch; forks and events without the `CLAUDE_CODE_OAUTH_TOKEN` secret skip by design. The caller deliberately uses the fleet reusable at `@main`, so one merge updates every repo; reviews bill the owner's Claude subscription, not Console credits.

`dependabot-auto-merge.yml` merges nothing itself. It arms GitHub's native auto-merge so the repo's `main-requires-green-ci` ruleset stays the only thing that decides whether a merge happens, and it asserts that gate rather than assuming it — a repo with `allow_auto_merge` off or no required status check is a hold, because `gh pr merge --auto` would otherwise degrade to an immediate merge. It runs only for `dependabot[bot]` pull requests opened on this repo under this owner, so forks never reach it, and it holds for a human on major bumps, the `no-automerge` label, a release that changed maintainers, pre-1.0 packages, empty or unverifiable metadata, and an unrecognised update type — withdrawing an auto-merge it armed earlier rather than merely not renewing it, since a rebase can make a compliant PR non-compliant. Empty or unverifiable metadata and an unrecognised update type are distinct holds. `dependabot.yml` groups this repo's GitHub Actions updates into one PR; `fetch-metadata` reports the highest semver change across the whole grouped PR, so one held member holds the group and the arm-or-hold decision applies to that grouped PR. Majors that reach classification are labelled `deferred-major`. It mints a GitHub App token when `FLEET_AUTOMERGE_APP_ID` and `FLEET_AUTOMERGE_PRIVATE_KEY` are present as **Dependabot** secrets (Actions secrets are unreadable from a Dependabot run and resolve to empty rather than erroring) and degrades to `GITHUB_TOKEN` when they are absent; on that fallback path the merge commit creates no workflow run at all, so `security.yml`'s push-triggered `Headers live` probe does not fire for it. The file is byte-identical in every fleet repo that takes it — see `FLEET.md`; it is not edited here alone — and its check must never become a required one: the job carries no `name:`, so it renders exactly `dependabot-auto-merge`, the string the fleet conformance audit excludes.

## The register law

A product launch or retirement moves four places here in the same change set, then two sibling repos:

1. Grid cell in `index.html` (`<section class="fleet">`): `<a class="cell">` with the lflag SVG, `cell-status`, `cell-name` + ↗, `cell-desc`, `cell-domain`.
2. Hero count in `index.html` — word-spelled ("Five products in service…").
3. Meta description in `index.html` — the count word and the full name list, Oxford comma.
4. The `README.md` product list.

Then the portfolio repo and both repos' READMEs update in the same change (the standing launch-registry rule). Current order: Pathfinder, Levelflow Cloud, Mimic, That's Extra, Proper Form.

## Laws

- Koalendar slug `windward-labs` is hardcoded in `schedule.html`; CSP `frame-src https://koalendar.com` in `vercel.json`; change both together.
- Labs is the only division with the blue accent: `--blue #2b59c9` / `--blue-ink #1e4098` (dark `#8aa5f2` / `#a9bcf6`), alongside the shared `--gold`.
- `cleanUrls: true` maps `/schedule` → `schedule.html`. `.vercelignore` excludes `docs/`.
- `fonts/` is OFL 1.1 territory, carved out of the proprietary `LICENSE`. `fonts/OFL.txt` carries the copyright line for every family in the directory and the verbatim license; it ships with the fonts and is never deleted. Adding or replacing a font adds or replaces its copyright line, taken from the font's own `name` table, not from memory.

## Declared gates

The machine-readable gate set. `scripts/fleet-conformance.sh` requires this block
and the workspace done-gate hook runs every `gate:` line before a session may
finish, so what runs is what is written here rather than what a hook guessed from
`package.json`. Each key states its own boundary: `gate:` runs at session end and
must be local and quick; `release:` runs before a pull request and may be slow;
`cadence:` is scheduled or needs the live machine and is run by neither.

```fleet-gates
gate: npx --yes html-validate@9 index.html
gate: node -e "JSON.parse(require('fs').readFileSync('vercel.json','utf8'))"
```
