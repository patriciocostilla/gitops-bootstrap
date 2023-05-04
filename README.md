# GitOps Bootstrap

# Installation Steps

## Install ArgoCD

[source](https://argo-cd.readthedocs.io/en/stable/getting_started/)

```sh
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```


Or you could do a `make up`.

## Install ArgoCD CLI

```sh
# 1 Download argocd binaries
curl -sSL -o argocd-linux-amd64 https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64
```

```sh
# 2 Install binaries into bin folder
sudo install -m 555 argocd-linux-amd64 /usr/local/bin/argocd
```

```sh
# 3 Remove binaries from download dir
rm argocd-linux-amd64
```

## Port-forward to ArgoCD Server
```sh
# On a separate terminal
kubectl port-forward service/argocd-server 8080:80 -n argocd
```

## Get ArgoCD initial password

```sh
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
# Ex: 16CHf34RixP5B3ME
```

## Login into ArgoCD and add this repo to ArgoCD

```sh
# Login via CLI
argocd login localhost:8080
# username: admin
# password: <the one from previous step>
```

```sh
# Add the gitops repo, you'll need to pass a ssh key with access to this
argocd repo add git@github.com:patriciocostilla/gitops-bootstrap.git --ssh-private-key-path </path/to/ssh-private-key> # Ex: ~/.ssh/id_rsa_argo
```

## Install App of Apps

```sh
kubectl apply -f apps.app.yaml
```
