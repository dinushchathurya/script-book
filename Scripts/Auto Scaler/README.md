### Create Deployment

```bash
kubectl create deployment autoscaler-demo --image=nginx
```

### Scale Deployment

```bash
kubectl scale deployment autoscaler-demo --replicas=100
```

### To check the progress of the pod’s deployment

```bash
kubectl get deployment autoscaler-demo --watch
```

### Evaluate the nodes number getting increased

```bash
kubectl get nodes
```