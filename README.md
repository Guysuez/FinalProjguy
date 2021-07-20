# FinalProjguy
YAMLs of first 16 questions:
first, if you cloned this repo, cd inside the folder "First-16-Question".

1. Deploy nginx pod:

```
 kubectl apply -f 01-nginx-pod-deploy.yml
```

```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl apply -f 01-nginx-pod-deploy.yml 
+pod/nginx-pod-guy created
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl get pods
+NAME                          READY   STATUS    RESTARTS   AGE
+nginx-pod-guy                 1/1     Running   0          27s

```




2. Deploy message pod:

```
kubectl apply -f 02-message-pod.yml
```
```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl apply -f 02-message-pod.yml 
+pod/messaging created
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl get pods
+NAME                          READY   STATUS    RESTARTS   AGE
+messaging                     1/1     Running   0          25s
```

3. create a namespace:
```
kubectl create -f 03-namespace.yml
```

```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl create -f 03-namespace.yml 
+namespace/apx-x998-guy created
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl get ns
+NAME                   STATUS   AGE
+apx-x998-guy           Active   25s
+default                Active   5d20h
+kube-node-lease        Active   5d20h
+kube-public            Active   5d20h
+kube-system            Active   5d20h
+kubernetes-dashboard   Active   4d23h
```



4. to create a json file with a list of nodes into a file named "nodes-guy", type this command: 

```
kubectl get -o json nodes > ./04-tmp/nodes-guy
```

solution is very long, added the folder and file into the git.

```diff
-cat ./04-tmp/nodes-guy
```

5. Create a service to expose message pod:
```
kubectl apply -f 05-06-service-messaging-service.yml
```
```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl apply -f 05-06-service-messaging-service.yml 
+service/messaging-service created
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl get svc
+NAME                TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
+kubernetes          ClusterIP   10.96.0.1        <none>        443/TCP    5d20h
+messaging-service   ClusterIP   10.105.184.201   <none>        6379/TCP   19s
```


7. create a deployment hr-web-app:

```
kubectl apply -f 07-hr-web-app-deployment.yml
```
```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl apply -f 07-hr-web-app-deployment.yml 
+deployment.apps/hr-web-app created
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl get deployments
+NAME         READY   UP-TO-DATE   AVAILABLE   AGE
+hr-web-app   2/2     2            2           35s
```

8. create a static-pod that uses busybox image and command sleep 1000:

```diff
+root@minikube:~# ls /etc/kubernetes/manifests/
+etcd.yaml            kube-controller-manager.yaml  static-busybox.yml
+kube-apiserver.yaml  kube-scheduler.yaml
+root@minikube:~# cat /etc/kubernetes/manifests/static-busybox.yml 
+apiVersion: v1
+kind: Pod
+metadata:
+ name: static-busybox
+spec:
+ containers:
+ - name: static-busybox
+   image: busybox
+   command: ["sleep"]
+   args: ["1000"]
+root@minikube:~# systemctl daemon-reload
+root@minikube:~# systemctl restart kubelet
+root@minikube:~# exit
+logout
+docker@minikube:~$ exit
+logout
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl get pods
+NAME                      READY   STATUS    RESTARTS   AGE
+static-busybox-minikube   1/1     Running   0          87s
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl delete pod static-busybox-minikube 
+pod "static-busybox-minikube" deleted
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl get pods
+NAME                      READY   STATUS    RESTARTS   AGE
+static-busybox-minikube   1/1     Running   0          32s
```


9. create a pod named temp-bus on a namespace named finance-guy:

```
kubectl apply -f 09-pod-temp-bus.yml
```
```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl apply -f 09-pod-temp-bus.yml 
+namespace/finance-guy created
+pod/temp-bus created
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl get ns
+NAME                   STATUS   AGE
+default                Active   5d20h
+finance-guy            Active   30s
+kube-node-lease        Active   5d20h
+kube-public            Active   5d20h
+kube-system            Active   5d20h
+kubernetes-dashboard   Active   5d
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl --namespace finance-guy get pods
+NAME       READY   STATUS    RESTARTS   AGE
+temp-bus   1/1     Running   0          81s
```


