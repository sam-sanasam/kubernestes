### useful commands
```c
$ kubectl create -f deployment.yml
$ kubectl get deployment
$ kubectl apply -f deployment.yml
$ kubectl rollout status deployment/deployment.yml
$ kubectl rollout hisory deployment/deploymentyyml
$ kubectl rollout undo deployment/deployment.yml

```

First, we will try to differentiate between ReplicaSet and Deployment

A ReplicaSet ensures that a specified number of pod replicas are running at any given time.\
However, a Deployment is a higher-level concept that manages **ReplicaSets** and provides **declarative updates**\
to Pods along with a lot of other useful features.\
Therefore, use Deployments instead of
directly using ReplicaSets,\
unless we require custom update orchestration or don't require updates at all.

This actually means that you may never need to manipulate ReplicaSet objects: use a Deployment instead, and define your application in the spec section.

>>> deployment-definition.yml 
```sh
apiVersion: app/v1
kind: Deployment
metadata:
   name: webapp-deployment
   lables:
     app: webapp
     type: frontend
spec:
   template:
      metadata:
        name: webapp-pod
        labels:
          type: frontend
   spec:
      containers:
         - name: nginx
           image: nginx
           
   replicas: 3
   
   selectors:
      matchlabels:
         type: frontend
         
         
         
  ```
  
  To create the deployment:
 ```c
 $ kubectl create -f deployment-definition.yml
 
# to check the deployment

 $ kubectl get deployment  
 
# to check the pod
$ kubectl get pod

$ kubectl describe deployment/<name_of_the_deployment>
 
 
 ### Type of deployment update
 There are two types of update in deployments:\
 1) RollingUpdate ( default)
 2) Recreate 

In rollingupdate, the running Pod will not destroyed at a time, Instead, the update will be done one pod down and one up at a time. this makes no disturbance to the users.

In recreate, all the pod will take down at a time and replication pod will bring up . This create a waitng peroid aor gap in the service which may lead to disruption to the user experience.
 
    
