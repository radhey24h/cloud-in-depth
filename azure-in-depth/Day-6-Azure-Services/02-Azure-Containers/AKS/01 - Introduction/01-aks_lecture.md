
# Lecture: Azure Kubernetes Service (AKS) Architecture and Key Components

## Part 1: Introduction to AKS and Kubernetes Architecture

Welcome everyone to today's session on Azure Kubernetes Service (AKS) architecture. Today, we'll dive deep into how AKS works, focusing on the control plane, worker nodes, and core Kubernetes components like Pods, Deployments, Services, and more. We'll use a real-time use case to help solidify these concepts. So, let's get started!

## Part 2: AKS Control Plane and Worker Node

### 2.1 AKS Control Plane

When we talk about Kubernetes architecture, the core of it involves the **control plane** and **worker nodes**. Let's start with the control plane, which is the brain of our Kubernetes cluster. 
In AKS, Azure manages the control plane for us. This includes critical components like the API Server, `etcd`, Controller Manager, and the Scheduler.

The control plane in AKS is responsible for managing the Kubernetes cluster, orchestrating workloads, and maintaining the desired state of the cluster. In AKS, the control plane is managed by Azure, abstracting away much of the complexity of setting up and maintaining the Kubernetes master components. Here are the key components and their roles:

- **API Server:** 
  1) Acts as the front-end for the Kubernetes control plane.
  2) Exposes the Kubernetes API, which is used by all other components to interact with the cluster.
  3) Receives REST commands (kubectl commands) to create, update, delete, and query Kubernetes resources (pods, services, deployments, etc.).
  4) The API server performs validation and processing of these requests, interacts with the etcd database to fetch or store the state of cluster resources, and returns the result to the client.

The API Server is the entry point for all the management commands. For example, when you deploy an application using `kubectl`, the API server is the one that processes this request.

  *"Imagine you want to deploy a new version of your application. You send the request using `kubectl apply`, and the API Server receives this request, validates it, and starts the deployment process."*




- **etcd:** 
  1) A highly available key-value store that stores all cluster data.
  2) Maintains the desired state, configuration, and status of all resources in the cluster (e.g., nodes, pods, services).
  3) All changes made to the cluster through the API server are persisted in etcd.
  4) It ensures that the cluster can recover and restore state after failures.
  
  This is the key-value store that holds the state of the entire cluster. Whenever a new deployment is made or a change occurs, `etcd` is updated with the new state of the cluster.

  *"Think of `etcd` like the memory of our cluster. It knows what should be running, where it should be running, and the current state of the cluster."*

  

- **Controller Manager:** This component runs various controllers to ensure the cluster's desired state is maintained. For example, if you want three instances of a web server running, the Replication Controller ensures that if one instance crashes, it automatically starts a new one to maintain the desired count.

  1) Runs various controllers that ensure the cluster is in the desired state.
  2) Node Controller: Monitors the health of worker nodes and handles node failures.
  3) Replication Controller: Ensures that the desired number of pod replicas are running.
  4) Service Account and Token Controllers: Manages service accounts and API tokens for accessing the API server.
  5) Each controller listens to the changes in etcd, and if any desired state deviates from the current state, they take corrective actions (e.g., restarting pods, rescheduling workloads).

  *"If one of your web server instances crashes, the Controller Manager steps in, saying, 'Hey, we're supposed to have three instances here,' and it starts a new one."*

- **Scheduler:** The Scheduler is responsible for assigning new pods to nodes. It watches for unscheduled pods and determines the best nodes to run them on, based on resource requirements.

  *"When you deploy your web server, the Scheduler decides on which worker nodes these servers should run, ensuring they have enough CPU, memory, and other resources."*

  1) Responsible for placing pods on the appropriate nodes based on resource requirements, constraints, and available resources.
  2) It listens to the API server for unscheduled pods, then assigns them to nodes based on factors like resource utilization, affinity/anti-affinity rules, and taints and tolerations.
  3) The scheduler optimizes for load balancing and efficient resource utilization across the cluster.

### 2.2 Worker Nodes

Now, let's move on to the **worker nodes**. These are the nodes where your application pods actually run. When you create an AKS cluster, you define the number and size of worker nodes. Each worker node has key components:

