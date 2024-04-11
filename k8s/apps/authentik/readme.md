# Authentik Installation

To install Authentik follow the steps below:

```bash
# In the k8s/apps/authentik folder
helm repo add authentik https://charts.goauthentik.io
helm repo update
helm upgrade --install authentik authentik/authentik -f values.yaml --namespace authentik --create-namespace

```

After that, apply the manifest configuration:

```bash
# In the k8s/apps/authentik folder
kubectl apply -f manifest.yaml -n authentik
```