10. create persistent volume:

```
kubectl apply -f 10-persistent-volume.yml
```

```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl apply -f 10-persistent-volume.yml 
+persistentvolume/pv-analytics created
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl get pv
+NAME           CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS      CLAIM   STORAGECLASS   REASON   AGE
+pv-analytics   100Mi      RWX            Retain           Available                                   18s
```


11. create a pod with volume EmptyDir:

```
kubectl apply -f 11-Pod-with-Volume.yml
```
```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl apply -f 11-Pod-with-Volume.yml 
+pod/redis-storage-guy created
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl describe pod redis-storage-guy | grep Volume -B3 -A3
+  Ready             True 
+  ContainersReady   True 
+  PodScheduled      True 
+Volumes:
+  redis-storage-guy:
+    Type:       EmptyDir (a temporary directory that shares a pod's lifetime)
+    Medium:     
```


12. create a pod with a persistent volume attached:

```
kubectl apply -f 12-pv-1-attched-pod.yml
```
```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl apply -f 12-pv-1-attached-pod.yml 
+persistentvolume/pv1 created
+persistentvolumeclaim/pv1-claim created
+pod/use-pv-guy created
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl get pods
+NAME                      READY   STATUS    RESTARTS   AGE
+static-busybox-minikube   1/1     Running   1          23m
+use-pv-guy                1/1     Running   0          4m47s
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl get pv
+NAME                                       CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS      CLAIM               STORAGECLASS   REASON   AGE
+pv1                                        200Mi      RWO            Retain           Available                                               4m12s
+pvc-beacfeba-81b8-4186-9639-0b11947d70fe   100Mi      RWO            Delete           Bound       default/pv1-claim   standard                4m12s
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl describe pod use-pv-guy | grep -A3 -B3 Mounts
+    Ready:          True
+    Restart Count:  0
+    Environment:    <none>
+    Mounts:
+      /data from pv1-claim (rw)
+      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-ffpk8 (ro)
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl describe pod use-pv-guy | grep -A3 -B3 Volumes
+  Ready             True 
+  ContainersReady   True 
+  PodScheduled      True 
+Volumes:
+  pv1-claim:
+    Type:       PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace)
+    ClaimName:  pv1-claim
```

13. create deployment and record the update:
```
kubectl apply -f 13-Deploy-and-update.yml
```
```diff
+kubectl set image deployment/nginx-deploy nginx=nginx:1.17 --record
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl apply -f 13-Deploy-and-update.yml 
+deployment.apps/nginx-deploy created
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl set image deployment/nginx-deploy nginx=nginx:1.17 --record 
+deployment.apps/nginx-deploy image updated
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl describe deployments nginx-deploy | grep -A5 -B5 Annotations
+Name:                   nginx-deploy
+Namespace:              default
+CreationTimestamp:      Mon, 19 Jul 2021 22:20:40 +0300
+Labels:                 <none>
+Annotations:            deployment.kubernetes.io/revision: 2
+                        kubernetes.io/change-cause: kubectl set image deployment/nginx-deploy nginx=nginx:1.17 --record=true
+Selector:               app=nginx
+Replicas:               1 desired | 1 updated | 1 total | 1 available | 0 unavailable
+StrategyType:           RollingUpdate
+MinReadySeconds:        0
```


14. create an nginx pod, expose it and use image busybox:1.28 for dns lookup, record results in ./root/nginx....svc and ./root/nginx....pod.

```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl apply -f 14-deployment-exposed-and-recorded.yml 
+pod/nginx-resolver created
+service/nginx-resolver-service created
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl get pods
+NAME                      READY   STATUS      RESTARTS   AGE
+nginx-resolver            1/1     Running     0          38s
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl get svc nginx-resolver-service 
+NAME                     TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)   AGE
+nginx-resolver-service   ClusterIP   10.102.189.101   <none>        80/TCP    105s
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl run busybox-nslookup --image=busybox:1.28 -- nslookup nginx-resolver-service
+pod/busybox-nslookup created

```
didn't manage to make it work from here... recorded no results... :(


