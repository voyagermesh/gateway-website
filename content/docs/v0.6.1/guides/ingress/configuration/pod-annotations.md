---
title: Configure Ingress Pod Annotations
menu:
  docs_v0.6.1:
    identifier: pod-annotations-configuration
    name: Pod Annotations
    parent: config-ingress
    weight: 10
product_name: voyager
menu_name: docs_v0.6.1
section_menu_id: guides
info:
  version: v0.6.1
---

> New to Voyager? Please start [here](/docs/v0.6.1/concepts/overview).

# Pod Annotations

You can specify annotations applied to HAProxy pods through ingress annotation `ingress.appscode.com/annotations-pod`. You have to provide it as a json formatted string to string map.

## Ingress Example

```yaml
apiVersion: voyager.appscode.com/v1
kind: Ingress
metadata:
  name: test-ingress
  namespace: default
  annotations:
    ingress.appscode.com/annotations-pod: '{"foo": "bar", "bar":"foo"}'
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

It will add following annotations to HAProxy pods:

```yaml
annotations:
    bar: foo
    foo: bar
    ingress.appscode.com/last-applied-annotation-keys: bar,foo
```

```bash
$ kubectl get pods voyager-test-ingress-6dbdbdf4f7-9f6w7 -o=jsonpath='{.metadata.annotations}' | tr " " "\n"

map[foo:bar
bar:foo
ingress.appscode.com/last-applied-annotation-keys:foo,bar]
```