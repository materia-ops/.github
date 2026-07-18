# .github — org profile & shared config for materia-ops

Small but high-blast-radius repo: files here are consumed org-wide.
This repo is PUBLIC — nothing sensitive, ever.

## Contents
- `renovate/default.json` — org-wide Renovate policy. Each repo's
  config extends it LAST
  (`github>materia-ops/.github//renovate/default`) so it overrides
  upstream presets. The org ruleset forbids direct pushes to default
  branches, so automerge must stay PR-based (`automergeType: "pr"` +
  `platformAutomerge`) — don't reintroduce branch automerge.
- `renovate/README.md` — why the preset is strict JSON named
  `default.json` (a `.json5` name is never resolved by Renovate) and
  where the policy rationale lives.
- `labels.yaml` — org label set (see its header for the sync contract).
  Deleting an entry deletes that label wherever the sync applies it.
- `.github/workflows/label-sync.yaml` — fans `labels.yaml` out to every
  repo in the org.
- `profile/README.md` — the public org profile page.
- `README.md` — the repo's own landing blurb.

## Rules
- Treat every edit as a fleet-wide change: small PRs, Conventional
  Commits (`type(scope):`), merged by the maintainer, not by sessions.
- Renovate-config edits: keep `default.json` strict JSON (no comments,
  never rename it to `.json5` — see `renovate/README.md`) and re-read
  that README plus the description fields in the file first — the
  constraints they document (org ruleset, no direct pushes, Aqua's IP
  allow list) are why the settings look the way they do.
