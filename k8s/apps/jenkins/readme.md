# Jenkins Installation

Firstly, install Jenkins using this guide: [Jenkins Installation](https://github.com/jenkinsci/helm-charts/blob/main/charts/jenkins/README.md#configuration).

Then apply the manifest file into the jenkins namespace:

```bash
# In the k8s/apps/jenkins folder
kubectl apply -f manifest.yaml -n jenkins
```