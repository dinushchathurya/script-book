### Create EKS Cluster

```bash
eksctl create cluster -f cluster.yaml
```

* If you want to avoid manually Associate CloudWatch Policy to EKS Worker Nodes Role which is our second step, plase use below config file.

```bash
eksctl create cluster -f cluster-with-policy.yaml
```

### Apply IAM Policy for Fluentd

Go to your Node Group Role and attach the following policy:

```bash
AmazonEKSWorkerNodePolicy
```

### Deploy CloudWatch Agent and Fluentd as DaemonSets

```bash
curl -s https://raw.githubusercontent.com/aws-samples/amazon-cloudwatch-container-insights/latest/k8s-deployment-manifest-templates/deployment-mode/daemonset/container-insights-monitoring/quickstart/cwagent-fluentd-quickstart.yaml | sed "s/{{cluster_name}}/<YOUR_CLUSTER_NAME>/;s/{{region_name}}/YOUR-AWS_REGION>/" | kubectl apply -f -
```

### Check DaemonSet status

```bash
kubectl get ds -n amazon-cloudwatch -o wide
```

###  Deploy sample application

Deploy application that you want to deploy to EKS cluster.

### Check CloudWatch Logs

CloudWatch -> Insights -> Container Insights 


### Clean up Container Insights

```bash
curl https://raw.githubusercontent.com/aws-samples/amazon-cloudwatch-container-insights/latest/k8s-deployment-manifest-templates/deployment-mode/daemonset/container-insights-monitoring/quickstart/cwagent-fluentd-quickstart.yaml | sed "s/{{cluster_name}}/cluster-name/;s/{{region_name}}/cluster-region/" | kubectl delete -f -
```


