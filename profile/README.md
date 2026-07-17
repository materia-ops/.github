# materia-ops

Materia Ops builds and runs the Materia realm: a GitOps-managed Kubernetes cluster,
the services on it, and the World of Warcraft 3.3.5a addons and tooling that ship to
players. Public repositories here are either the source of something we run, or the
release mirror an in-game updater pulls from.

## What you can verify about the code here

**Workflow actions are pinned to immutable references.** Every `uses:` in every
workflow resolves to a full-length commit SHA (or, for container actions, an image
digest) — never a mutable tag like `@v4`. This is enforced by GitHub's org-wide SHA
pinning policy, so it cannot quietly drift; it is not a convention we ask people to
remember.

**Releases aimed at end users are signed.** Every release publishes a `SHA256SUMS`
covering the other assets, and a `SHA256SUMS.sig` — an RSA-SHA256 signature over that
file. The verifying public key is committed next to the source and pinned inside the
shipped updater, which checks the signature before installing anything. A compromised
mirror therefore cannot feed a tampered build to a client. You can check any release
yourself:

```sh
sha256sum -c SHA256SUMS
openssl dgst -sha256 -verify release-key.pub -signature SHA256SUMS.sig SHA256SUMS
```

**Default branches take pull requests only.** Force pushes and branch deletion are
blocked across the org, and nothing pushes directly to a default branch — including
our own automation, which opens a pull request like anyone else.

**Secrets are never in git.** Application and infrastructure secrets live in 1Password
and reach the cluster through External Secrets. CI reads a small, dedicated vault
through a service account scoped to it alone, so a workflow cannot reach cluster
credentials. Secrets are scoped to the repository that needs them; an organization-wide
secret requires a written reason, and today the only candidate is the credential that
bootstraps 1Password access itself — the one secret that cannot live in 1Password.

**Dependencies are updated by bots, deliberately.** Most repositories use Renovate;
the standalone WoW addon repositories use Dependabot. Never both on the same
repository.

## Provenance

`materia.wtf` is a verified domain for this organization. Releases, images, or updater
feeds sourced from anywhere else are not ours, regardless of naming.

Security issues can be reported privately through GitHub's private vulnerability
reporting, which is enabled on our repositories.
