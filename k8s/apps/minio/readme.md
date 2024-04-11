# Minio Installation

To install Minio follow the steps below:

```bash
# In the k8s/apps/minio folder
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update
helm upgrade --install minio bitnami/minio -f values.yaml --namespace minio --create-namespace

```
