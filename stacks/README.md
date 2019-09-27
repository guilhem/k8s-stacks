# Stacks

## Description

## List

- [ingress](./ingress/)
- [cluster-autoscaler](./cluster-autoscaler/)
- [kured](./kured/)

## Requirements

To be able to deploy this stack you will need the following dependencies:

### kubernetes cluster

Your `kubectl` should works.

### [`helm`](https://github.com/helm/helm)

```bash
kubectl -n kube-system create serviceaccount tiller

kubectl create clusterrolebinding tiller --clusterrole=cluster-admin --serviceaccount=kube-system:tiller

helm init --service-account tiller
```

### [`helmfile`](https://github.com/roboll/helmfile)


### [`helm-diff`](https://github.com/databus23/helm-diff)
