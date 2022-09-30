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