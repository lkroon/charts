# charts

Deployment configuration for [lkroon/frameworks](https://github.com/lkroon/frameworks),
following the GitOps pattern: the `release` workflow in the frameworks repo
builds images to GHCR on every `v*` tag and commits the new `imageTag` to
`frameworks/values.yaml` here; Argo CD watches this repo and syncs the
cluster.

- `frameworks/` — Helm chart for the whole stack (Postgres, fastapi,
  pyramid, base, ingress, HPA, RBAC)
- `argocd/frameworks.yaml` — the Argo CD Application; apply once by hand

Not in this repo on purpose: the `fastapi-auth` Secret (session key + Google
OAuth credentials) is created out-of-band from the frameworks repo's
untracked `.env`. Argo CD ignores resources it does not manage.