15. create static pod on node01 make sure it is restarted automatically:
```
<!-- minikube's option for nameing nodes is quite complex, I didn't rename and went on with minikube-m02 node. -->
```
```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ minikube ssh -n minikube-m02
+Last login: Mon Jul 19 18:50:50 2021 from 192.168.49.1
+docker@minikube-m02:~$ sudo -i
+root@minikube-m02:~# cd /etc/kubernetes/manifests/
+root@minikube-m02:/etc/kubernetes/manifests# cat nginx-critical.yml 
+apiVersion: v1
+kind: Pod
+metadata:
+root@minikube-m02:/etc/kubernetes/manifests# rm nginx-critical.yml 
+root@minikube-m02:/etc/kubernetes/manifests# cat <<EOF>> nginx-critical.yml
+> apiVersion: v1
+> kind: Pod
+> metadata:
+>  name: nginx-critical
+> spec:
+>  containers:
+>  - name: nginx-critical
+>    image: nginx
+> EOF
+root@minikube-m02:/etc/kubernetes/manifests# systemctl daemon-reload
+root@minikube-m02:/etc/kubernetes/manifests# systemctl restart kubelet
+root@minikube-m02:/etc/kubernetes/manifests# exit
+logout
+docker@minikube-m02:~$ exit
+logout
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl get pods
+NAME                          READY   STATUS    RESTARTS   AGE
+nginx-critical-minikube-m02   1/1     Running   0          42s
+static-busybox-minikube       1/1     Running   7          129m
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl delete pod nginx-critical-minikube-m02 
+pod "nginx-critical-minikube-m02" deleted
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl get pod nginx-critical-minikube-m02 
+NAME                          READY   STATUS    RESTARTS   AGE
+nginx-critical-minikube-m02   0/1     Pending   0          6s
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl get pod nginx-critical-minikube-m02 
+NAME                          READY   STATUS    RESTARTS   AGE
+nginx-critical-minikube-m02   1/1     Running   0          9s
```

16. create a pod called multi-pod with two containers:

```
kubectl apply -f 16-create-multi-pod.yml
```

```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl apply -f 16-create-multi-pod.yml 
+pod/multi-pod created
+Events:
+  Type    Reason     Age   From               Message
+  ----    ------     ----  ----               -------
+  Normal  Scheduled  68s   default-scheduler  Successfully assigned default/multi-pod to minikube-m03
+  Normal  Pulling    67s   kubelet            Pulling image "nginx"
+  Normal  Pulled     40s   kubelet            Successfully pulled image "nginx" in 27.198592767s
+  Normal  Created    40s   kubelet            Created container alpha
+  Normal  Started    40s   kubelet            Started container alpha
+  Normal  Pulling    40s   kubelet            Pulling image "busybox"
+  Normal  Pulled     37s   kubelet            Successfully pulled image "busybox" in 2.308581166s
+  Normal  Created    37s   kubelet            Created container beta
+  Normal  Started    37s   kubelet            Started container beta
```



Pod Design Questions:


1. Type the command for get pods with label information

```
kubectl get pods --show-labels
```
```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl get pods --show-labels 
+NAME                          READY   STATUS    RESTARTS   AGE     LABELS
+nginx-critical-minikube-m02   1/1     Running   0          5m26s   <none>
+static-busybox-minikube       1/1     Running   8          137m    <none>
```



2. Create 5 nginx pods in which two of them is labeled env=prod and three of them is labeled env=dev:

```
kubectl run "name" --image=nginx --labels env=prod (X2)
kubectl run "name" --image-nginx --labels env=dev (X3)
```
```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl run pod01 --image=nginx --labels env=prod
+pod/pod01 created
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl run pod02 --image=nginx --labels env=prod
+pod/pod02 created
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl run pod03 --image=nginx --labels env=dev
+pod/pod03 created
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl run pod04 --image=nginx --labels env=dev
+pod/pod04 created
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl run pod05 --image=nginx --labels env=dev
+pod/pod05 created
```


3. Verify all the pods are created with correct labels

