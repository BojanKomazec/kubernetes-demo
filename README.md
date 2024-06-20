# kubernetes-demo
Kubernetes demo

First run `minikube start` so `kubectl` gets configured to talk to minikube's cluster.

# kubectl tool

* To make typing faster: `alias k='kubectl'`
* A shorter equivalent for `--all-namespaces` is `-A`

## Namespaces

To get all namespaces:
```
kubectl get ns
kubectl get namespace
kubectl get namespaces
```

## Pods

To get all pods in the default namespace:
```
kubectl get pods
```
To get pods in all namespaces:
```
kubectl get pods --all-namespaces
```
To get a list of pods in a specific namespace:
```
kubectl get pods -n namespace_name
```
To get a details about specific pod we also need to specify its namespace:
```
kubectl describe pod pod_name -n namespace_name
```

## Replica Sets

To list all replica sets:
```
kubectl get rs
kubectl get rs -o wide
```

## Deployments

To create a deployment (if not created) or update it (configure it - if it's already been created):
```
kubectl apply -f my-deployment.yaml
```
To list all deployments in the default namespace:
```
kubectl get deploy
kubectl get deployment
kubectl get deployments

kubectl get deploy -o wide
```
To list all deployments in all namespaces:
```
kubectl get deploy -o wide --all-namespaces
```
To get details about particular deployment we also need to specify its namespace:
```
kubectl describe deployment my-deployment -n namespace_name
```
To get affinities for all deployments in all namespaces:
```
kubectl get deploy  -o custom-columns=NAME:".metadata.name",AFFINITIES:".spec.template.spec.affinity" --all-namespaces
```
To scale deployment up or down we can set the number of replicas:
```
kubectl scale deployment deployment_name --replicas number_of_replicas
```
To delete deployment:
```
kubectl delete deployment deployment_name
```

## Nodes

To list all nodes in the cluster:
```
kubectl get node
kubectl get nodes
kubectl get nodes -o wide
```
To get details about specific node:
```
kubectl describe node node_name
```

## All Kubernetes objects

To get information about all Kubernetes objects in the defuault namespace:
```
kubectl get all
kubectl get all -o wide
```
To get information about all Kubernetes objects in all namespaces:
```
kubectl get all -o wide --all-namespaces
```
