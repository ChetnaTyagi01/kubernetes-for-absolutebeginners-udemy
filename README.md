# Creating Kubernetes PODs using YAML Configuration file

PS C:\Users\tyache01\Downloads\kubernetes-for-absolutebeginners-udemy\pods>kubectl create -f pod.yaml    
pod/nginx created

PS C:\Users\tyache01\Downloads\kubernetes-for-absolutebeginners-udemy\pods> kubectl get pods
NAME    READY   STATUS              RESTARTS   AGE
nginx   0/1     ContainerCreating   0          3s

PS C:\Users\tyache01\Downloads\kubernetes-for-absolutebeginners-udemy\pods> kubectl get pods
NAME    READY   STATUS    RESTARTS   AGE
nginx   1/1     Running   0          10s

PS C:\Users\tyache01\Downloads\kubernetes-for-absolutebeginners-udemy\pods> kubectl describe pods 
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

PS C:\Users\tyache01\Downloads\kubernetes-for-absolutebeginners-udemy\pods> kubectl get pods -o wide
NAME    READY   STATUS    RESTARTS   AGE   IP           NODE       NOMINATED NODE   READINESS GATES
nginx   1/1     Running   0          46s   10.244.0.8   minikube   <none>           <none>