```
kubectl get pods --show-labels
```
```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl get pods --show-labels 
+NAME                          READY   STATUS    RESTARTS   AGE     LABELS
+nginx-critical-minikube-m02   1/1     Running   0          9m16s   <none>
+pod01                         1/1     Running   0          94s     env=prod
+pod02                         1/1     Running   0          88s     env=prod
+pod03                         1/1     Running   0          75s     env=dev
+pod04                         1/1     Running   0          69s     env=dev
+pod05                         1/1     Running   0          62s     env=dev
+static-busybox-minikube       1/1     Running   8          140m    <none>
```


4. Get the pods with label env=dev

```
kubectl get pod -l env=dev
```
```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl get pod -l env=dev
+NAME    READY   STATUS    RESTARTS   AGE
+pod03   1/1     Running   0          112s
+pod04   1/1     Running   0          106s
+pod05   1/1     Running   0          99s
```


5. Get the pods with label env=dev and also output the labels

```
kubectl get pods -l env=dev --show-labels
```
```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl get pod -l env=dev --show-labels 
+NAME    READY   STATUS    RESTARTS   AGE     LABELS
+pod03   1/1     Running   0          3m1s    env=dev
+pod04   1/1     Running   0          2m55s   env=dev
+pod05   1/1     Running   0          2m48s   env=dev
```



6. Get the pods with label env=prod

```
kubectl get pods -l env=prod 
```

```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl get pod -l env=prod
+NAME    READY   STATUS    RESTARTS   AGE
+pod01   1/1     Running   0          4m26s
+pod02   1/1     Running   0          4m20s
```

7. Get the pods with label env=prod and also output the labels

```
kubectl get pods -l env=prod --show-labels
```
```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl get pods -l env=prod --show-labels
+NAME    READY   STATUS    RESTARTS   AGE     LABELS
+pod01   1/1     Running   0          5m11s   env=prod
+pod02   1/1     Running   0          5m5s    env=prod
```


8. Get the pods with label env

```
kubectl get pods -l env
```

```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl get pods -l env
+NAME    READY   STATUS    RESTARTS   AGE
+pod01   1/1     Running   0          5m38s
+pod02   1/1     Running   0          5m32s
+pod03   1/1     Running   0          5m19s
+pod04   1/1     Running   0          5m13s
+pod05   1/1     Running   0          5m6s
```


9. Get the pods with labels env=dev and env=prod

```
kubectl get pods -L env | egrep 'dev|prod'
```

```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl get pods -L env | egrep 'dev|prod'
+pod01                         1/1     Running   0          8m39s   prod
+pod02                         1/1     Running   0          8m33s   prod
+pod03                         1/1     Running   0          8m20s   dev
+pod04                         1/1     Running   0          8m14s   dev
+pod05                         1/1     Running   0          8m7s    dev
```


10. Get the pods with labels env=dev and env=prod and output the labels as well

```
kubectl get pods -l env --show-labels | egrep 'dev|prod'
```

```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl get pods -l env --show-labels | egrep 'dev|prod'
+pod01   1/1     Running   0          9m33s   env=prod
+pod02   1/1     Running   0          9m27s   env=prod
+pod03   1/1     Running   0          9m14s   env=dev
+pod04   1/1     Running   0          9m8s    env=dev
+pod05   1/1     Running   0          9m1s    env=dev
```


11. Change the label for one of the pod to env=uat and list all the pods to verify

```
kubectl label --overwrite pods/"podname" env=uat
```

```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl label pod pod01 env=uat --overwrite 
+pod/pod01 labeled
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl get pods --show-labels 
+NAME                          READY   STATUS    RESTARTS   AGE    LABELS
+nginx-critical-minikube-m02   1/1     Running   0          19m    <none>
+pod01                         1/1     Running   0          11m    env=uat
+pod02                         1/1     Running   0          11m    env=prod
+pod03                         1/1     Running   0          11m    env=dev
+pod04                         1/1     Running   0          11m    env=dev
+pod05                         1/1     Running   0          11m    env=dev
+static-busybox-minikube       1/1     Running   9          150m   <none>
```



