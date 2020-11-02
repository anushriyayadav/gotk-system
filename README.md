# gotk-system
Playing with flux2/gotk

## Installation

https://toolkit.fluxcd.io/guides/installation/#generic-git-server

```
gotk check
gotk install
kubectl get pods --namespace gotk-system
gotk check

# Export the installation yamls
gotk install -export > gotk-components.yaml
```

## Configuration

```
gotk create source git gotk-system \
  --url=https://github.com/sysadmin4j/gotk-system.git \
  --branch=main \
  --interval=1m

# Export the source configuration yaml
gotk export source git gotk-system > toolkit-source.yaml
```

```
gotk create kustomization gotk-system \
  --source=gotk-system \
  --path="./local-k8s-cluster" \
  --prune=true \
  --interval=10m

# Export the kustomization configuration yaml
gotk export kustomization gotk-system > toolkit-kustomization.yaml
```

```
gotk get sources git
gotk get sources helm
gotk reconcile source git gotk-system
```

```
gotk get kustomizations gotk-system
gotk reconcile kustomization gotk-system
gotk reconcile kustomization gotk-system --with-source
gotk reconcile kustomization gotk-apps --with-source --verbose

```

## Issues

### Reconcile hang/timeout
https://github.com/sysadmin4j/gotk-system/commit/369c403aca1e4af23f65e1e518e41ca577edd34d

### Rbac not effective
https://github.com/docker/for-mac/issues/3694


