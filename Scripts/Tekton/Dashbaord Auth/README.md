### Create Secret 

```bash
kubectl create secret generic oauth2-proxy-creds-github --from-literal=client-id=<github-client-id> --from-literal=client-secret=<github-client-secret>  --from-literal=cookie-secret=<cookie-secret> -n oauth-proxy
```
*** You can generate cookie-secret by following instructions in [this](https://oauth2-proxy.github.io/oauth2-proxy/docs/configuration/overview/#cookie-secret) link.

### Install Helm Chart

```bash
helm repo add oauth2-proxy https://oauth2-proxy.github.io/manifests

helm repo update

helm install oauth2-proxy oauth2-proxy/oauth2-proxy --namespace oauth-proxy --values oauth-proxy-values.yaml
```
*** Please make sure to replace values in `oauth-proxy-values.yaml` file with your own values.

### Change the Ingress of Tekton Dashboard to use the oauth2-proxy

At below line in `<your-tekton-dashbaord-ingress>.yaml` file:

```yaml
annotations:
    nginx.ingress.kubernetes.io/auth-url: https://<your-oauth2-proxy-server>/oauth2/auth 
    nginx.ingress.kubernetes.io/auth-signin: https://<your-oauth2-proxy-server>/oauth2/start
```

And at below line in `<your-tekton-dashbaord-ingress>.yaml` file:

```yaml
pathType: ImplementationSpecific
```

Here is an example of `<your-tekton-dashbaord-ingress>.yaml` file:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: tekton-dashboard-nginx-ingress
  namespace: tekton-pipelines
  annotations:
    kubernetes.io/ingress.class: nginx
    cert-manager.io/cluster-issuer: letsencrypt-prod
    nginx.ingress.kubernetes.io/auth-url: https://<your-proxy-domain>/oauth2/auth 
    nginx.ingress.kubernetes.io/auth-signin: https://<your-proxy-domain>/oauth2/start
spec:
  rules:
  - host: <tekton-dashboard-domain>
    http:
      paths:
        - path: /
          pathType: ImplementationSpecific
          backend:
            service:
              name: tekton-dashboard
              port:
                number: 9097
  tls:
    - hosts:
        - <tekton-dashboard-domain>
      secretName: tekton-dashboard-tls



