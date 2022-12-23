### Create New User

```bash
kubectl edit  cm arogocd-cm -n argocd

# Add username
data:
  accounts.<username>: apiKey, login

# Example 
data:
  accounts.john: apiKey, login
```

### Set Password for newly created users

```
argocd account update-password --account <username>

# Example
argocd account update-password --account john
```

### Create Policies for users

```bash
kubectl edit cm argocd-rbac-cm -n argocd

data:
  policy.csv: |
    p, role: developer, applications, get, <project>/*, allow
    g, mark, role:developer

data:
  policy.csv: |
    p, role: developer, applications, get, *, allow
    g, mark, role:developer
```