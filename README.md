# Creating Kubernetes PODs using YAML Configuration file

- kubectl create -f pod.yaml    

pod/nginx created


- kubectl get pods

NAME    READY   STATUS              RESTARTS   AGE

nginx   0/1     ContainerCreating   0          3s


- kubectl get pods

NAME    READY   STATUS    RESTARTS   AGE

nginx   1/1     Running   0          10s


- kubectl describe pods 

Name:             nginx
Namespace:        default
Priority:         0
Service Account:  default
Node:             minikube/192.168.59.104
Start Time:       Tue, 21 Feb 2023 17:37:03 +0530
Labels:           app=nginx
                  tier=frontend
Annotations:      <none>
Status:           Running
IP:               10.244.0.8
IPs:
  IP:  10.244.0.8
Containers:
  nginx:
    Container ID:   docker://859415fed9daa616b024ce0aa196190aadb290fe59d270970d168512fb67b1a4
    Image:          nginx
    Image ID:       docker-pullable://nginx@sha256:6650513efd1d27c1f8a5351cbd33edf85cc7e0d9d0fcb4ffb23d8fa89b601ba8
    Port:           <none>
    Host Port:      <none>
    State:          Running
      Started:      Tue, 21 Feb 2023 17:37:10 +0530
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
Conditions:
  Type              Status
  Initialized       True
  Ready             True
  ContainersReady   True
  PodScheduled      True
Volumes:
  kube-api-access-6zfkh:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type    Reason     Age   From               Message
  ----    ------     ----  ----               -------
  Normal  Scheduled  23s   default-scheduler  Successfully assigned default/nginx to minikube
  Normal  Pulling    21s   kubelet            Pulling image "nginx"
  Normal  Pulled     17s   kubelet            Successfully pulled image "nginx" in 3.620466616s (3.620473393s including waiting)
  Normal  Created    17s   kubelet            Created container nginx
  Normal  Started    16s   kubelet            Started container nginx


- kubectl get pods -o wide

NAME    READY   STATUS    RESTARTS   AGE   IP           NODE       NOMINATED NODE   READINESS GATES

nginx   1/1     Running   0          46s   10.244.0.8   minikube   <none>           <none>

# Creating ReplicaSets

- kubectl create -f .\replicaset.yaml

replicaset.apps/myapp-replicaset created


- kubectl get replicaset

NAME               DESIRED   CURRENT   READY   AGE

myapp-replicaset   3         3         3       24s


- kubectl get pods

NAME                     READY   STATUS    RESTARTS   AGE

myapp-replicaset-hwtgf   1/1     Running   0          66s

pod "myapp-replicaset-hwtgf" deleted


- kubectl get pods

NAME                     READY   STATUS    RESTARTS   AGE

myapp-replicaset-nbvqr   1/1     Running   0          12s

myapp-replicaset-qghfm   1/1     Running   0          3m41s

myapp-replicaset-tb98q   1/1     Running   0          3m40s


- kubectl describe replicaset myapp-replicaset 

Name:         myapp-replicaset
Namespace:    default
Selector:     app=myapp
Labels:       app=myapp
Annotations:  <none>
Replicas:     3 current / 3 desired
Pods Status:  3 Running / 0 Waiting / 0 Succeeded / 0 Failed
Pod Template:
  Labels:  app=myapp
  Containers:
   nginx:
    Image:        nginx
    Port:         <none>
    Host Port:    <none>
    Environment:  <none>
    Mounts:       <none>
Events:
  Type    Reason            Age    From                   Message
  Normal  SuccessfulCreate  5m24s  replicaset-controller  Created pod: myapp-replicaset-qghfm
  Normal  SuccessfulCreate  5m23s  replicaset-controller  Created pod: myapp-replicaset-tb98q
  Normal  SuccessfulCreate  115s   replicaset-controller  Created pod: myapp-replicaset-nbvqr


- kubectl edit replicaset myapp-replicaset

replicaset.apps/myapp-replicaset edited


