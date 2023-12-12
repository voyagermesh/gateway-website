---
title: Configure Ingress Loadbalancer IP
menu:
  docs_v0.6.1:
    identifier: loadbalancer-ip-configuration
    name: Loadbalancer IP
    parent: config-ingress
    weight: 10
product_name: voyager
menu_name: docs_v0.6.1
section_menu_id: guides
info:
  version: v0.6.1
---

> New to Voyager? Please start [here](/docs/v0.6.1/concepts/overview).

# LoadBalancer IP

For `LoadBalancer` type ingresses, you can specify `LoadBalancerIP` of HAProxy services using `ingress.appscode.com/load-balancer-ip` annotation.

Note that, this feature is supported for cloud providers GCE, GKE, Azure, ACS and Openstack.

## Ingress Example

```yaml
apiVersion: voyager.appscode.com/v1
kind: Ingress
metadata:
  name: test-ingress
  namespace: default
  annotations:
    ingress.appscode.com/load-balancer-ip: "78.11.24.19"
spec:
  rules:
  - host: voyager.appscode.test
    http:
      paths:
      - path: /foo
        backend:
          service:
            name: test-server
            port:
              number: 80
```