### Install Dashboard

```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.6.1/aio/deploy/recommended.yaml
```

### Get all pods, services and deployments

```
kubectl get all -n kubernetes-dashboard
```

### Expose port

* Using port forwarding

Get actual port number

```
kubectl -n kubernetes-dashboard describe service kubernetes-dashboard | findstr TargetPort
```

Forward port

```
kubectl -n kubernetes-dashboard port-forward <kubernetes-dashboard-pod_name> 8443:8443
```

Access dashboard

```
https://localhost:8443
```

* Using NodePort

```
kubectl -n kubernetes-dashboard edit service kubernetes-dashboard
```

Change type to NodePort

```
type: NodePort
nodePort: 32323
```

Confirm changes

```
kubectl -n kubernetes-dashboard get service kubernetes-dashboard
```

Accesss dashboard

```
https://<node_ip>:32323
```

### Create Service Account

```
kubectl apply -f sa_cluster_admin.yaml
```

### Get token

Check all the service accounts

```
kubectl get sa -n kube-system
```

Get token

```
kubectl -n kube-system describe sa dashboard-admin
```

Get actual token

```
kubectl -n kube-system describe secret dashboard-admin-token-<token_id>
```