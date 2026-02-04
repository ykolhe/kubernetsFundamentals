# Chapter 00: Environment Setup & Cluster Initialization

## 1. Definition
Before managing Kubernetes resources, you must establish a local cluster environment. This involves starting a Container Engine (Docker Desktop) and a Cluster Orchestrator (Minikube). Minikube creates a virtual Kubernetes node inside a Docker container.

## 2. Real-World Example
Think of this as setting up a **Digital Playground**. 
* **Docker Desktop** is the physical ground/park where everything sits.
* **Minikube** is the supervisor who sets up the equipment.
* **Kubectl** is you, giving instructions on which equipment to use. 
If the park (Docker) is closed, the supervisor (Minikube) cannot set anything up.

## 3. Rules
* **Mandatory Prerequisite:** Docker Desktop **MUST** be launched and running (indicated by the green status icon) before you execute any Minikube commands.
* **Driver Consistency:** On Windows, Minikube typically uses the `docker` driver. If Docker is not running, Minikube will fail with `PROVIDER_DOCKER_NOT_RUNNING`.
* **Resource Check:** Ensure Docker Desktop has enough RAM (at least 4GB recommended) to prevent the cluster from crashing.

## 4. Step-by-Step Initialization Code

# Step 1: Open Docker Desktop manually from the Start Menu
# (Wait for the green whale icon in the system tray)

# Step 2: Verify Docker is alive in your terminal
docker ps

# Step 3: Start the Minikube cluster
minikube start --driver=docker

# Step 4: Verify the cluster status
minikube status

# Step 5: Confirm kubectl is connected to Minikube
kubectl get nodes

## 5. Expected Output Box
+----------------------------------------------------------------------+
| $ docker ps                                                          |
| CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS         |
| (If Docker is running, this command will return an empty list or IDs)|
|                                                                      |
| $ minikube start                                                     |
| * minikube v1.37.0 on Windows 11                                     |
| * Using the docker driver based on user configuration                |
| * Starting control plane node minikube in cluster minikube           |
| * Done! kubectl is now configured to use "minikube" cluster          |
|                                                                      |
| $ kubectl get nodes                                                  |
| NAME       STATUS   ROLES           AGE   VERSION                    |
| minikube   Ready    control-plane   1m    v1.31.0                    |
+----------------------------------------------------------------------+