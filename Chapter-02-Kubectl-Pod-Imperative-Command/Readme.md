# Definition
Imperative commands allow you to manage the lifecycle of a specific unit of work (a Pod) directly from the command line. This involves creating the resource, inspecting its internal state, and eventually destroying it.

# Real-World Example
Think of a Pod like a temporary "Service Badge." You issue a badge to a specific person (Create), check their access details (Describe), and once the job is done, you revoke and shred the badge (Delete).

# Rules
1. **Naming**: You must provide a unique name for the pod (e.g., `nginx`).
2. **Targeting**: Most commands require you to specify the resource type (`pod`) followed by that specific name.
3. **Cleanup**: Always delete temporary pods to save system resources on your Minikube node.

# Code
# 1. Create a pod with a specific name
# Syntax: kubectl run <YOUR_POD_NAME> --image <IMAGE_NAME>
kubectl run nginx --image nginx

# 2. Check the status of all pods
kubectl get pods

# 3. Get detailed info about the SPECIFIC pod you created
# Syntax: kubectl describe pod <NAME_OF_CREATED_POD>
kubectl describe pod nginx

# 4. Delete the SPECIFIC pod you created to clean up
# Syntax: kubectl delete pod <NAME_OF_CREATED_POD>
kubectl delete pod nginx

# Expected Output Box
----------------------------------------------------------------------
| > kubectl run nginx --image nginx                                  |
| pod/nginx created                                                  |
|                                                                    |
| > kubectl get pods                                                 |
| NAME    READY   STATUS    RESTARTS   AGE                           |
| nginx   1/1     Running   0          15s                           |
|                                                                    |
| > kubectl describe pod nginx                                       |
| Name:         nginx                                                |
| Status:       Running                                              |
| Events:       Started container nginx                              |
|                                                                    |
| > kubectl delete pod nginx                                         |
| pod "nginx" deleted                                                |
----------------------------------------------------------------------

# Learning Note
When you see <NAME_OF_CREATED_POD>, it means you must use the exact name 
you chose in Step 1. In your case, that name was "nginx".