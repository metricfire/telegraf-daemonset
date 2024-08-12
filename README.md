<h2 style="text-align:center;">
<img style="width:300px;margin:.5rem" src="https://kubernetes.io/_common-resources/images/flower.svg" /> --->
<img style="width:50px;margin:.5rem;border-radius:50%" src="https://cdn.buttercms.com/bCPe2yZrQrCP0n42ordd"/>
</h2>

## Deply telegraf as a daemonset into your kubernetes cluster
- Select the context you want to deploy the telegraf daemonset into:
  - kubectl config get-contexts
  - kubectl config use-context $context-name
- Add your Hosted Graphite API Key to the telegraf/config.yaml file:
  - prefix = "$YOUR-HG-API-KEY.telegraf"
- Deploy the kustomization.yaml manifest:
  - kubectl apply -k . --dry-run=client
  - kubectl apply -k .
- Expected output:
```
namespace/monitoring created
serviceaccount/telegraf-sa created
clusterrole.rbac.authorization.k8s.io/telegraf-cluster-role created
clusterrolebinding.rbac.authorization.k8s.io/telegraf-sa-binding created
configmap/telegraf-config created
daemonset.apps/telegraf created
```

- Confirm the daemonset is running in your context, with the name *telegraf* and the namespace *monitoring*:
  - kubectl get daemonsets --all-namespaces