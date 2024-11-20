# DEVOPSAREA K8S COURSE

1- Create deployment
```bash
kubectl create deployment nginx-dep --image=iginx
```


2- Describe deployment
```bash
 kubectl describe deployment nginx-dep
```
3- scalling up replicaset to be 7 pods
```bash
kubectl scale deployment nginx-dep --replicas=7

```

4-kubectl get po -o wide
```bash
NAME                         READY   STATUS             RESTARTS   AGE    IP           NODE       NOMINATED NODE   READINESS GATES
nginx-dep-5bd87f6766-66l6p   0/1     ImagePullBackOff   0          116s   10.244.0.5   minikube   <none>           <none>
nginx-dep-5bd87f6766-bczlf   0/1     ErrImagePull       0          116s   10.244.0.8   minikube   <none>           <none>
nginx-dep-5bd87f6766-bsjkm   0/1     ImagePullBackOff   0          15m    10.244.0.3   minikube   <none>           <none>
nginx-dep-5bd87f6766-j5mqm   0/1     ErrImagePull       0          116s   10.244.0.7   minikube   <none>           <none>
nginx-dep-5bd87f6766-j92ht   0/1     ImagePullBackOff   0          116s   10.244.0.4   minikube   <none>           <none>
nginx-dep-5bd87f6766-v4hcc   0/1     ErrImagePull       0          116s   10.244.0.6   minikube   <none>           <none>
nginx-dep-5bd87f6766-wzk68   0/1     ErrImagePull       0          116s   10.244.0.9   minikube   <none>           <none>

```
