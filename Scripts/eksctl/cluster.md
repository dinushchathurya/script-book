### Create Cluster

```
eksctl create cluster --name=<cluster-name> --region=us-east-1 --zones=us-east-1a,us-east-1b --without-nodegroup 
```

### Get List of clusters

```
eksctl get clusters 
```

### Create & Associate IAM OIDC Provider for our EKS Cluster

```
eksctl utils associate-iam-oidc-provider --region region-code --cluster <cluter-name> --approve
```

### Create Node Group with additional Add-Ons in Public Subnets

```
eksctl create nodegroup --cluster=demo --region=us-east-1 --name=demo-ng --node-type=t3.medium --nodes=2 --nodes-min=1 --nodes-max=3 --managed --node-volume-size=20 --ssh-access --ssh-public-key=demo --asg-access --external-dns-access --full-ecr-access --appmesh-access --alb-ingress-access 
```

### List Node Groups in a Cluster

```
eksctl get nodegroup --cluster=<cluster-name> 
```

### List Nodes in current cluster

```
kubectl get nodes -o wide 
```

### Get current context

```
kubectl config view --minify 
```

