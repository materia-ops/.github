# Org-wide Renovate policy for materia-ops

`default.json` is the shared preset every fleet repo extends **last**, so it
overrides upstream presets:

```json5
extends: [
  "github>home-operations/renovate-presets#2.1.0",
  "github>materia-ops/.github//renovate/default",
]
```

Why it exists: the org ruleset forbids direct pushes to default branches (no
bypass), so upstream `:automergeBranch` presets would be rejected at push.
This preset forces every automerge through a PR that Renovate then
auto-merges (the ruleset requires 0 approvals, so it stays hands-off).

Why it is strict JSON named `default.json`, not json5: renovate resolves an
extensionless `github>owner/repo//path/default` preset by fetching
`default.json` (falling back to `renovate.json`) — a `default.json5` file is
never tried and every consumer aborts with "Cannot find preset's package"
(this outage happened 2026-07-18). Comments live here instead.
