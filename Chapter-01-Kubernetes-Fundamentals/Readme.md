# Chapter 01: Kubernetes Fundamentals

## 1. Definition
Kubernetes (K8s) is an open-source container orchestration platform. It automates the deployment, scaling, and management of containerized applications. At its core, it consists of a **Control Plane** (the brain) and **Worker Nodes** (the muscle) that run your applications in units called **Pods**.

## 2. Real-World Example
Think of Kubernetes as a **Ship Captain**. The containers are the cargo boxes. The Captain (Control Plane) decides where each box (Container) should go on the ship (Node) to keep the boat balanced and ensures that if a box falls overboard, a new one is immediately brought out to replace it.

## 3. Rules
* **Immutability:** You generally don't "repair" a running Pod; you replace it.
* **Declarative vs Imperative:** While we are learning Imperative (direct commands), K8s internally always works toward a "Desired State."
* **Smallest Unit:** The Pod is the smallest deployable unit in K8s, not the Container.
* **Connectivity:** Every Pod gets its own unique IP address within the cluster.

## 4. Code (Essential Discovery Commands)

# 1. Check cluster information (Master and Services)
kubectl cluster-info

# 2. List all nodes in the cluster to check health
kubectl get nodes

# 3. List all namespaces (logical partitions)
kubectl get namespaces

# 4. List all pods across the entire cluster
kubectl get pods -A

# 5. Get detailed information about a specific node
kubectl describe node <node-name>

## 5. Expected Output Box
+----------------------------------------------------------------------+
| $ kubectl get nodes                                                  |
| NAME             STATUS   ROLES           AGE   VERSION              |
| control-plane    Ready    control-plane   10d   v1.31.0              |
| worker-node-01   Ready    worker          10d   v1.31.0              |
|                                                                      |
| $ kubectl cluster-info                                               |
| Kubernetes control plane is running at https://127.0.0.1:6443        |
| CoreDNS is running at https://127.0.0.1:6443/api/v1/proxy/nodes...   |
+----------------------------------------------------------------------+