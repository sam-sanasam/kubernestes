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
