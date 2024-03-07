# Redis Configuration

Install redis normally via Helm:

```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install redis bitnami/redis
```

After that, apply the ingress configuration from the file in this directory. It will expose the redis service.