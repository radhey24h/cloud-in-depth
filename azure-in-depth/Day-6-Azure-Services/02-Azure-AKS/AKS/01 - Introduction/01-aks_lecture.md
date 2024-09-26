
# Lecture: Azure Kubernetes Service (AKS) Architecture and Key Components

## Part 1: Introduction to AKS and Kubernetes Architecture

Welcome everyone to today's session on Azure Kubernetes Service (AKS) architecture. Today, we'll dive deep into how AKS works, focusing on the control plane, worker nodes, and core Kubernetes components like Pods, Deployments, Services, and more. We'll use a real-time use case to help solidify these concepts. So, let's get started!

## Part 2: AKS Control Plane and Worker Node

### 2.1 AKS Control Plane

When we talk about Kubernetes architecture, the core of it involves the **control plane** and **worker nodes**. Let's start with the control plane, which is the brain of our Kubernetes cluster. In AKS, Azure manages the control plane for us. This includes critical components like the API Server, `etcd`, Controller Manager, and the Scheduler.

- **API Server:** The API Server is the entry point for all the management commands. For example, when you deploy an application using `kubectl`, the API server is the one that processes this request.

  *"Imagine you want to deploy a new version of your application. You send the request using `kubectl apply`, and the API Server receives this request, validates it, and starts the deployment process."*

- **etcd:** This is the key-value store that holds the state of the entire cluster. Whenever a new deployment is made or a change occurs, `etcd` is updated with the new state of the cluster.

  *"Think of `etcd` like the memory of our cluster. It knows what should be running, where it should be running, and the current state of the cluster."*

- **Controller Manager:** This component runs various controllers to ensure the cluster's desired state is maintained. For example, if you want three instances of a web server running, the Replication Controller ensures that if one instance crashes, it automatically starts a new one to maintain the desired count.

  *"If one of your web server instances crashes, the Controller Manager steps in, saying, 'Hey, we're supposed to have three instances here,' and it starts a new one."*

- **Scheduler:** The Scheduler is responsible for assigning new pods to nodes. It watches for unscheduled pods and determines the best nodes to run them on, based on resource requirements.

  *"When you deploy your web server, the Scheduler decides on which worker nodes these servers should run, ensuring they have enough CPU, memory, and other resources."*

### 2.2 Worker Nodes

Now, let's move on to the **worker nodes**. These are the nodes where your application pods actually run. When you create an AKS cluster, you define the number and size of worker nodes. Each worker node has key components:

- **Kubelet:** This agent runs on each worker node and communicates with the API Server to receive instructions on what pods should run on this node.

  *"The Kubelet is like the caretaker of each node. When the Scheduler assigns a pod to a node, the Kubelet makes sure that the pod is created and running correctly."*

- **Container Runtime:** This is the component that runs containers on the node. AKS supports several runtimes like Docker or containerd.

  *"If the Kubelet is the caretaker, the container runtime is the worker that does the heavy lifting—pulling images and starting containers."*

- **Kube-proxy:** This component manages network rules on each node. It routes traffic to the appropriate pods, ensuring that communication within the cluster and with the outside world is smooth.

  *"When the frontend of your application tries to talk to the backend, `kube-proxy` ensures the network traffic is correctly routed to the appropriate pod, even if the pods are running on different nodes."*

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

### 4.2 Deployments
- **Definition:** Manages a set of identical Pods and ensures the desired number of replicas.
  
  *"You use a Deployment to specify that you want three replicas of the frontend. If one crashes, the Deployment ensures a new one is started."*

### 4.3 Services
- **Definition:** Expose your application to other applications or the internet.
  
  *"A Service provides a stable IP and DNS name for your backend pods, so the frontend can always reach them."*

### 4.4 ReplicaSets
- **Definition:** Ensure that a specified number of Pod replicas are running at any time.
  
  *"ReplicaSets are managed by Deployments in most cases to maintain the desired count of pods."*

### 4.5 Ingress Controller
- **Definition:** Provides external access to services in the cluster.
  
  *"The Ingress Controller manages the traffic routing, ensuring requests to `myapp.com` are correctly routed to the frontend and backend services."*

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
