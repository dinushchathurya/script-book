### Create IAM OIDC provider

```
eksctl utils associate-iam-oidc-provider --region ${AWS_REGION} --cluster ${EKS_CLUSTER_NAME} --approve
```

### Create an IAM policy 

```
aws iam create-policy --policy-name AWSLoadBalancerControllerIAMPolicy --policy-document file://iam_policy.json
```

### Create a IAM role and ServiceAccount

```
eksctl create iamserviceaccount --cluster=${EKS_CLUSTER_NAME} --namespace=kube-system --name=aws-load-balancer-controller --attach-policy-arn=arn:aws:iam::${AWS_ACCOUNT_ID}:policy/AWSLoadBalancerControllerIAMPolicy --override-existing-serviceaccounts --region ${AWS_REGION} --approve
```

### Install the Target Group Binding CRDs

```
kubectl apply -k "github.com/aws/eks-charts/stable/aws-load-balancer-controller//crds?ref=master"

kubectl get crd
```

### Deploy the Helm chart

```
helm repo add eks https://aws.github.io/eks-charts
```

### Configure AWS ALB (Apllication Load Balancer) to sit infront of Ingress

```
helm upgrade --install  aws-load-balancer-controller eks/aws-load-balancer-controller -n kube-system --set clusterName=demo --set serviceAccount.create=false --set region=us-east-1 --set image.repository=602401143452.dkr.ecr.region-code.amazonaws.com/amazon/aws-load-balancer-controller --set serviceAccount.name=aws-load-balancer-controller
```

*** Warning ***

Sometime it said that `failed to download "eks/aws-load-balancer-controller"`. To avoid it use below command

```
helm upgrade --install  aws-load-balancer-controller eks/aws-load-balancer-controller -n kube-system --set clusterName=${EKS_CLUSTER_NAME} --set serviceAccount.create=false --set region=${AWS_REGION} --set image.repository=602401143452.dkr.ecr.region-code.amazonaws.com/amazon/aws-load-balancer-controller --set serviceAccount.name=aws-load-balancer-controller
```
<a href="https://docs.aws.amazon.com/eks/latest/userguide/aws-load-balancer-controller.html">Refer this link</a>

### Verify that the AWS Load Balancer controller is installed. 

```
kubectl get deployment -n kube-system aws-load-balancer-controller
```
### Deploy Sample Application

```
kubectl apply -f example-ns.yaml

kubectl apply -f example-deployment.yaml

kubectl apply -f example-service.yaml

kubectl apply -f example-ingress.yaml
```
### Get Ingress url

```
kubectl get ingress nginx-blue -n nginx-blue
```
### Troubleshooting

Refer this link <a href="https://aws.amazon.com/premiumsupport/knowledge-center/eks-load-balancers-troubleshooting/">for triubleshooting</a>