- kubectl get pods

NAME                     READY   STATUS              RESTARTS   AGE

myapp-replicaset-27p5c   0/1     ContainerCreating   0          11s

myapp-replicaset-nbvqr   1/1     Running             0          19m

myapp-replicaset-qghfm   1/1     Running             0          22m

myapp-replicaset-tb98q   1/1     Running             0          22m


- kubectl get pods

NAME                     READY   STATUS    RESTARTS   AGE 

myapp-replicaset-27p5c   1/1     Running   0          110s

myapp-replicaset-nbvqr   1/1     Running   0          20m 

myapp-replicaset-qghfm   1/1     Running   0          24m 

myapp-replicaset-tb98q   1/1     Running   0          24m


- kubectl scale replicaset myapp-replicaset --replicas=2

replicaset.apps/myapp-replicaset scaled


- kubectl get pods

NAME                     READY   STATUS        RESTARTS   AGE  

myapp-replicaset-27p5c   1/1     Terminating   0          2m21s

myapp-replicaset-nbvqr   1/1     Terminating   0          21m

myapp-replicaset-qghfm   1/1     Running       0          24m

myapp-replicaset-tb98q   1/1     Running       0          24m


- kubectl get pods

NAME                     READY   STATUS    RESTARTS   AGE

myapp-replicaset-qghfm   1/1     Running   0          25m

myapp-replicaset-tb98q   1/1     Running   0          25m

# Creating Deployments

- kubectl get pods

No resources found in default namespace.


- kubectl create -f .\deployment.yaml

deployment.apps/myapp-deployment created


- kubectl get deployments

NAME               READY   UP-TO-DATE   AVAILABLE   AGE

myapp-deployment   0/3     3            0           8s


- kubectl get replicasets

NAME                          DESIRED   CURRENT   READY   AGE

myapp-deployment-576897dc49   3         3         3       17s


- kubectl get pods 

NAME                                READY   STATUS    RESTARTS   AGE 

myapp-deployment-576897dc49-qplqf   1/1     Running   0          1m6s

myapp-deployment-576897dc49-r8s46   1/1     Running   0          1m6s

myapp-deployment-576897dc49-zq5fn   1/1     Running   0          1m6s


- kubectl get all

NAME                                    READY   STATUS    RESTARTS   AGE  

pod/myapp-deployment-576897dc49-qplqf   1/1     Running   0          3m21s

pod/myapp-deployment-576897dc49-r8s46   1/1     Running   0          3m21s

pod/myapp-deployment-576897dc49-zq5fn   1/1     Running   0          3m21s

NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE 

service/kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   2d  

NAME                               READY   UP-TO-DATE   AVAILABLE   AGE   

deployment.apps/myapp-deployment   3/3     3            3           3m22s 

NAME                                          DESIRED   CURRENT   READY   AGE  

replicaset.apps/myapp-deployment-576897dc49   3         3         3       3m22s


- kubectl describe deployment myapp-deployment

Name:                   myapp-deployment
Namespace:              default
CreationTimestamp:      Wed, 22 Feb 2023 16:27:53 +0530
Labels:                 app=myapp
Annotations:            deployment.kubernetes.io/revision: 1
Selector:               app=myapp
Replicas:               3 desired | 3 updated | 3 total | 3 available | 0 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  25% max unavailable, 25% max surge
Pod Template:
  Labels:  app=myapp
  Containers:
   nginx:
    Image:        nginx
    Port:         <none>
    Host Port:    <none>
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Available      True    MinimumReplicasAvailable
  Progressing    True    NewReplicaSetAvailable
OldReplicaSets:  <none>
NewReplicaSet:   myapp-deployment-576897dc49 (3/3 replicas created)
Events:
  Type    Reason             Age    From                   Message
  ----    ------             ----   ----                   -------
  Normal  ScalingReplicaSet  4m21s  deployment-controller  Scaled up replica set myapp-deployment-576897dc49 to 3