### Serives in Kubernetes
Service is the object in the kubernetes which listen from th euser and send the request to respective pod for completing the task.\
There are 3 types of services:
1. nodePort
2. clusterIP
3. loadBalancer

**nodePort** listen the user at port at the node and transfer the reqest to the targer pod.
![image](https://user-images.githubusercontent.com/68118215/116071544-a7d05980-a6ab-11eb-8197-bc416992cd44.png)

As we can see in the above image, the user send the request to the nodeport. The service listen the request at port of Node ( Nodeport: 30000-32727 default range).
And the request send to the target of the pod.

```sh
apiVersion : v1
kind: Service
metadata:
   name: nodeport-service
spec:
  type: nodePort
  ports:
    - targetPod: 80   # port on the target pod
      port: 80        # port on the service
      nodePort: 30008 
  selector:           # this is used to link to the pod. "Type: frontend " is the lebels defined in the pod definition
    type: frontend    
      
      
   ```


### CLusterIP

```sh
apiVersion: vi
kind: Service
metadata: 
  name: webapp-clusterIp
spec:
  type: ClusterIP
  ports:
    - targetPort: 80
      port: 80
selector:
   name: frontend
   
   ```
   
   
   
   
   ### LoadBalancer
   Below is the simple example for explaingnthe load balancer service in kubernetes.
   ![image](https://user-images.githubusercontent.com/68118215/116077098-b2dab800-a6b2-11eb-9224-14bf194a3443.png)
Here, if we use other services like nodeport and cluster Ip, it will give multiple url addresses to access the repective port which is not favourable for the user.
We we need to create a Vm in-inbetweenthe User and the Kubernetes cluster and configure it to act like a load balancer. However this is very tedius job.
So we create a service called **Loadbalancer** in the kubernetes cluster to distribute the load .

```sh
apiVersion: v1
kind: Service
metadata:
 name: loadbalcer-service
spec:
  type: LoadBlancer
  ports:
    - tagetPort: 80
      port: 80
 selector:
   name: frontend
   
   
```
