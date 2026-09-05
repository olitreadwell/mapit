# mysociety/mapit context
> refreshed 2026-09-05 | upstream default: master @ 137da94

## Identity & policies
- upstream: mysociety/mapit, default branch master, primary language Python/Django, English-first (yes)
- CLA/DCO: none (policy passport: cla_required false, dco_required false)
- AI-assisted PR policy: unstated (bans_ai false, ai_disclosure_required false) — fork PR bodies/commits carry no AI mention; promotion-time disclosure per config
- signed commits required: no
- PR template: NONE (pr_template_present false) -> pipeline 3-section fallback body + exactly one PROMOTION NOTE + verify block
- external tracker: github

## Conventions (verified from merged PRs)
- maintainer @dracos commits directly and reviews/merges outside PRs promptly (e.g. #430 torotil merged 2024-06, #415 mikejamesthompson merged 2023-11; open external #440 RossLYoung, #444 c-tonneslan, #422 lucascumsille).
- test command (tox envlist flake8, py310-{4.2,5.2}): `flake8 mapit mapit_gb mapit_it mapit_no mapit_se mapit_za project` then Django tests on py310 against PostGIS. Test jobs need a PostGIS database.
- lint config: tox.ini [flake8] max-line-length=119, ignore=E123,E722,W503. flake8 PASSES at HEAD.
- CI: .github/workflows/default.yml — matrix flake8 + Django 4.2/5.2 on python 3.10, postgis/postgis:15-3.5 service, gdal-bin.

## Maintainer picture
- active maintainers: @dracos (Matthew Somerville, mySociety), @davea. Active + responsive.
- avoid in-flight maintainer work: psycopg3/Django 6 (#442 open), area m2m migration (#315 WIP), annual OS Boundary-Line imports.

## Issue-area health
- open issues are mostly old wishlist/feature requests, many untouched for years; no maintainer-engaged open bug issue currently claimable.
- #421 (API returns HTML for 404s) is claimed by open PR #444 -> previously dropped (tried-repos 2026-08-24). Do not re-pick.
- #448 (override delete confirmation page, updated 2026-06) is a feature request, not claimed; not a low-risk pick.

## Gap ledger (dedupe — READ FIRST, never re-pick)
- 2026-08-24 issue #421 — outcome dropped(claimed, PR #444 addresses it) — lesson: always check open PRs before re-picking an issue
- 2026-09-05 self-found gap (config-docs drift: stale COUNTRY lists KE/SA, omit SE) — outcome pr-opened — PR link in this run's log

## Mined gaps (discovered, not yet attempted)
- 2026-09-05 config-docs: `conf/general.yml-example:14` and `project/settings.py:32` country comments are stale — they list non-existent country codes KE and SA and omit SE. Authoritative source `mapit/countries/__init__.py` dispatches on GB, NO, IT, SE, ZA (+ external Global). git history: mapit_ke and mapit_sa never existed; mapit_se added c0858cc; mapit_za added 1e422a1 (SA was a mistake for ZA/South Africa). Fix both comments to "GB, NO, IT, SE, or ZA". Verify: flake8 passes; comments-only so no tests affected. Dedupe: no upstream issue/PR references this. status: attempted (2026-09-05)
