# .github — org profile & shared config for materia-ops

Small but high-blast-radius repo: files here are consumed org-wide.
This repo is PUBLIC — nothing sensitive, ever.

## Contents
- `renovate/default.json5` — org-wide Renovate policy. Each repo's
  config extends it LAST
  (`github>materia-ops/.github//renovate/default`) so it overrides
  upstream presets. The org ruleset forbids direct pushes to default
  branches, so automerge must stay PR-based (`automergeType: "pr"` +
  `platformAutomerge`) — don't reintroduce branch automerge.
- `labels.yaml` — org label set (see its header for the sync contract).
  Deleting an entry deletes that label wherever the sync applies it.
- `profile/README.md` — the public org profile page.

## Rules
- Treat every edit as a fleet-wide change: small PRs, Conventional
  Commits (`type(scope):`), merged by the maintainer, not by sessions.
- Renovate-config edits: keep the JSON5 valid and re-read the comment
  block in the file — the constraints it documents (org ruleset, no
  direct pushes) are why the settings look the way they do.
