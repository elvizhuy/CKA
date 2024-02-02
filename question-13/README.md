# Question 13:

![](./context13.png)

#### Context
An existing Pod needs to be integrated into the Kubernetes built-in logging architecture (e.g. kubectl logs). Adding a streaming sidecar container is a good and common way to accomplish this requirement.

#### Task -
Add a sidecar container named ```sidecar```, using the busybox image, to the existing Pod ```big-corp-app```. The new sidecar container has to run the following command:

![](./note13-01.png)

Use a Volume, mounted at ```/var/log```, to make the log ```file big-corp-app.log``` available to the sidecar container.

![](./note13-02.png)

## Correct Answer:

- Create a container ```sidecar```. Edit pod ```big-corp-app```:
```
$ kubectl edit pod big-corp-app
...
  containers:
  - name: sidecar
    image: busybox
    command: ["/bin/sh", "-c", "tail -n+1 -f /var/log/big-corp-app.log"]
    volumeMounts:
    - name: varlog
      mountPath: /var/log
  volumes:
  - name: varlog
    emptyDir: {}
...
```

- Link: https://kubernetes.io/docs/concepts/cluster-administration/logging/
- Search: ```sidecar pod```