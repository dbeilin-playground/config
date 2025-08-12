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

Also, need to give SA permissions to pull from GH:
```
kubectl create secret docker-registry ghcr-creds \
  --docker-server=ghcr.io \
  --docker-username=<your-github-username> \
  --docker-password=<PAT with read:packages> \
  -n nginx-stg

kubectl create secret docker-registry ghcr-creds \
  --docker-server=ghcr.io \
  --docker-username=<your-github-username> \
  --docker-password=<PAT with read:packages> \
  -n nginx-cand
```
