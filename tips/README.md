# tips and tricks

## Networking

### Filtering/whitelisting IPs

Filtering can be done at 2 points: Ingress or LB.

#### Ingress

No default implementation exists. Depending of Ingress Controller used, annotation is different.

##### _nginx-ingress_

Annotation [`nginx.ingress.kubernetes.io/whitelist-source-range`](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/#whitelist-source-range) can be used.

Example:
```yaml
kind: Ingress
metadata:
  annotations:
    nginx.ingress.kubernetes.io/whitelist-source-range: "XXX.XXX.XXX/32"
```

#### Load Balancer

When using a Service with `spec.type: LoadBalancer`, you can specify the IP ranges that are allowed to access the load balancer by using `spec.loadBalancerSourceRanges`.

More information: https://kubernetes.io/docs/tasks/access-application-cluster/configure-cloud-provider-firewall/#restrict-access-for-loadbalancer-service

Example:
```yaml
apiVersion: v1
kind: Service
spec:
  type: LoadBalancer
  loadBalancerSourceRanges:
  - XXX.XXX.XXX.XXXX/32
```