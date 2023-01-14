### Create Namespace

```
kubectl create ns argocd
```

### Install ArgoCD

```
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

### Get all ArgoCD Services, Pods, Deployments, etc.

```
kubectl get all -n argocd
```

### Change ArgoCD Service Type to NodePort

```
kubectl edit svc argocd-server -n argocd

or

kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "NodePort"}}'
```

### Get default password for ArgoCD

```
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

### Install ArgoCD CLI

```
VERSION=v2.5.5; curl -sL -o argocd https://github.com/argoproj/argo-cd/releases/download/$VERSION/argocd-linux-amd64
chmod +x argocd
sudo mv argocd /usr/local/bin/argocd
```

Check latest release from<a href="https://github.com/argoproj/argo-cd/releases"> here</a>