12. Remove the labels for the pods that we created now and verify all the labels are removed

to remove:
```
kubectl label pods -l env env-
```
```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl label pods -l env env-
+pod/pod01 labeled
+pod/pod02 labeled
+pod/pod03 labeled
+pod/pod04 labeled
+pod/pod05 labeled
```


to verify:
```
kubectl get pods --show-labels
```

```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl get pod --show-labels 
+NAME                          READY   STATUS    RESTARTS   AGE    LABELS
+nginx-critical-minikube-m02   1/1     Running   0          20m    <none>
+pod01                         1/1     Running   0          12m    <none>
+pod02                         1/1     Running   0          12m    <none>
+pod03                         1/1     Running   0          12m    <none>
+pod04                         1/1     Running   0          12m    <none>
+pod05                         1/1     Running   0          12m    <none>
+static-busybox-minikube       1/1     Running   9          152m   <none>
```


13. Let’s add the label app=nginx for all the pods and verify (using kubectl)

```
kubectl pods label --all app=nginx
```
```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl label pods --all app=nginx
+pod/nginx-critical-minikube-m02 labeled
+pod/pod01 labeled
+pod/pod02 labeled
+pod/pod03 labeled
+pod/pod04 labeled
+pod/pod05 labeled
+pod/static-busybox-minikube labeled
```


to verify:
```
kubectl get pods --show-labels
```
```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl get pods --show-labels
+NAME                          READY   STATUS    RESTARTS   AGE    LABELS
+nginx-critical-minikube-m02   1/1     Running   0          22m    app=nginx
+pod01                         1/1     Running   0          15m    app=nginx
+pod02                         1/1     Running   0          15m    app=nginx
+pod03                         1/1     Running   0          14m    app=nginx
+pod04                         1/1     Running   0          14m    app=nginx
+pod05                         1/1     Running   0          14m    app=nginx
+static-busybox-minikube       1/1     Running   9          154m   app=nginx
```



14. Get all the nodes with labels (if using minikube you would get only master node)

```
kubectl get nodes --show-labels
```
```difd
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl get nodes --show-labels
+NAME           STATUS   ROLES    AGE     VERSION   LABELS
+minikube       Ready    <none>   3d11h   v1.21.2   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=minikube,kubernetes.io/os=linux
+minikube-m02   Ready    <none>   31h     v1.21.2   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=minikube-m02,kubernetes.io/os=linux
+minikube-m03   Ready    <none>   3h58m   v1.21.2   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=minikube-m03,kubernetes.io/os=linux
```


15. Label the worker node nodeName=nginxnode

```
kubectl label node/"nodename" nodeName=nginxnode
```
```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl label node minikube-m02 nodeName=nginxnode
+node/minikube-m02 labeled
```

verify:
```
kubectl get nodes --show-labels 
```
```difd
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl get node minikube-m02 --show-labels 
+NAME           STATUS   ROLES    AGE   VERSION   LABELS
+minikube-m02   Ready    <none>   31h   v1.21.2   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=minikube-m02,kubernetes.io/os=linux,nodeName=nginxnode
```



16. Create a Pod that will be deployed on the worker node with the label nodeName=nginxnode
```
kubectl apply -f Answer-for-Pod-design-Q16
```
```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl apply -f ../Pod-Design-Questions/Answer-for-Pod-design-Q16.yml 
+pod/nginx created
```

17. Verify the pod that it is scheduled with the node selector on the right node… fix it if it’s not behind scheduled.

```
kubectl get pod nginx -o wide 
```
```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl get pod nginx -o wide
+NAME    READY   STATUS    RESTARTS   AGE   IP           NODE           NOMINATED NODE   READINESS GATES
+nginx   1/1     Running   0          99s   172.17.0.5   minikube-m02   <none>           <none>
```


18. Verify the pod nginx that we just created has this label

```
kubectl describe pod nginx | grep Node-Selectors
```
```difd
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/First-16-Questions$ kubectl describe pod nginx | grep Node-Selectors
+Node-Selectors:              nodeName=nginxnode
```


Deployments:

1. Create the deployment:

