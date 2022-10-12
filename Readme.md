# Argo-cd Bootstrap 

## Prerequisite

You need access to k8s cluster or create a new one using i.e. https://microk8s.io/

```shell
brew install ubuntu/microk8s/microk8s
microk8s start
microk8s kubectl get nodes
```

**Note:** Easiest way to access microk8s cluster is to prefix any `kubectl` command with `microk8s`, 
ie. `microk8s kubectl get pod` 

## Installation

- install argocd 
```shell
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

- fetch argocd ui password
```shell
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

- forward argocd ui

```shell
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

Visit http://localhost:8080 username: `admin` password fetched in previous step


Bootstrap argocd applications
```shell
kubectl apply -f bootstrap.yaml
```