- **Kubelet:** This agent runs on each worker node and communicates with the API Server to receive instructions on what pods should run on this node.

  *"The Kubelet is like the caretaker of each node. When the Scheduler assigns a pod to a node, the Kubelet makes sure that the pod is created and running correctly."*

  1) An agent that runs on each worker node.
  2) Communicates with the control plane to receive pod specifications (PodSpecs) and ensure the containers described in those pods are running.
  3) Monitors the running containers and reports their status back to the API server.
  4) Kubelet uses container runtimes (e.g., containerd, Docker) to manage the lifecycle of containers on the node.

- **Container Runtime:** This is the component that runs containers on the node. AKS supports several runtimes like Docker or containerd.

  *"If the Kubelet is the caretaker, the container runtime is the worker that does the heavy lifting—pulling images and starting containers."*
  
  1) The software responsible for running containers on the node.
  2) Common runtimes include Docker and containerd.
  3) It pulls the required container images from container registries (e.g., Azure Container Registry, Docker Hub) and starts/stops containers based on the instructions from the kubelet.

- **Kube-proxy:** This component manages network rules on each node. It routes traffic to the appropriate pods, ensuring that communication within the cluster and with the outside world is smooth.

  *"When the frontend of your application tries to talk to the backend, `kube-proxy` ensures the network traffic is correctly routed to the appropriate pod, even if the pods are running on different nodes."*

  1) Runs on each worker node and manages the network routing for services in the cluster.
  2) Maintains the network rules that allow network communication to and from pods.
  3) Facilitates communication between services by load-balancing network traffic to the appropriate pods based on their IP addresses and ports.

## Part 3: Real-Time Use Case - Deploying a Scalable Web Application on AKS

Let's apply these concepts with a real-time use case. Imagine you want to deploy a scalable web application on AKS. This application consists of a React frontend and a Node.js backend.

### Step 1: Deploying the Application

- You define the desired state of your application using YAML files. These include the frontend and backend deployments.
  
  *"You create two YAML files: `frontend-deployment.yaml` and `backend-deployment.yaml`. These files define the number of replicas, container images, and resource requirements."*

- You then apply these files using `kubectl apply`. This command goes to the API Server, which updates the cluster state in `etcd`.

### Step 2: Scheduling and Pod Creation

- The Scheduler identifies the best worker nodes to run these pods based on resource availability.
  
  *"For example, it might place two frontend pods on Node 1 and one backend pod on Node 2, ensuring that the nodes have enough resources."*

- The Kubelet on each node then pulls the container images and starts the containers as defined in the deployment.

  *"The Kubelet on Node 1 pulls the React frontend image and starts two instances of it, while the Kubelet on Node 2 pulls and starts the Node.js backend."*

### Step 3: Exposing the Application

- To expose the application, you create **Services**. A Service exposes your application's pods within the cluster and optionally to the outside world.

  *"You create a `Service` for the backend with type `ClusterIP`, allowing the frontend pods to communicate with the backend. You might also create a `LoadBalancer` service to expose the frontend to the internet."*

### Step 4: Routing with Ingress

- To manage external access, you create an **Ingress** resource, which provides URL-based routing.

  *"For example, you can route traffic from `myapp.com/api` to the backend service and `myapp.com` to the frontend service."*

## Part 4: Kubernetes Components Overview

### 4.1 Pods
- **Definition:** The smallest unit in Kubernetes, representing a single instance of a running process.
  
  *"In our use case, each instance of the frontend or backend is a Pod."*

  Use Case: Pods are used to run your application containers. For example, a Pod may contain a web server and a sidecar container that logs the server's activities.

### 4.2 Deployments
- **Definition:** Manages a set of identical Pods and ensures the desired number of replicas.
  
  *"You use a Deployment to specify that you want three replicas of the frontend. If one crashes, the Deployment ensures a new one is started."*

Use Case: You use Deployments to ensure a specified number of replicas of your application are running. They automatically replace pods if they crash or when you update the deployment.

### 4.3 Services
- **Definition:** Expose your application to other applications or the internet.
  
  *"A Service provides a stable IP and DNS name for your backend pods, so the frontend can always reach them."*

Types:
- **ClusterIP:**: Exposes the service on an internal IP within the cluster.
- **NodePort:**: Exposes the service on each Node's IP at a static port.
- **LoadBalancer:**: Exposes the service using a cloud provider's load balancer.

Use Case: Services are used to expose your application's pods to other services, the internet, or other pods.

### 4.4 ReplicaSets
- **Definition:** Ensure that a specified number of Pod replicas are running at any time.
  
  *"ReplicaSets are managed by Deployments in most cases to maintain the desired count of pods."*
