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


## 5. Code (Connection Troubleshooting & Verification

# --- THE ERROR SCENARIOS (What you saw when it failed) ---
# C:\Users>kubectl run my-pod --image=nginx
Unable to connect to the server: http2: client connection lost

# C:\Users>kubectl run my-pod --image=nginx
Unable to connect to the server: net/http: TLS handshake timeout

# --- THE DIAGNOSTIC COMMANDS ---

# 1. Check if the cluster is reachable
kubectl cluster-info

# 2. List all available contexts (Your Command)
kubectl config get-contexts

# 3. Check which context is currently active (Your Command)
kubectl config current-context

# 4. Manually force the switch to Minikube (Your Command)
kubectl config use-context minikube

# 5. Final check of the system state
kubectl get nodes
kubectl get pods -A