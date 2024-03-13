# Certmanager Installation

Please follow the instructions on the [official documentation](https://cert-manager.io/docs/installation/helm/) to install cert-manager using Helm.

> Don't forget to include the installCRDs flag to true.

Example:

```bash
helm install cert-manager jetstack/cert-manager --namespace cert-manager --create-namespace --set installCRDs=true
```

After that, apply the api key secret and the cluster issuer:

```bash
kubectl apply -f k8s/apps/certmanager/cloudflare-api-key-secret.yaml
kubectl apply -f k8s/apps/certmanager/cluster-issuer.yaml
```
