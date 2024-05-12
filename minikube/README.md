# Pod

To create Pod:
```
kubectl create -f ./minikube/pod/pod-definition.yaml
```
To list pods:
```
kubectl get pods
```
To list all pods and their labels:
```
$ kubectl get pods -A --show-labels
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
or
```
kubectl delete rs <replicaset_name>
```

# Deployment

To create a deployment from a definition file:
```
kubectl create -f ./minikube/deployment/deployment_definition.yaml
```
If number of deployment definition attributes is small, we can create a deployment without the full-blown definition file:
```
kubectl create deployment <deployment_name> --image=<image_name> --replicas=<replicas_count>
```
To list Deployments:

```
kubectl get deployments
```
To see the status of the rollout:
```
$ kubectl rollout status deployment/<deployment_name>
```
To see the revisions and history of rollouts run:
```
$ kubectl rollout history deployment/<deployment_name>
```
To see details about specific revision:
```
$ kubectl rollout history deployment/<deployment_name> --revision=<revision_number>
```

# Services

To create a service:
```
$ kubectl create -f path/to/service-definition.yaml
```
To list services:
```
$ kubectl get services
```
To get minikube node IP:
```
$ minikube node list
```
or
```
$ minikube ip
```
or
```
$ minikube service list
```
To get service definition:
```
$ kubectl get service myapp-service -o yaml
```
To delete service:
```
$ kubectl delete service myapp-service
```

# General

To list all created Kubernetes objects:
```
kubectl get all
```