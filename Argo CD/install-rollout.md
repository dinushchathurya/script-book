### Create Namespace

```bash
kubectl create namespace argo-rollouts
```

### Install Argo Rollouts

```bash
kubectl apply -n argo-rollouts -f https://github.com/argoproj/argo-rollouts/releases/latest/download/install.yaml
```

### Argo-rollouts Plugin Installation

```bash
curl -LO https://github.com/argoproj/argo-rollouts/releases/latest/download/kubectl-argo-rollouts-linux-amd64

chmod +x ./kubectl-argo-rollouts-linux-amd64

sudo mv ./kubectl-argo-rollouts-linux-amd64 /usr/local/bin/kubectl-argo-rollouts

kubectl argo rollouts version
```

### Get Argo Rollout Dashboard

```bash
kubectl argo rollouts dashboard
```