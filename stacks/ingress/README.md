# Ingress Stack

This stack allows you to deploy the following components:

* NGINX ingress controller _([here](https://github.com/kubernetes/ingress-nginx))_
* External-DNS _([here](https://github.com/kubernetes-incubator/external-dns))_
* Cert-manager _([here](https://github.com/jetstack/cert-manager))_

## Usage

Once you have fill all the prerequisites, you can now deploy this stack on your cluster. To do it, run the following command:

```bash
export DNS_RESOURCE_GROUP=<RESOURCE_GROUP_DNS_ZONE> _(required)_
export INGRESS_REPLICAS=<NUMBER_POD_FOR_INGRESS> _(default: 1)_
export K8S_ISSUERS_EMAIL=<TEAM_EMAIL> _(email used by lets encrypt to send notification.)_

helmfile apply
```