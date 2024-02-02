# Question 15:

![](./context15.png)

#### Task -
A Kubernetes worker node, named ```wk8s-node-0``` is in state NotReady.

Investigate why this is the case, and perform any appropriate steps to bring the node to a Ready state, ensuring that any changes are made permanent.

![](./note15.png)

## Correct Answer:

- SSH to the master node:
```
$ ssh wk8s-node-0
....
....
$ sudo -i
```

- Restart the kubelet service & show status:
```
$ systemctl restart kubelet
...

$ systemctl status kubelet
```
