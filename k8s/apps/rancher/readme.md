# Rancher Installation

To install Rancher, first you need to install Cert-Manager. Please read the [Cert-Manager Installation](../certmanager/readme.md) guide.

Then, create the Certificate for Rancher using the following command:

```bash
# In the k8s/apps/rancher folder
kubectl apply -f manifest.yaml
```

After that, you can install Rancher using the following Helm command:

```bash
# In the k8s/apps/rancher folder
helm repo add rancher-latest https://releases.rancher.com/server-charts/latest
helm install rancher rancher-latest/rancher --namespace cattle-system --create-namespace -f values.yaml
```
