### Install using Helm Chart

```
helm repo add bitnami https://charts.bitnami.com/bitnami

helm install keycloak bitnami/keycloak
```

### Patch serivce to use ClusterIP

```
kubectl patch svc keycloak -p '{"spec": {"type": "ClusterIP"}}'
```

### Get admin password

```bash
kubectl get secret --namespace default keycloak -o jsonpath="{.data.admin-password}" | base64 --decode
```