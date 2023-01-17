### Create EKS Cluster

```bash
eksctl create cluster -f cluster.yaml
```

### Create OIDC Provider

```bash
eksctl utils associate-iam-oidc-provider --cluster <cluser-name> --approve
```

### Create Service Account for Cloudwatch Logs

```bash
eksctl create iamserviceaccount --name fluentd --namespace kube-system --cluster <cluster-name> --attach-policy-arn arn:aws:iam::aws:policy/CloudWatchAgentServerPolicy --approve --override-existing-serviceaccounts
```

### Create Cluster Role for Cloudwatch Logs

```bash
kubectl apply -f  kube-manifest/cluster-role.yaml
```

### Create Cluster Role Binding for Cloudwatch Logs

```bash
kubectl apply -f  kube-manifest/cluster-role-binding.yaml
```

### Create ConfigMap for Fluentd

```bash
kubectl apply -f  kube-manifest/configmap.yaml
```

### Create DaemonSet for Fluentd

```bash
kubectl apply -f  kube-manifest/daemonset.yaml
```

Warning: Make sure to change the region & cluster name in the daemonset.yaml file.

### Check DaemonSet status

```bash
kubectl get ds -n kube-system
```

### Apply sample application

Deploy application that you want to deploy to EKS cluster.

### Apply IAM Policy for Fluentd

Go to your Node Group Role and attach the following policy:

```bash
AmazonEKSWorkerNodePolicy
```

