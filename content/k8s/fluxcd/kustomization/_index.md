---
_db_id: 1041
content_type: project
flavours:
- none
from_repo: k8s/manual-app-deployment/project-overview
prerequisites:
  hard:
  - k8s/manual-app-deployment/project-overview
  soft:
  - k8s/fluxcd/bootstrap-flux
ready: true
submission_type: continue_repo
tags:
- kubernetes
- fluxcd
title: Kustomization
---

## Kustomization


Kustomize, a configuration management tool native to Kubernetes, streamlines the customization and management of Kubernetes manifests. Its overlays prove invaluable when configuring multiple clusters using the same kustomization files. With Kustomize, users can efficiently tailor Kubernetes configurations without directly altering original YAML files. This approach enhances modularity and eases maintenance by separating desired changes into overlay files, making it ideal for consistent deployment across diverse clusters. In essence, Kustomize is a powerful tool that significantly improves the flexibility and scalability of Kubernetes configurations, facilitating smoother operations in multi-cluster environments.

```
|-- infrastructure
|   |-- my-cluster
|   |   |-- kustomization.yaml
|-- infrastructure
|   |-- kustomization.yaml
```


```
kubectl -n flux-system get kustomization
kubectl -n flux-system describe kustomization
```

Now we need to add a new kustomization for our base infrastructure

In the infrastructure directory create the following files

```
# clusters/my-cluster/infrastructure.yaml
---
apiVersion: kustomize.toolkit.fluxcd.io/v1
kind: Kustomization
metadata:
  name: infrastructure
  namespace: flux-system
spec:
  interval: 30s
  sourceRef:
    kind: GitRepository
    name: flux-system
  path: ./infrastructure
  prune: true
```

You can use Helm and Kustomize together by embedding Kustomize overlays within a Helm chart. This enables you to benefit from Helm's packaging and release management alongside Kustomize's declarative configuration customization for Kubernetes applications. The combination allows for a more modular and adaptable approach to managing Kubernetes configurations.

You'll notice kustomize tells flux to go and look inside the ./infrastructure folder for further instructions and then it will again look for the kustomization file and follow instructions

Commit to github you can push straight to main branch

Here are some useful commands to help with debugging.

`kubectl -n flux-system describe kustomiztion`
`kubectl -n flux-system describe helmrepository`
`kubectl -n flux-system describe helmchart`
`kubectl -n flux-system describe helmrelease`

```
kubectl -n flux-system get kustomization --watch
```

You'll need to wait a minute or so and you'll notice the new kustomization rolling out, if you run it with `kubectl -n flux-system describe kustomization` it tells you that it's missing a file let's add it now

```
infrastructure   60s   False     kustomize build failed: kustomization.yaml is empty 
```

```
# infrastructure/kustomization.yaml
---
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization
resources:
```

Now it says the file is empty but let's add some sources in the next section