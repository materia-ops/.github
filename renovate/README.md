# Org-wide Renovate policy for materia-ops

`default.json` is the shared preset every Renovate-managed repo extends
**last**, so it overrides upstream presets. (Not every repo here runs
Renovate: the standalone WoW addon repos use Dependabot, and a few repos have
no dependency bot at all.)

```json5
extends: [
  // the repo's own upstream presets first: "config:recommended", or a
  // version-pinned preset such as "github>home-operations/renovate-presets#<tag>"
  "config:recommended",
  "github>materia-ops/.github//renovate/default",
]
```

The upstream entries and their pins belong to each consuming repo — read that
repo's Renovate config for the current ones rather than copying a version
from here.

Why it exists: the org ruleset forbids direct pushes to the default branch of
every Renovate-managed repo (no bypass), so upstream `:automergeBranch`
presets would be rejected at push. This preset forces every automerge through
a PR that Renovate then auto-merges (the ruleset requires 0 approvals, so it
stays hands-off). It only sets *how* an automerge happens; whether a given
update automerges at all is decided by each repo's own `automerge` rules.

Why it is strict JSON named `default.json`, not json5: renovate resolves an
extensionless `github>owner/repo//path/default` preset by fetching
`default.json` (falling back to `renovate.json`) — a `default.json5` file is
never tried and every consumer aborts with "Cannot find preset's package"
(this outage happened 2026-07-18). Comments live here instead.
