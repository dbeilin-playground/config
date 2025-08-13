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
  username: your-github-username
  password: ghp_your_token_here
EOF
```

### Create Kargo Secret
```shell
kubectl apply -f - <<EOF
apiVersion: v1
kind: Secret
type: Opaque
metadata:
  name: github-creds
  namespace: apps  # This should be in your Kargo project namespace
  labels:
    kargo.akuity.io/cred-type: git
stringData:
  repoURL: https://github.com/dbeilin-playground
  username: your-github-username
  password: ghp_your_personal_access_token_here
EOF
```
