# Question 16:

![](./context16.png)

#### Task -
Create a new PersistentVolumeClaim:

✑ Name: ```pv-volume```

✑ Class: ```csi-hostpath-sc```

✑ Capacity: ```10Mi```

Create a new Pod which mounts the PersistentVolumeClaim as a volume:

✑ Name: ```web-server```

✑ Image: ```nginx```

✑ Mount path: ```/usr/share/nginx/html```

Configure the new Pod to have ReadWriteOnce access on the volume.
Finally, using kubectl edit or kubectl patch expand the PersistentVolumeClaim to a capacity of ```70Mi``` and record that change.

## Correct Answer:

- Create a Persistent Volume Claim:
```
$ vi pvc.yaml
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pv-volume
spec:
  storageClassName: csi-hostpath-sc
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 10Mi
```
```
$ kubectl apply -f pvc.yaml
```

- Create a Pod:
```
$ vi pod.yaml
apiVersion: v1
kind: Pod
metadata:
  name: web-server
spec:
  volumes:
  - name: vol
    persistentVolumeClaim:
        claimName: pv-volume
  containers:
  - name: web-server
    image: "nginx"
    volumeMounts:
    - name: vol
      mountPath: /usr/share/nginx/html
```