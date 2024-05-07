# Pod

To create Pod:
```
kubectl create -f ./minikube/pod/pod-definition.yaml
```
To list pods:
```
kubectl get pods
```
To delete pod:
```
kubectl delete pod <pod_name>
```
or
```
kubectl delete -f ./minikube/pod/pod-definition.yaml
```

# ReplicaSet

To create ReplicaSet:

```
kubectl create -f ./minikube/replicaset/replicaset-definition.yaml
```

To list ReplicaSets:

```
kubectl get replicasets
```

There are several ways to edit ReplicaSet:

1) Make a change in its definition file and execute:
```
kubectl replace -f ./minikube/replicaset/replicaset-definition.yaml
```
2) To change replicas number:
```
kubectl scale --replicas=<new_value> -f ./minikube/replicaset/replicaset-definition.yaml
```
or
```
kubectl scale --replicas=<new_value> replicaset <replicaset_name>
```
3) Run
```
kubectl edit replicaset <replicaset_name>
```


To delete ReplicaSets:
```
kubectl delete -f ./minikube/replicaset/replicaset-definition.yaml
```