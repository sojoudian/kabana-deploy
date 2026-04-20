# kabana-deploy

GitOps deployment manifests for [kabana](https://github.com/mii1na/kabana).

Argo CD on the target cluster reconciles manifests from this repo.
Argo CD Image Updater watches `ghcr.io/mii1na/kabana` and commits tag bumps back here.

## Flow
```
git push mii1na/kabana:master
  -> GH Actions builds ghcr.io/mii1na/kabana:<sha>
    -> Image Updater detects new tag
      -> commits updated tag to this repo
        -> Argo CD reconciles
          -> Knative rolls a new Revision
```

## Layout
- `kabana/kabana-knative.yaml` — Knative Service + DomainMapping for `kabana.tunnels.solutions`.
