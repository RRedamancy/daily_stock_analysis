# Weekday Schedule 15:38 Design

## Goal

Run the daily analysis workflow once on every weekday at 15:38 Beijing time, away from the high-load period near the start of each UTC hour.

## Scope

- Replace the existing schedule with `38 7 * * 1-5` (UTC 07:38, Beijing 15:38).
- Update both comments in `.github/workflows/00-daily-analysis.yml`.
- Replace the 09:08 example and reference-table entry in `docs/full-guide.md` and `docs/full-guide_EN.md`.
- Update the existing `[Unreleased]` schedule entry in `docs/CHANGELOG.md` instead of adding a duplicate history line.
- Keep `workflow_dispatch`, trading-day checks, concurrency behavior, job steps, and notification behavior unchanged.

## Verification

- Confirm the workflow contains exactly one weekday schedule: `38 7 * * 1-5`.
- Confirm the four affected files contain no stale `09:08`, `UTC 01:08`, or `8 1 * * 1-5` schedule references.
- Run `git diff --check` and inspect the final diff.
- After pushing, read the workflow from GitHub and confirm it is active on `main`.

## Risk And Rollback

GitHub scheduled workflows may still be delayed or dropped because they are not an exact-time service. Rollback is a one-line cron change plus matching documentation updates.
