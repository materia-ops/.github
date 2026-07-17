# materia-ops

Materia Ops builds and runs **Materia**: a GitOps-managed Kubernetes cluster and
the World of Warcraft 3.3.5a services and tooling that run on it. Every public
repository here is either the source of something we operate or the release
mirror an in-game updater pulls from.

## What you can verify about the code here

We would rather you check than trust us. Each statement below is enforced by an
org policy or a mechanism you can inspect — not a convention we ask people to
remember.

**Workflow actions are pinned to immutable references.** Every `uses:` in every
workflow resolves to a full-length commit SHA — or, for container actions, an
image digest — never a moving tag like `@v4`. GitHub's org-wide SHA-pinning
policy enforces this, so it cannot quietly drift.

**Default branches only move through pull requests.** Force-pushes and branch
deletions are blocked across the organization, and nothing writes to a default
branch directly — our own automation opens a pull request like everyone else.
This is an organization ruleset with no bypass, so it holds even for an owner's
token.

**Secrets never touch git.** Application and infrastructure secrets live in
1Password and reach the cluster through External Secrets. CI reads a small,
dedicated vault through a service account scoped to it alone, so a workflow
cannot reach cluster credentials. A secret is scoped to the one repository that
needs it; an organization-wide secret would require a written reason.

**End-user releases are signed.** Every release publishes a `SHA256SUMS` over its
assets and a `SHA256SUMS.sig` — an RSA-SHA256 signature over that file. The
verifying public key is committed next to the source and pinned inside the
shipped updater, which checks the signature before installing anything, so a
compromised mirror cannot hand a client a tampered build. You can check any
release yourself:

```sh
sha256sum -c SHA256SUMS
openssl dgst -sha256 -verify release-key.pub -signature SHA256SUMS.sig SHA256SUMS
```

**Dependencies are updated by bots, deliberately.** Most repositories use
Renovate; the standalone WoW addon repositories use Dependabot. Never both on the
same repository.

## Provenance and reporting

Releases, images, and updater feeds are published only from repositories in this
organization. Anything sourced elsewhere, however it is named, is not ours.

Please report security issues privately through GitHub's private vulnerability
reporting on the affected repository, rather than opening a public issue.