Use Case: Although you usually interact with ReplicaSets through Deployments, they can be used directly to maintain a fixed number of pod replicas.

### 4.5 Ingress Controller
- **Definition:** Provides external access to services in the cluster.
  
  *"The Ingress Controller manages the traffic routing, ensuring requests to `myapp.com` are correctly routed to the frontend and backend services."*

Use Case: Ingress and Ingress Controllers are used to expose HTTP and HTTPS routes to services within the cluster, allowing for URL-based routing and SSL termination.

### 4.6 ConfigMap
- **Definition:** An API object used to store non-confidential configuration data in key-value pairs.
- **Details:** Decouples configuration artifacts from image content to keep containerized applications portable.

Use Case: Use ConfigMaps to pass environment variables, command-line arguments, or configuration files to your application.
### 4.7 Secret
- **Definition:** Similar to ConfigMaps, but intended for storing sensitive information like passwords, OAuth tokens, and SSH keys.
- **Details:** Secrets are encoded to protect them from accidental exposure, though not encrypted by default.

Use Case: Use Secrets to provide sensitive information securely to your application containers.
### 4.8 StatefulSet
- **Definition:** Manages the deployment and scaling of a set of Pods, providing guarantees about the ordering and uniqueness of these Pods.
- **Details:** Maintains a sticky identity for each pod. It is used for stateful applications like databases.

Use Case: Use StatefulSets for applications that require stable, persistent storage, unique network identities, or ordered deployment and scaling.
### 4.9 DaemonSet
- **Definition:** Ensures that a particular pod runs on all or specific nodes in the cluster.
- **Details:** Used for background tasks like logging, monitoring, or networking.

Use Case: Use DaemonSets to deploy network plugins, log collection agents, or monitoring agents on every node.

### 4.10 Job and CronJob
#### Job:
- **Definition:**  Creates one or more pods and ensures they run to completion.

Use Case: Use Jobs for batch processing tasks like backups or data processing.

#### CronJob:
- **Definition:**  Schedules Jobs to run periodically at specified times.

Use Case: Use CronJobs for periodic tasks like scheduled reports or database cleanups.

### 4.11 PersistentVolume (PV) and PersistentVolumeClaim (PVC)
PersistentVolume (PV):
- **Definition:**  A piece of storage in the cluster that has been provisioned by an administrator.

Use Case: PVs provide storage resources that can be used by the pods.

### 4.12 PersistentVolumeClaim (PVC):
- **Definition:**  A request for storage by a user, specifying size and access modes.

Use Case: Use PVCs to consume storage resources from PVs for your pods.
### 4.13 Namespace
- **Definition:**  A way to divide cluster resources between multiple users or teams.
- **Details:**  Provides a scope for names, enabling resource isolation and organization within a single cluster.

Use Case: Use Namespaces to create logical partitions within the cluster for different environments (e.g., dev, test, prod) or teams.

### 4.14 Horizontal Pod Autoscaler (HPA)
- **Definition:**  Automatically scales the number of pod replicas based on observed CPU utilization or other metrics.
- **Details:**  Monitors the resource usage of pods and adjusts the number of replicas to match the demand.

Use Case: Use HPA to automatically scale your application pods up or down to handle varying loads.

## Part 5: Scaling and Auto-healing

AKS and Kubernetes also handle scaling and healing:

- **Scaling:** You can scale the number of pods or nodes in your cluster to handle more traffic.
  
  *"If your web app suddenly gets more traffic, you can increase the number of frontend pods from 3 to 10 using the `kubectl scale` command."*

- **Auto-healing:** If a node fails or a pod crashes, the control plane detects the failure and schedules the creation of new pods.

  *"If Node 1 crashes, the control plane ensures that the pods running on Node 1 are rescheduled on another available node."*

## Part 6: Summary and Q&A

To sum up, the AKS architecture involves a managed control plane that orchestrates the deployment, scaling, and maintenance of your applications. The worker nodes run your application containers, with the control plane ensuring everything is running smoothly according to the desired state.

- **Control Plane:** The brain of the cluster, managing deployments, scheduling, and health monitoring.
- **Worker Nodes:** Run the application pods and handle networking and container lifecycle.
- **Core Components:** Pods, Deployments, Services, Ingress, and others work together to manage application lifecycle and scaling.

Now, let's open the floor for any questions you may have about AKS architecture, control plane, worker nodes, or Kubernetes components!
