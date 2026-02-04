# Definition
A **NodePort** service is a networking object that exposes a Pod to external traffic. It maps a port on every Node (the NodePort) to a port on the Pod (the TargetPort). This allows you to access the application using the IP address of any Node in the cluster plus the assigned port number.

# Real-World Example
Imagine an apartment building (the Node) with a main switchboard (the NodePort). Even though the resident (the Pod) is in Room 80 (TargetPort), the delivery person just needs to dial extension 30007 on the building's front door to be routed directly to that room.

# Rules
1. **Port Range**: By default, NodePorts must be within the range **30000-32767**.
2. **Selector**: The service uses "Labels" to find which Pods it should send traffic to.
3. **Connectivity**: Once created, the service stays active even if the underlying Pods are deleted and recreated.

# Code
# 1. First, ensure a Pod is running with a label (we use 'run=nginx')
kubectl run nginx --image=nginx --port=80

# 2. Create a NodePort service to expose the 'nginx' pod
# Syntax: kubectl expose pod <POD_NAME> --type=NodePort --port=<INTERNAL_PORT>
kubectl expose pod nginx --type=NodePort --port=80 --name=nginx-service

# 3. Check the service to find the assigned NodePort
kubectl get svc nginx-service

# 4. (Minikube specific) Get the URL to browse the service
minikube service nginx-service --url

# 5. Cleanup: Delete the service and the pod
# Syntax: kubectl delete service <SERVICE_NAME>
kubectl delete svc nginx-service

kubectl delete pod nginx

# Expected Output Box
----------------------------------------------------------------------
| > kubectl expose pod nginx --type=NodePort --port=80               |
| service/nginx-service exposed                                      |
|                                                                    |
| > kubectl get svc nginx-service                                    |
| NAME            TYPE       CLUSTER-IP      PORT(S)        AGE      |
| nginx-service   NodePort   10.105.20.144   80:31245/TCP   10s      |
|                                                                    |
| > kubectl delete svc nginx-service                                 |
| service "nginx-service" deleted                                    |
----------------------------------------------------------------------

# Command Breakdown for "Specific" Targeting
- kubectl describe svc nginx-service     # See which Pods are connected to this service
- kubectl delete svc nginx-service       # Deletes the specific service named 'nginx-service'