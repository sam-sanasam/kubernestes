 ### What is Kubernetes replication?
Before we dive into the details on how you would do replication, let’s talk about why we use replication in the kubernetes cluster.\
We would want to replicate your containers for several reasons, including:\
**Reliability**: By having multiple versions of an application, you prevent problems if one or more fails.  This is particularly true if the system replaces any containers that fail.\
**Load balancing**: Having multiple versions of a container enables you to easily send traffic to different instances to prevent overloading of a single instance or node. This is something that Kubernetes does out of the box, making it extremely convenient.\
**Scaling**: When load does become too much for the number of existing instances, Kubernetes enables you to easily scale up your application, adding additional instances as needed.


### Kubernetes Replication Controller
The Replication Controller is the original form of replication in Kubernetes.  It’s being replaced by **Replica Sets**, but it’s still in wide use, so it’s worth understanding what it is and how it works. A Replication Controller is a structure that enables you to easily create multiple pods, then make sure that that number of pods always exists. If a pod does crash, the Replication Controller replaces it.  A Kubernetes controller such as the Replication Controller also provide other benefits, such as the ability to scale the number of pods, and to update or delete multiple pods with a single command. You can create a Replication Controller with an imperative command, or declaratively, from a file


```c
apiVersion: v1
kind: ReplicationController
metadata:
   name: rc-controller
   labels:
    tier: frontend

spec:
  template:       # template of the pod. with this pod specification, replication controller will create 3 replicas as it mention replicas=3
     metadata:
       name: webapp-pod
       labels:
          type: frontend
     spec:
       containers:
         - name: webapp
           image: nginx

  replicas: 3   # no. of pod need to bring up

```

### Kubernetes Replica Sets
It can be tricky to compare a replica controller vs replica set (ReplicalSet), because the latter is a sort of a hybrid. They are in some ways more powerful than ReplicationControllers, and in others they are less powerful. ReplicaSets are declared in essentially the same way as ReplicationControllers, except that they have more options for the selector


```c
apiVersion: app/v1
kind: ReplicaSet
metadata:
   name: rc-controller
   labels:
    tier: frontend

spec:
  template:
     metadata:
       name: webapp-pod
       labels:
          type: frontend
     spec:
       containers:
         - name: webapp
           image: nginx

  replicas: 3
  selector:
    matchLabels:
      type: frontend
      
  ```
  #### Note:\
  The major difference between the ReplicatinCOntroller and ReplicaSet is that **The Selector option followed by matchLables** in \
  the replicaset is not valiable in the Replication controller.
  
