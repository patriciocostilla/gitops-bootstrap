# GitOps Bootstrap

# Installation Steps

## Install ArgoCD

[source](https://argo-cd.readthedocs.io/en/stable/getting_started/)

```sh
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

## Add this repo to ArgoCD

```sh
argocd repo add git@github.com:patriciocostilla/gitops-bootstrap.git --ssh-private-key-path ~/.ssh/id_rsa_argo
```

## Install App of Apps

```sh
kubectl apply -f apps.argocd.yaml
```