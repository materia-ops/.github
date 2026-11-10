# Contributing

Thanks for taking the time. The short version:

- **Small, focused PRs.** One concern per pull request.
- **Conventional Commits.** Title commits and PRs as
  `type(scope): summary` (e.g. `fix(renovate): ...`).
- **Everything goes through a PR.** Default branches only move through
  pull requests — an org ruleset requires a PR into `main` across the
  org's repositories and blocks force-pushes and branch deletion, with
  no bypass. Our own automation opens PRs like everyone else. (A small
  number of internal repositories also accept direct pushes;
  force-pushes and deletion are blocked there too.)
- **PRs are squash-merged.** The merge button is squash-only (one
  internal repository also keeps merge commits), and the PR title
  becomes the squash commit on `main` — so the title itself must be a
  valid Conventional Commit; where a repository versions its releases
  from commit types, that title decides the version.
- **Maintainer merges.** Contributor PRs are merged by the maintainer;
  Renovate and release automation merge some of their own PRs once
  checks pass.
- **Dependency bumps are handled by bots.** Renovate (or, on the
  standalone WoW addon repos, Dependabot) keeps dependencies updated —
  please don't open manual version-bump PRs.

Security issues: don't open an issue — see [SECURITY.md](SECURITY.md).
