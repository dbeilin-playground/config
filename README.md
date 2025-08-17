# Config
Playground

## Kargo
### Create GH Secret for ArgoCD Auth

```shell
kubectl apply -f - <<EOF
apiVersion: v1
kind: Secret
metadata:
  name: github-repo-creds
  namespace: argocd
  labels:
    argocd.argoproj.io/secret-type: repo-creds
stringData:
  type: git
  url: https://github.com/dbeilin-playground
  username: dbeilin
  password: REDACTED
EOF
```

### Create Kubernetes Registry Secret

```shell
kubectl create secret docker-registry ghcr-creds \
  --docker-server=ghcr.io \
  --docker-username=dbeilin \
  --docker-password=REDACTED \
  --namespace=apps
```

### Create Kargo Secret
```shell
kubectl apply -f - <<EOF
apiVersion: v1
kind: Secret
type: Opaque
metadata:
  name: github-creds
  namespace: apps
  labels:
    kargo.akuity.io/cred-type: git
stringData:
  repoURL: https://github.com/dbeilin-playground
  repoURLIsRegex: "true"
  username: dbeilin
  password: REDACTED
EOF
```
