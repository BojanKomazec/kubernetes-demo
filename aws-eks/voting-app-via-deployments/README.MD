Use all deployments and services from ./minikube/voting-app-via-deployments/deployment/ and ./minikube/voting-app-via-deployments/service/ apart from voting-app-service and result-app-service which should be provisioned via configurations in ./aws-eks/voting-app-via-deployments/service/.

```
$ kubectl create -f ./minikube/voting-app-via-deployments/deployment/voting-app-deployment.yaml
deployment.apps/voting-app-deploy created

$ kubectl create -f ./aws-eks/voting-app-via-deployments/service/voting-app-service-lb.yaml
service/voting-service created

$ kubectl create -f ./minikube/voting-app-via-deployments/deployment/redis-deployment.yaml
deployment.apps/redis-deploy created

$ kubectl create -f ./minikube/voting-app-via-deployments/service/redis-service.yaml
service/redis created

$ kubectl create -f ./minikube/voting-app-via-deployments/deployment/postgres-deployment.yaml
deployment.apps/postgres-deploy created

$ kubectl create -f ./minikube/voting-app-via-deployments/service/postgres-service.yaml
service/db created

$ kubectl create -f ./minikube/voting-app-via-deployments/deployment/worker-app-deployment.yaml
deployment.apps/worker-app-deploy created

$ kubectl create -f ./minikube/voting-app-via-deployments/deployment/result-app-deployment.yaml
deployment.apps/result-app-deploy created

$ kubectl create -f ./aws-eks/voting-app-via-deployments/service/result-app-service-lb.yaml
service/result-service created
```
