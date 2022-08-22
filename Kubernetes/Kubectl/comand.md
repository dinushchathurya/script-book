## Deployment

### Create Deployment
    
```
kubectl create deployment <deployment-name> --image=<container-image-name>
```

### Edit Deployment
    
```
kubectl edit deployment <deployment-name> 
```

### Delete Deployment
    
```
kubectl delete deployment <deployment-name>
```

## Status

### Get Deployment Status
    
```
kubectl get deployment <deployment-name> -o yaml
```    

## Debugging

### Log to console

```
kubectl logs <pod-name>
```

### Get a terminal of running container

```
kubectl exec -it <pod-name>  -- /bin/bash
```

### Get pod details

```
kubectl describe pod <pod-name>
```

## Configuration file

### Apply a configuration file

```
kubectl apply -f <configuration-file-name>
```

### Get current context

```
kubectl config get-contexts
```

### To switch to a different context,

```
kubectl config use-context <context-name>
```
```