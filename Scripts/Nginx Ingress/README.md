### Install Nginx Ingress Controller

```
helm repo add nginx-stable https://helm.nginx.com/stable

helm repo update

helm upgrade --install nginx-ingress ingress-nginx --repo https://kubernetes.github.io/ingress-nginx --namespace nginx-ingress --create-namespace
```

### Install Issuer 

In here we use [Let's Encrypt](https://letsencrypt.org/) to generate SSL certificate. First we need to install [nginx ingress controller](https://kubernetes.github.io/ingress-nginx/deploy/) and then we need to install [cert-manager](https://cert-manager.io/docs/installation/kubernetes/).

```
kubectl create -f cluster-issuer/staging_issuer.yaml

kubectl create -f cluster-issuer/prod_issuer.yaml
```

### Deploy Sample App

```
kubectl create -f 2048/deployment.yaml

kubectl create -f 2048/service.yaml

kubectl create -f 2048/ingress.yaml
```
