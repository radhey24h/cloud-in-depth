# AWS EKS Architecture and Key Kubernetes Components

## Table of Contents
1. [Introduction to Amazon EKS](#introduction-to-amazon-eks)
2. [EKS Control Plane](#eks-control-plane)
3. [EKS Worker Nodes](#eks-worker-nodes)
4. [Real-Time Use Case: Deploying a Web Application on EKS](#real-time-use-case-deploying-a-web-application-on-eks)
5. [Core Kubernetes Components](#core-kubernetes-components)
    - [Pods](#pods)
    - [Deployments](#deployments)
    - [Services](#services)
    - [ReplicaSets](#replicasets)
    - [Ingress Controller](#ingress-controller)
    - [ConfigMap and Secrets](#configmap-and-secrets)
    - [StatefulSet and DaemonSet](#statefulset-and-daemonset)
    - [Horizontal Pod Autoscaler (HPA)](#horizontal-pod-autoscaler-hpa)
6. [Scaling and Auto-Healing in EKS](#scaling-and-auto-healing-in-eks)
7. [Conclusion](#conclusion)

---

## Introduction to Amazon EKS

Amazon Elastic Kubernetes Service (EKS) is a managed service that allows you to run Kubernetes clusters in the AWS cloud. It abstracts away the complexity of managing the Kubernetes control plane while providing flexibility for configuring worker nodes.

---

## EKS Control Plane

The EKS control plane is fully managed by AWS and consists of several key components:

- **API Server**: Handles all Kubernetes API requests (e.g., deploying apps, scaling pods).
- **etcd**: Stores the cluster’s current state, including resources like pods, services, and secrets.
- **Controller Manager**: Maintains the cluster's desired state by managing operations like scaling pods and creating new replicas.
- **Scheduler**: Decides which nodes should run specific pods based on their resource requirements.

The control plane is responsible for handling all management tasks while AWS ensures its availability and performance.

---

## EKS Worker Nodes

Worker nodes in EKS are EC2 instances that run your application workloads. Each worker node contains the following components:

- **Kubelet**: Communicates with the control plane to ensure pods are running on the node.
- **Container Runtime**: Runs the actual containers (e.g., Docker, containerd).
- **Kube-proxy**: Manages networking rules, ensuring communication between pods and external services.

Worker nodes are where the application pods are scheduled and run. You have full control over the size, type, and number of worker nodes.

---

## Real-Time Use Case: Deploying a Web Application on EKS

### Step 1: Deploy the Application
- Define the deployment configuration in YAML files (e.g., `frontend-deployment.yaml`, `backend-deployment.yaml`).
- Use `kubectl apply` to deploy both the frontend (React) and backend (Node.js) to the cluster.

### Step 2: Pod Scheduling and Creation
- The control plane's Scheduler assigns the pods to worker nodes based on resource requirements.
- The Kubelet ensures the containers are running and healthy on the nodes.

### Step 3: Exposing the Application
- Create Kubernetes Services for both frontend and backend, using a LoadBalancer service for the frontend and a ClusterIP service for internal communication.

### Step 4: Managing Traffic with Ingress
- Set up an Ingress to route HTTP and HTTPS traffic to the appropriate services based on URL paths.

---

## Core Kubernetes Components

### Pods
- A **Pod** is the smallest deployable unit in Kubernetes and consists of one or more containers. In the use case, each frontend and backend instance is a pod.

### Deployments
- **Deployments** manage the lifecycle of Pods. You specify how many replicas of a Pod you want, and Kubernetes ensures the desired number is always running.

### Services
- A **Service** provides networking for Pods. It can expose Pods internally or externally via LoadBalancers, ClusterIP, or NodePort.

### ReplicaSets
- **ReplicaSets** ensure that a specified number of pod replicas are always running. They are typically managed by Deployments.

### Ingress Controller
- **Ingress Controllers** handle external HTTP/HTTPS traffic and route it to services within the cluster.

### ConfigMap and Secrets
- **ConfigMap**: Stores non-sensitive data such as environment variables.
- **Secret**: Stores sensitive information like API keys or credentials securely.

### StatefulSet and DaemonSet
- **StatefulSet**: Ensures that Pods are uniquely identified and maintain persistent storage (used for stateful apps).
- **DaemonSet**: Ensures that a specific pod runs on all worker nodes, typically used for monitoring or logging.

### Horizontal Pod Autoscaler (HPA)
- **HPA** automatically scales the number of pods based on CPU, memory, or other resource usage.

---

## Scaling and Auto-Healing in EKS

### Scaling
- EKS supports automatic scaling of both worker nodes and pods. Horizontal Pod Autoscaler (HPA) can scale Pods based on load, while you can configure the cluster to add more worker nodes when resource demands increase.

### Auto-Healing
- The control plane monitors worker nodes and pods. If a pod or worker node fails, EKS automatically reschedules the pods to healthy nodes, ensuring continuous availability.

---

## Conclusion

Amazon EKS provides a powerful platform for deploying, scaling, and managing containerized applications using Kubernetes. By leveraging core Kubernetes components like Pods, Deployments, and Services, along with AWS's fully managed control plane, you can build highly scalable and resilient applications with minimal management overhead.

For more detailed documentation, check out the [AWS EKS documentation](https://docs.aws.amazon.com/eks/latest/userguide/what-is-eks.html).

