### Create IAM Policy

```bash
aws iam create-policy --policy-name AllowExternalDNSUpdates --policy-document file://external-dns-policy.json
```
### See all custom created plolices

```bash
aws iam list-policies --scope Local
```

### Create IAM Service Account

Now we need to create a service account for the external-dns to use. This service account will be assigned the IAM policy we created in the previous step.

```bash
eksctl create iamserviceaccount --name SERVICE_ACCOUNT_NAME --namespace NAMESPACE --cluster CLUSTER_NAME --attach-policy-arn IAM_POLICY_ARN --approve --override-existing-serviceaccounts
```

**Note:** Replace the following values in the above command:

- SERVICE_ACCOUNT_NAME: The name of the service account you want to create. For example, external-dns.
- NAMESPACE: The namespace you want to create the service account in. For example, default.
- CLUSTER_NAME: The name of the EKS cluster you want to create the service account in.
- IAM_POLICY_ARN: The ARN of the IAM policy you created in the previous step. For example,arn:aws:iam::<account-id>:policy/AllowExternalDNSUpdates.

To check if the service account was created successfully, run the following command:

```bash
kubectl get sa -n NAMESPACE
```

### Create ClusterRole

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: external-dns
rules:
- apiGroups: [""]
  resources: ["services","endpoints","pods"]
  verbs: ["get","watch","list"]
- apiGroups: ["extensions","networking.k8s.io"]
  resources: ["ingresses"]
  verbs: ["get","watch","list"]
- apiGroups: [""]
  resources: ["nodes"]
  verbs: ["list","watch"]
```

To apply this ClusterRole, run the following command:

```bash
kubectl apply -f external-dns-clusterrole.yaml
```

### Create ClusterRoleBinding

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: external-dns-viewer
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: external-dns
subjects:
- kind: ServiceAccount
  name: external-dns ### Service Account Name which we created in previous step
  namespace: default ### Namespace where we created the service account
```

To apply this ClusterRoleBinding, run the following command:

```bash
kubectl apply -f external-dns-clusterrolebinding.yaml
```

### Create ExternalDNS Deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: external-dns
spec:
  strategy:
    type: Recreate
  selector:
    matchLabels:
      app: external-dns
  template:
    metadata:
      labels:
        app: external-dns
    spec:
      serviceAccountName: external-dns
      containers:
      - name: external-dns
        image: registry.k8s.io/external-dns/external-dns:v0.13.4 ### You can find the latest version of the image here: https://github.com/kubernetes-sigs/external-dns/releases
        args:
        - --source=service
        - --source=ingress
        - --domain-filter=YOUR_DOMIAN_NAME # will make ExternalDNS see only the hosted zones matching provided domain, omit to process all available hosted zones
        - --provider=aws
        - --policy=upsert-only # would prevent ExternalDNS from deleting any records, omit to enable full synchronization
        - --aws-zone-type=public # only look at public hosted zones (valid values are public, private or no value for both)
        - --registry=txt
        - --txt-owner-id=HOSTED_ZONE_ID
      securityContext:
        fsGroup: 65534 # For ExternalDNS to be able to read Kubernetes and AWS token files
```

You can find more configuration options for the ExternalDNS deployment here: https://github.com/kubernetes-sigs/external-dns

To apply this deployment, run the following command:

```bash
kubectl apply -f external-dns-deployment.yaml
```

### Deploy Sample Application

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx
  annotations:
    external-dns.alpha.kubernetes.io/hostname: nginx.example.com ### This is the domain name which we want to point to the nginx service
spec:
  ports:
    - port: 80
      targetPort: 80
      protocol: TCP
  type: LoadBalancer
  selector:
    app: nginx

---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx
spec:
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - image: nginx
          name: nginx
          ports:
            - containerPort: 80
              name: http
```