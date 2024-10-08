<p align="center" width="100%">
<img style="width:33%;" src="https://kubernetes.io/_common-resources/images/flower.svg" />
</p>

## Deploy Telegraf as a daemonset into your Kubernetes cluster
- Select the context you want to deploy the telegraf daemonset into:
  - kubectl config get-contexts
  - kubectl config use-context $context-name
- Add your Hosted Graphite API Key to the resources/config.yaml file:
  - prefix = "$API-KEY.telegraf-k8"
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
- Instantly visualize your metrics:
  - Import the 'Kubernetes Overview' dashboard into your HG account - from the HG Dashboard Library