```
kubectl create deployment webapp --image=nginx --dry-run -o yaml > webapp.yaml
```

to run it with the 5 replicas already made, apply the file I edited; called 01-webapp.yaml under Deployments directory.

```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/Deployments$ kubectl apply -f 01-webapp.yaml 
+deployment.apps/webapp created
```


2. Get the deployment rollout status

```
kubectl rollout status deployments/webapp
```
```difd
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/Deployments$ kubectl rollout status deployment webapp 
+deployment "webapp" successfully rolled out
```


3. Get the replicaset that created with this deployment

```
kubectl get replicasets
```
```difd
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/Deployments$ kubectl get replicasets
+NAME               DESIRED   CURRENT   READY   AGE
+webapp-5654c984c   5         5         5       118s
```


4. EXPORT the yaml of the replicaset and pods of this deployment

```
kubectl get deployments/webapp -o yaml > "filename"
```
```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/Deployments$ kubectl get deployments/webapp -o yaml > 04-webapp-deployment.yaml
```
```
kubectl get replicaset webapp-"result of Q3" -o yaml > "filename"
```
```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/Deployments$ kubectl get replicaset webapp-5654c984c -o yaml > 04-webapp-replicaset.yaml
```

5. Delete the deployment you just created and watch all the pods are also being deleted

```
kubectl delete -f 01-webapp.yaml
```
```
kubectl get pods --watch
```

```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/Deployments$ kubectl delete -f 01-webapp.yaml 
+^[[A^[[A^[[A^[[Adeployment.apps "webapp" deleted
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/Deployments$ kubectl get pods --watch
+NAME                          READY   STATUS        RESTARTS   AGE
+nginx-critical-minikube-m02   1/1     Running       0          8m26s
+static-busybox-minikube       1/1     Running       10         8m26s
+webapp-5654c984c-6ljx8        0/1     Terminating   0          28s
+webapp-5654c984c-cdvs2        0/1     Terminating   0          28s
+webapp-5654c984c-hv9vt        0/1     Terminating   0          28s
+webapp-5654c984c-t24s2        0/1     Terminating   0          28s
+webapp-5654c984c-cdvs2        0/1     Terminating   0          33s
+webapp-5654c984c-cdvs2        0/1     Terminating   0          33s
+webapp-5654c984c-6ljx8        0/1     Terminating   0          33s
+webapp-5654c984c-6ljx8        0/1     Terminating   0          33s
+webapp-5654c984c-t24s2        0/1     Terminating   0          34s
+webapp-5654c984c-t24s2        0/1     Terminating   0          34s
+webapp-5654c984c-hv9vt        0/1     Terminating   0          34s
+webapp-5654c984c-hv9vt        0/1     Terminating   0          34s
+^Cguy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/Deployments$ kubectl get pods --watch
+NAME                          READY   STATUS    RESTARTS   AGE
+nginx-critical-minikube-m02   1/1     Running   0          8m45s
+static-busybox-minikube       1/1     Running   10         8m45s
```


6. Create a deployment of webapp with image nginx:1.17.1 with container port 80 and verify the image version

```
kubectl create deploy webapp --image=nginx:1.17.1 --dry-run -o yaml > 06-webapp.yaml
```
```
for comfort run kubectl apply -f 06-webapp.yaml
```

```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/Deployments$ kubectl apply -f 06-webapp.yaml 
+deployment.apps/webapp created
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/Deployments$ kubectl describe pod webapp-b7889ff56-xk4vd  | grep image
+  Normal  Pulling    2m46s  kubelet            Pulling image "nginx:1.17.1"
+  Normal  Pulled     2m25s  kubelet            Successfully pulled image "nginx:1.17.1" in 21.184697008s
```


7. Update the deployment with the image version 1.17.4 and verify

