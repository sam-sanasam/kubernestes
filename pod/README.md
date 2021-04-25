### To create a pod from the command line, use the command:

Create an NGINX Pod
```c
kubectl run nginx --image=nginx
```


As of version 1.18, kubectl run (without any arguments such as --generator) will create a pod instead of a deployment.



To create a deployment using imperative command, use kubectl create:
```c
kubectl create deployment nginx --image=nginx
```


## Command apiVersion for kubernetes objects

| kind  |   apiVersion |
|-----  |--------------|
|pod    |  v1          |
|service| v1           |
|replicaset| app/v1    |
|deployment|  app/v1  |


## Working with YAML file

NOte: Indentation is the key of YAML file

In kubernetes, normally the below file structure is followed in all the object creates in kubernetes

```c
apiVersion:
kink:
metadata:
spec:

```


Lets now populate the yaml file > pod-definition.yml

>>>>> pod-definition.yml <<<<<

```c
---
 apiVersion: v1
 kind: Pod
 metadata:
   name: myapp
 spec:
   containers:
    - name: myapp-pod
      iamge: nginx
  ```
  
  To run the pod, use the below command:
 ```c
 $kubectl create -f pod-definition.yml 
 ```
 -f flag = passing the file
