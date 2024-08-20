# Task 1 [Pods, ReplicaSet, Deployment]
1- Create a pod with the name redis and with the image redis.
```bash
$ kubectl apply -f pod_redis.yml
NAME    READY   STATUS              RESTARTS      AGE
ngnix   0/1     ContainerCreating   0             3s
```

3- Create a pod with the name nginx and with the image “nginx123”
Use a pod-definition YAML file.

-> Not an image name

5- Change the nginx pod image to “nginx” check the status again
```bash
pod/ngnix created

NAME    READY   STATUS              RESTARTS      AGE
nginx   1/1     Running             0             38s
redis   1/1     Running             1 (11m ago)   24h
```

7- create a ReplicaSet with
name= replica-set-1
image= busybox
replicas= 3
```bash
--> kubectl get po
NAME                  READY   STATUS         RESTARTS      AGE
nginx                 1/1     Running        0             15m
ngnix                 0/1     ErrImagePull   0             16m
redis                 1/1     Running        1 (28m ago)   24h
replica-set-1-8cgqx   1/1     Running        0             12s
replica-set-1-ch6fl   1/1     Running        0             12s
replica-set-1-srsgw   1/1     Running        0             12s
--> kubectl get replicaset
NAME            DESIRED   CURRENT   READY   AGE
replica-set-1   3         3         3       23s
```


8- Scale the ReplicaSet replica-set-1 to 5 PODs.
```bash
--->  kubectl get replicaset
NAME            DESIRED   CURRENT   READY   AGE
replica-set-1   5         5         5       2m16s
```