```difd
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/Deployments$ kubectl rollout status deployment webapp 
+Waiting for deployment "webapp" rollout to finish: 1 old replicas are pending termination...
+Waiting for deployment "webapp" rollout to finish: 1 old replicas are pending termination...
+deployment "webapp" successfully rolled out
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/Deployments$ kubectl set image deployments webapp nginx=nginx:1.17.4
+deployment.apps/webapp image updated
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/Deployments$ kubectl describe pod webapp-9cf988f87-vpxjp  | grep image
+  Normal  Pulling    54s   kubelet            Pulling image "nginx:1.17.4"
+  Normal  Pulled     32s   kubelet            Successfully pulled image "nginx:1.17.4" in 22.303459691s
```

8. Check the rollout history and make sure everything is ok after the update

```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/Deployments$ kubectl rollout history deployment webapp 
+deployment.apps/webapp 
+REVISION  CHANGE-CAUSE
+1         <none>
+2         <none>
```



9. Undo the deployment to the previous version 1.17.1 and verify Image has the
previous version

```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/Deployments$ kubectl rollout undo deployment webapp 
+deployment.apps/webapp rolled back
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/Deployments$ kubectl rollout status deployment webapp 
+deployment "webapp" successfully rolled out
```


10. Update the deployment with the wrong image version 1.100 and verify something is wrong with the deployment

```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/Deployments$ kubectl set image deployment webapp nginx=nginx:1.000
+deployment.apps/webapp image updated
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/Deployments$ kubectl rollout status deployment webapp 
+Waiting for deployment "webapp" rollout to finish: 1 old replicas are pending termination...
```
a. Expect: kubectl get pods (ImagePullErr)

```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/Deployments$ kubectl get pods 
+NAME                          READY   STATUS             RESTARTS   AGE
+nginx-critical-minikube-m02   1/1     Running            0          23m
+static-busybox-minikube       1/1     Running            11         23m
+webapp-7d8467f67-lhmzx        0/1     ImagePullBackOff   0          57s
+webapp-b7889ff56-m4rw5        1/1     Running            0          2m3s
```

b. Undo the deployment with the previous version and verify everything is Ok

```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/Deployments$ kubectl rollout undo deployment webapp 
+deployment.apps/webapp rolled back
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/Deployments$ kubectl rollout status deployment webapp 
+deployment "webapp" successfully rolled out
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/Deployments$ kubectl rollout history deployment webapp 
+deployment.apps/webapp 
+REVISION  CHANGE-CAUSE
+2         <none>
+4         <none>
+5         <none>
```

d. Check the history of the specific revision of that deployment

```difd
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/Deployments$ kubectl rollout history deployment  webapp --revision=5
+deployment.apps/webapp with revision #5
+Pod Template:
+  Labels:	app=webapp
+	pod-template-hash=b7889ff56
+  Containers:
+   nginx:
+    Image:	nginx:1.17.1
+    Port:	80/TCP
+    Host Port:	0/TCP
+    Environment:	<none>
+    Mounts:	<none>
+  Volumes:	<none>
```

  e. update the deployment with the image version latest and check the history and verify nothing is going on

```difd
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/Deployments$ kubectl set image deploy webapp nginx=nginx:latest
+deployment.apps/webapp image updated
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/Deployments$ kubectl rollout history deployment webapp 
+deployment.apps/webapp 
+REVISION  CHANGE-CAUSE
+2         <none>
+4         <none>
+5         <none>
+6         <none>
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/Deployments$ kubectl get pods
+NAME                          READY   STATUS    RESTARTS   AGE
+nginx-critical-minikube-m02   1/1     Running   0          33m
+static-busybox-minikube       1/1     Running   12         33m
+webapp-6b9d4c7497-4dptj       1/1     Running   0          5m19s
```


11. Apply the autoscaling to this deployment with and verify hpa is created and replicas are increased

```difd
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/Deployments$ kubectl autoscale deployment webapp --max=20 --min=10 --cpu-percent=85
+horizontalpodautoscaler.autoscaling/webapp autoscaled
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/Deployments$ kubectl get horizontalpodautoscalers.autoscaling webapp 
+NAME     REFERENCE           TARGETS         MINPODS   MAXPODS   REPLICAS   AGE
+webapp   Deployment/webapp   <unknown>/85%   10        20        10         69s
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/Deployments$ kubectl get deployments.apps 
+NAME     READY   UP-TO-DATE   AVAILABLE   AGE
+webapp   10/10   10           10          24m
```

