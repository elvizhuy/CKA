# Question 17:

![](./context17.png)

#### Task -
Create a new nginx Ingress resource as follows:

✑ Name: ```pong```

✑ Namespace: ```ing-internal```

✑ Exposing service ```hello``` on path ```/hello``` using service port ```5678```

## Correct Answer:

- Create an nginx Ingress:
```
$ vi ingress.yaml
---
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: pong
  namespace: ing-internal
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - http:
      paths:
      - path: /hello
        pathType: Prefix
        backend:
          service:
            name: hello
            port:
              number: 5678
```
```
$ kubectl apply -f ingress.yaml
```

- Link: https://kubernetes.io/docs/concepts/services-networking/ingress/
- Search: ```ingress```