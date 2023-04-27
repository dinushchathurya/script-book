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
