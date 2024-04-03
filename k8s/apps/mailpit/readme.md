# Mailpit Installation

To install mailpit follow the steps below:

```bash
# In the k8s/apps/mailpit folder
helm repo add jouve https://jouve.github.io/charts/
helm install mailpit jouve/mailpit --namespace mailpit --create-namespace
```

After that, apply the manifest configuration:

```bash
# In the k8s/apps/mailpit folder
kubectl apply -f manifest.yaml -n mailpit
```