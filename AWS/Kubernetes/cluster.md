### Create Cluster

Managed Nodes

```
eksctl create cluster --name <cluster-name> --region <region-code>
```

AWS Fargate

```
eksctl create cluster --name <cluster-name> --region <region-code> --fargate
```

### Create Cluster with Nodes

```
eksctl create cluster --name <cluster-name> --region <region-code> --nodegroup-name <node-name> --node-type t3.small --managed --nodes 2
```

### List all cluster related to particular region

```
aws eks list-clusters --region=<region_code>
```

### Delete Cluster

```
eksctl delete cluster --name <cluster-name> --region <region-code>
```
