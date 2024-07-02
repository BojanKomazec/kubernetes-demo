Components:
- Voting app
- Redis
- Worker app
- Postgres
- Result app

Plan of actions:
* write definition files for deployments for each component
* write definition files for services for each component apart from the Worker app (in order to expose them internally/externally)
* create Kubernetes objects defined in definition files
  * Verify that the default namespace is empty:
    ```
    $ kubectl get all
    No resources found in default namespace.
    ```
  * If it's not empty, list all objects in there and delete all objects for each object category:
    ```
    $ kubectl delete service --all
    $ kubectl delete deployment --all
    $ kubectl delete replicaset --all
    $ kubectl delete pod --all
    ```
  * create deployments and services:
    ```
    $ kubectl create -f ./kodecloud-voting-app/voting-app-via-deployments/deployment/voting-app-deployment.yaml
    $ kubectl create -f ./kodecloud-voting-app/voting-app-via-deployments/service/voting-app-service.yaml
    $ kubectl create -f ./kodecloud-voting-app/voting-app-via-deployments/deployment/redis-deployment.yaml
    $ kubectl create -f ./kodecloud-voting-app/voting-app-via-deployments/service/redis-service.yaml
    $ kubectl create -f ./kodecloud-voting-app/voting-app-via-deployments/deployment/postgres-deployment.yaml
    $ kubectl create -f ./kodecloud-voting-app/voting-app-via-deployments/service/postgres-service.yaml
    $ kubectl create -f ./kodecloud-voting-app/voting-app-via-deployments/deployment/worker-app-deployment.yaml
    $ kubectl create -f ./kodecloud-voting-app/voting-app-via-deployments/deployment/result-app-deployment.yaml
    $ kubectl create -f ./kodecloud-voting-app/voting-app-via-deployments/service/result-app-service.yaml
    ```
  * check if pod and service are created; check if service is forwarding request to the pod (use curl or browser)
    ```
    $ kubectl get pod,svc
    $ minikube service voting-service --url
    http://192.168.59.100:30004
    $ curl http://192.168.59.100:30004
    $ minikube service result-service --url
    http://192.168.59.100:30005
    $ curl http://192.168.59.100:30005
    ```
  * Try to scale deployment from original 1 to 3 replicas:
    ```
    $ kubectl scale deployment voting-app-deploy --replicas=3
    deployment.apps/voting-app-deploy scaled
    $ kubectl get deploy
    NAME                READY   UP-TO-DATE   AVAILABLE   AGE
    postgres-deploy     1/1     1            1           18m
    redis-deploy        1/1     1            1           19m
    result-app-deploy   1/1     1            1           17m
    voting-app-deploy   3/3     3            3           21m
    worker-app-deploy   1/1     1            1           17m
    ```
  * Verify that the Voting app web page is served by different pods by going to browser and refreshing the http://192.168.59.100:30004 page.
    Pod names can be checked via:
    ```
    $ kubectl get pod
    NAME                                 READY   STATUS    RESTARTS   AGE
    postgres-deploy-5b59bf5dff-k6mq2     1/1     Running   0          20m
    redis-deploy-58bdbddb55-bgjr7        1/1     Running   0          21m
    result-app-deploy-cdd6d7689-4z7hn    1/1     Running   0          19m
    voting-app-deploy-86db9b874b-8m49p   1/1     Running   0          2m53s
    voting-app-deploy-86db9b874b-kzxzj   1/1     Running   0          23m
    voting-app-deploy-86db9b874b-t9dvq   1/1     Running   0          2m53s
    worker-app-deploy-544dd746f4-6npdl   1/1     Running   0          19m
    ```


## Deploying Voting App on AWS EKS

Use all deployments and services from ./kodecloud-voting-app/voting-app-via-deployments/deployment/ and ./kodecloud-voting-app/voting-app-via-deployments/service/ apart from voting-app-service and result-app-service which should be provisioned via configurations in ./kodecloud-voting-app/voting-app-via-deployments/service/aws/.

```
$ kubectl create -f ./kodecloud-voting-app/voting-app-via-deployments/deployment/voting-app-deployment.yaml
deployment.apps/voting-app-deploy created

$ kubectl create -f ./kodecloud-voting-app/voting-app-via-deployments/service/aws/voting-app-service-lb.yaml
service/voting-service created

$ kubectl create -f ./kodecloud-voting-app/voting-app-via-deployments/deployment/redis-deployment.yaml
deployment.apps/redis-deploy created

$ kubectl create -f ./kodecloud-voting-app/voting-app-via-deployments/service/redis-service.yaml
service/redis created

$ kubectl create -f ./kodecloud-voting-app/voting-app-via-deployments/deployment/postgres-deployment.yaml
deployment.apps/postgres-deploy created

$ kubectl create -f ./kodecloud-voting-app/voting-app-via-deployments/service/postgres-service.yaml
service/db created

$ kubectl create -f ./kodecloud-voting-app/voting-app-via-deployments/deployment/worker-app-deployment.yaml
deployment.apps/worker-app-deploy created

$ kubectl create -f ./kodecloud-voting-app/voting-app-via-deployments/deployment/result-app-deployment.yaml
deployment.apps/result-app-deploy created

$ kubectl create -f ./kodecloud-voting-app/voting-app-via-deployments/service/aws/result-app-service-lb.yaml
service/result-service created
```