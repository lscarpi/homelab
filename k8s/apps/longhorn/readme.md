# Longhorn Installation

Before doing anything, make sure all clusters comply with the installation requirements found [here](https://longhorn.io/docs/1.5.4/deploy/install/#installation-requirements).

Proceed to install Longhorn from within the Rancher UI.

After that, apply the manifest configuration:

```bash
# In the k8s/apps/longhorn folder
kubectl apply -f manifest.yaml -n longhorn-system
```
