### Create new namespace

```
kubcetl create namespace test
```

### Get all namespaces

```
kubectl get ns 
```

### Create private key 

```
openssl genrsa -out john.key 2048
```

### Create certificate

```
openssl req -new -key john.key -out john.csr -subj "/CN=john/O=test"
```

### Get master node certificate

```
To list files

cd /etc/kubernetes/pki


Copy certificate and key to current directory

scp /etc/kubernetes/pki/ca.{crt,key} .
```

If you are using minikube

```
scp /home/dinush/.minikube/ca.{crt,key} .
```

### Sign user certificate with master node certificate

```
openssl x509 -req -in john.csr -CA ca.crt -CAkey ca.key -CAcreateserial -out john.crt -days 365
```

### Create kubeconfig file

** Create kubeconfig by user

Files need to send `ca.crt`, `john.crt` and `john.key`

1.Create `kubeconfig` file

```bash
kubectl --kubeconfig john.kubeconfig config set-cluster kubernetes --server <server_url> --certificate-authority=ca.crt --embed-certs=true
```

2.Add user to kubeconfig file

```bash
kubectl --kubeconfig john.kubeconfig config set-credentials john --client-certificate /home/dinush/Desktop/Learning/Kubernetes/RABC/john.crt --client-key /home/dinush/Desktop/Learning/Kubernetes/RABC/john.key
```

3.Create context

```bash
kubectl --kubeconfig john.kubeconfig config set-context john-kubernetes --cluster john --namespace test --user john
```

4. Copy user kubeconfig to kube home directory (optional)

```bash
cp john.kubeconfig ~/.kube/config
```

** Create kubeconfig by admin

1. copy default config file

```
cp ~/.kube/config john.kubeconfig
```

2. Replace client-certificate and client-key

```
cat john.crt | base64 -w0

cat john.key | base64 -w0 
```

### Create role


```
kubectl create role list-pods --verb=get,list --resource=pods --namespace test
```

* check create role

```
kubectl -n test get role list-pods -o yaml
```

* edit created rule

```
kubectl -n test edit list-pods
```

### Bind created role


* create user role binding

```
kubectl create rolebinding list-pods-rolebinding --role list-pods --user=john --namespace=test
```

* create group role binding

```
kubectl create rolebinding test-list-pods-rolebinding --role list-pods --group=test --namespace=test
```

* check role binding

```
kubectl -n test get rolebindings list-pods-rolebinding -o yaml
```

* delete created role binding

```
kubectl -n test delete rolebindings list-pods-rolebinding 
```

### Use created config file

```
kubectl --kubeconfig john.kubeconfig get pods
```