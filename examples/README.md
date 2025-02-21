Create cluster (enable pod static IP) https://console.cloud.tencent.com/tke2/cluster/create?rid=1

Create tag and bind resource https://console.cloud.tencent.com/tag/taglist

Get AK/SK https://console.cloud.tencent.com/cam/capi


Install karpenter:

```sh
kubectl create namespace karpenter
kubectl -n karpenter create secret generic apisecret --from-file=./secretID --from-file=./secretKey

helm upgrade --install karpenter  https://github.com/tkestack/karpenter-provider-tke/raw/refs/heads/main/charts/karpenter-0.1.8-beta29.tgz --namespace "karpenter" --create-namespace \
  --set "settings.clusterID=cls-xxx" \
  --set "settings.region=ap-xxx" \
  --set controller.resources.requests.cpu=0.1 \
  --set controller.resources.requests.memory=100Mi \
  --set controller.resources.limits.cpu=1 \
  --set controller.resources.limits.memory=1Gi \
  --set replicas=1 \
  --wait
```