13. Clean the cluster by deleting deployment and hpa you just created

```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/Deployments$ kubectl delete horizontalpodautoscalers.autoscaling webapp 
+horizontalpodautoscaler.autoscaling "webapp" deleted
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/Deployments$ kubectl delete -f 0
+01-webapp.yaml             04-webapp-replicaset.yaml
+04-webapp-deployment.yaml  06-webapp.yaml
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/Deployments$ kubectl delete -f 06-webapp.yaml 
+deployment.apps "webapp" deleted
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/Deployments$ kubectl get pods
+NAME                          READY   STATUS    RESTARTS   AGE
+nginx-critical-minikube-m02   1/1     Running   0          37m
+static-busybox-minikube       1/1     Running   12         37m
```

14. Create a job and make it run 10 times one after one (run > exit > run >exit ..) using
the following configuration:

```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/Deployments$ kubectl create job hello-job --image=busybox --dry-run -o yaml -- echo "hello I am from job" > hello-job.yaml
+W0720 01:27:12.313473 2496665 helpers.go:557] --dry-run is deprecated and can be replaced with --dry-run=client.
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/Deployments$ kubectl delete -f hello-job.yaml 
+job.batch "hello-job" deleted
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/Deployments$ kubectl apply -f hello-job.yaml 
+job.batch/hello-job created
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/Deployments$ kubectl get jobs
+NAME        COMPLETIONS   DURATION   AGE
+hello-job   1/10          5s         5s
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/Deployments$ kubectl get jobs
+NAME        COMPLETIONS   DURATION   AGE
+hello-job   1/10          8s         8s
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/Deployments$ kubectl get jobs
+NAME        COMPLETIONS   DURATION   AGE
+hello-job   2/10          10s        10s
```


CONFIG MAP:

1. Create a file called config.txt with two values key1=value1 and key2=value2 and
verify the file

```difd
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/CONFIG-MAP$ cat >> config.txt <<EOF
+> key1=value1
+> key2=value2
+> EOF
```

2. Create a configmap named keyvalcfgmap and read data from the file config.txt and verify that configmap is created correctly:

```difd
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/CONFIG-MAP$ kubectl create configmap keyvalcfgmap --from-file=config.txt 
+configmap/keyvalcfgmap created
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/CONFIG-MAP$ kubectl get configmaps 
+NAME               DATA   AGE
+keyvalcfgmap       1      55s
+kube-root-ca.crt   1      6d
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/CONFIG-MAP$ kubectl describe configmaps keyvalcfgmap 
+Name:         keyvalcfgmap
+Namespace:    default
+Labels:       <none>
+Annotations:  <none>
+
+Data
+====
+config.txt:
+----
+key1=value1
+key2=value2
+
+Events:  <none>
```


3. Create an nginx pod and load environment values from the above configmap
keyvalcfgmap and exec into the pod and verify the environment variables and delete
the pod:

```diff
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/CONFIG-MAP$ kubectl apply -f nginx-pod.yml 
+pod/nginx created
+guy@virtbuntu:~/Desktop/Kubernetes/git/FinalProjguy/CONFIG-MAP$ kubectl exec -it nginx -- env
+PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
+HOSTNAME=nginx
+TERM=xterm
+config.txt=key1=value1
+key2=value2

+KUBERNETES_PORT_443_TCP=tcp://10.96.0.1:443
+KUBERNETES_PORT_443_TCP_PROTO=tcp
+KUBERNETES_PORT_443_TCP_PORT=443
+KUBERNETES_PORT_443_TCP_ADDR=10.96.0.1
+KUBERNETES_SERVICE_HOST=10.96.0.1
+KUBERNETES_SERVICE_PORT=443
+KUBERNETES_SERVICE_PORT_HTTPS=443
+KUBERNETES_PORT=tcp://10.96.0.1:443
+NGINX_VERSION=1.21.1
+NJS_VERSION=0.6.1
+PKG_RELEASE=1~buster
+HOME=/root
```

Thanks for reading :)
