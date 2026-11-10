# .github — org profile & shared config for materia-ops

Small but high-blast-radius repo: files here are consumed org-wide.
This repo is PUBLIC — nothing sensitive, ever.

## Contents
- `renovate/default.json` — org-wide Renovate policy. Each repo's
  config extends it LAST
  (`github>materia-ops/.github//renovate/default`) so it overrides
  upstream presets. The org ruleset forbids direct pushes to the
  default branch of every Renovate-managed repo, so automerge must stay
  PR-based (`automergeType: "pr"` + `platformAutomerge`) — don't
  reintroduce branch automerge. The preset sets how automerge happens,
  not whether: each repo's own rules decide that.
- `renovate/README.md` — why the preset is strict JSON named
  `default.json` (a `.json5` name is never resolved by Renovate) and
  where the policy rationale lives.
- `labels.yaml` — org label set (see its header for the sync contract).
  Deleting an entry deletes that label wherever the sync applies it.
- `.github/workflows/label-sync.yaml` — fans `labels.yaml` out to every
  repo in the org (nightly, and on every `labels.yaml` change). The
  nightly run is not a standing guarantee: GitHub disables scheduled
  workflows in a public repo after 60 days without repository
  activity (commits count, workflow runs do not), so check the workflow
  is still enabled when this repo has been quiet.
- `.github/workflows/label-sync-watchdog.yaml` — report-only check for
  that lapse: reads the Label Sync's state and last successful run and
  opens one issue, in the repo that runs it, when the sync is disabled
  or stale. It is a reusable workflow with no schedule of its own — a
  schedule here would lapse with the one it watches — so it only
  guards the sync while an active repo calls it on a schedule. It
  changes nothing; re-enabling the sync stays a manual step.
- `profile/README.md` — the public org profile page.
- `README.md` — the repo's own landing blurb.
- `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, `SECURITY.md`,
  `.github/ISSUE_TEMPLATE/`, `.github/PULL_REQUEST_TEMPLATE.md` —
  org-default community health files; every org repo without its own
  copy inherits these.

## Rules
- Treat every edit as a fleet-wide change: small PRs, Conventional
  Commits (`type(scope):`), merged by the maintainer — a session merges
  only when the maintainer explicitly asks it to land that PR.
- The merge button is squash-only and the squash commit takes the PR
  title, so the PR title must itself be a Conventional Commit.
- Renovate-config edits: keep `default.json` strict JSON (no comments,
  never rename it to `.json5` — see `renovate/README.md`) and re-read
  that README plus the description fields in the file first — the
  constraints they document (org ruleset, no direct pushes, Aqua's IP
  allow list) are why the settings look the way they do.

## Work docs

Code-describing docs (architecture, CI, troubleshooting) live in this
repo. Work-describing docs — decisions, plans, handovers, reviews,
prompts, anything cross-repo — live in the private
`materia-ops/materia-vault` Obsidian vault; its root CLAUDE.md holds
the note contract.
