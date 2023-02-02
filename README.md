# GitOps Bootstrap

# Installation Steps

## Install ArgoCD

[source](https://argo-cd.readthedocs.io/en/stable/getting_started/)

```sh
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

Or you could do a `make up`.

## Add this repo to ArgoCD

```sh
argocd repo add git@github.com:patriciocostilla/gitops-bootstrap.git --ssh-private-key-path /path/to/ssh-private-key # Ex: ~/.ssh/id_rsa_argo
```

## Install App of Apps

```sh
kubectl apply -f apps.argocd.yaml
```

## Get ArgoCD initial password

```sh
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
# Ex: 16CHf34RixP5B3ME
```
