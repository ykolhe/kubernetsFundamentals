# Definition
A **ReplicaSet** is a neighbor to the Pod. Its primary purpose is to maintain a stable set of replica Pods running at any given time. It is often used to guarantee the availability of a specified number of identical Pods. While usually managed by Deployments, understanding them imperatively is key to mastering K8s scaling.

# Real-World Example
Think of a ReplicaSet like a **Lifeguard** at a pool. If the "rule" is to have 3 swimmers (Pods) in the water, and one swimmer leaves or gets tired (crashes), the Lifeguard immediately blows the whistle and sends a new swimmer in to maintain the count of 3.

# Rules
1. **Selection**: It uses a `selector` to identify which Pods it owns. 
2. **Equality**: If you manually delete a Pod owned by a ReplicaSet, the ReplicaSet will instantly recreate it.
3. **Labels**: It identifies Pods by their labels. If you change a Pod's label, the ReplicaSet will "lose" it and create a replacement.
4. **Scale**: You can scale a ReplicaSet up or down instantly.

# Code

## 1. Scaling a Resource (Imperative)
# If you have a ReplicaSet named 'my-repset', scale it to 5 replicas
kubectl scale rs my-repset --replicas=5

## 2. Inspecting the ReplicaSet
kubectl get rs                                      # List all ReplicaSets
kubectl describe rs my-repset                       # See why replicas are/aren't starting
kubectl get pods -l app=my-app                      # View all pods managed by the set label

## 3. Connecting/Interacting with Replicas
# To talk to a SPECIFIC pod in a ReplicaSet, find the name first:
kubectl get pods
# Then use the name of one of the generated pods:
kubectl exec -it <POD_NAME_FROM_GET_PODS> -- /bin/sh
kubectl logs <POD_NAME_FROM_GET_PODS>

## 4. Testing Self-Healing (The "Killer" Test)
# Delete one specific pod and watch the ReplicaSet recreate it immediately
kubectl delete pod <POD_NAME_FROM_GET_PODS>
kubectl get pods -w                                 # Watch the replacement happen

## 5. Deleting the ReplicaSet
# This will delete the ReplicaSet and all the Pods it manages
kubectl delete rs my-repset

# Expected Output Box
----------------------------------------------------------------------
| > kubectl scale rs my-repset --replicas=3                          |
| replicaset.apps/my-repset scaled                                   |
|                                                                    |
| > kubectl get pods                                                 |
| NAME             READY   STATUS    RESTARTS   AGE                  |
| my-repset-abc1   1/1     Running   0          10s                  |
| my-repset-xyz2   1/1     Running   0          10s                  |
| my-repset-lmn3   1/1     Running   0          10s                  |
|                                                                    |
| > kubectl delete pod my-repset-abc1                                |
| pod "my-repset-abc1" deleted                                       |
|                                                                    |
| > kubectl get pods                                                 |
| NAME             READY   STATUS    RESTARTS   AGE                  |
| my-repset-xyz2   1/1     Running   0          15s                  |
| my-repset-lmn3   1/1     Running   0          15s                  |
| my-repset-new4   0/1     Pending   0          1s                   |
----------------------------------------------------------------------