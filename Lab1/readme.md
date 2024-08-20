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

10- Delete any one of the 5 PODs then check How many PODs exist now?
Why are there still 5 PODs, even after you deleted one?
```bash 
--> Replica set created another one 

NAME                  READY   STATUS             RESTARTS      AGE
nginx                 1/1     Running            0             20m
ngnix                 0/1     ImagePullBackOff   0             21m
redis                 1/1     Running            1 (33m ago)   24h
replica-set-1-8cgqx   1/1     Running            0             4m41s
replica-set-1-ch6fl   1/1     Running            0             4m41s
replica-set-1-fz64m   1/1     Running            0             2m46s
replica-set-1-kwqpq   1/1     Running            0             2m46s
replica-set-1-srsgw   1/1     Running            0             4m41s

-->kubectl delete pod replica-set-1-8cgqx
pod "replica-set-1-8cgqx" deleted

--->kubectl get po
NAME                  READY   STATUS             RESTARTS      AGE
nginx                 1/1     Running            0             21m
ngnix                 0/1     ImagePullBackOff   0             22m
redis                 1/1     Running            1 (33m ago)   24h
replica-set-1-45zcl   1/1     Running            0             38s
replica-set-1-ch6fl   1/1     Running            0             5m32s
replica-set-1-fz64m   1/1     Running            0             3m37s
replica-set-1-kwqpq   1/1     Running            0             3m37s
replica-set-1-srsgw   1/1     Running            0             5m32s
```

13- How many Deployments and ReplicaSets exist on the system now?
```bash
--->kubectl get deployments
NAME           READY   UP-TO-DATE   AVAILABLE   AGE
deployment-1   3/3     3            3           12s

-->kubectl get po
NAME                            READY   STATUS         RESTARTS      AGE
deployment-1-58dcf7dd57-68nsh   1/1     Running        0             16s
deployment-1-58dcf7dd57-9qxjh   1/1     Running        0             16s
deployment-1-58dcf7dd57-fh9j4   1/1     Running        0             16s
```

15- Update deployment-1 image to nginx then check the ready pods again
--> Creating a new replicaset with 3 new pods and deleting the old replica and it's pod
```bash
deployment-1-58dcf7dd57-68nsh   1/1     Terminating        0             3m22s
deployment-1-58dcf7dd57-9qxjh   1/1     Terminating        0             3m22s
deployment-1-58dcf7dd57-fh9j4   1/1     Terminating        0             3m22s
deployment-1-7d48865487-n5fgp   1/1     Running            0             22s
deployment-1-7d48865487-tc6sj   1/1     Running            0             33s
deployment-1-7d48865487-v9l7f   1/1     Running            0             29s
```
16- Run kubectl describe deployment deployment-1 and check events
What is the deployment strategy used to upgrade the deployment-1?
```bash
  Type    Reason             Age    From                   Message
  ----    ------             ----   ----                   -------
  Normal  ScalingReplicaSet  10m    deployment-controller  Scaled up replica set deployment-1-58dcf7dd57 to 3
  Normal  ScalingReplicaSet  7m25s  deployment-controller  Scaled up replica set deployment-1-7d48865487 to 1
  Normal  ScalingReplicaSet  7m21s  deployment-controller  Scaled down replica set deployment-1-58dcf7dd57 to 2 from 3
  Normal  ScalingReplicaSet  7m21s  deployment-controller  Scaled up replica set deployment-1-7d48865487 to 2 from 1
  Normal  ScalingReplicaSet  7m14s  deployment-controller  Scaled down replica set deployment-1-58dcf7dd57 to 1 from 2
  Normal  ScalingReplicaSet  7m14s  deployment-controller  Scaled up replica set deployment-1-7d48865487 to 3 from 2
  Normal  ScalingReplicaSet  7m11s  deployment-controller  Scaled down replica set deployment-1-58dcf7dd57 to 0 from 1
```

17- Rollback the deployment-1

```bash
 ---->kubectl rollout status deployment/deployment-1
deployment "deployment-1" successfully rolled out
```
