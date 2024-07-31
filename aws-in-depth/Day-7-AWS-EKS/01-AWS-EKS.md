# AWS Elastic Kubernetes Service (EKS)

AWS Elastic Kubernetes Service (EKS) is a managed Kubernetes service that simplifies running Kubernetes on AWS without needing to install and operate your own Kubernetes control plane. This document provides a detailed overview of EKS components, architecture, use cases, billing details, and relevant commands and YAML examples.

## EKS Architecture

AWS EKS architecture consists of several key components that work together to manage and orchestrate containerized applications:

### 1. Kubernetes Cluster
   - **Description:** The core component of EKS. A Kubernetes cluster consists of a control plane and worker nodes. The control plane is managed by AWS and includes components like the API server, ETCD, and scheduler. Worker nodes are EC2 instances that run the containerized applications.
   - **Architecture:** 
     - **Control Plane:** Managed by AWS. Handles API requests, schedules workloads, and maintains the cluster state. It runs across multiple Availability Zones for high availability.
     - **Worker Nodes:** EC2 instances running in your VPC that execute containerized workloads. Managed as part of an Auto Scaling group.
   - **Use Case:** A company wants to deploy a scalable web application using microservices. EKS provides a Kubernetes cluster where each microservice runs in its own pod on the worker nodes.
   - **Billing Details:** Charges for the control plane (flat fee) and worker nodes (based on the underlying EC2 instance types and sizes).
   - **Commands:**
     ```bash
     # Create an EKS cluster using eksctl
     eksctl create cluster --name <ClusterName> --region <Region> --nodegroup-name <NodeGroupName> --node-type <InstanceType> --nodes 3
     
     # Update kubeconfig to access the cluster
     aws eks --region <Region> update-kubeconfig --name <ClusterName>
     ```

### 2. Node Groups
   - **Description:** Managed groups of EC2 instances that host the pods. Node groups can be scaled independently and have different instance types.
   - **Architecture:** 
     - **Managed Node Groups:** AWS handles the provisioning and lifecycle management of the nodes.
     - **Self-Managed Node Groups:** Users manually manage EC2 instances and configurations.
   - **Use Case:** An organization requires high-performance compute nodes for AI workloads and general-purpose nodes for other applications. They create separate node groups for each requirement.
   - **Billing Details:** Costs based on the EC2 instances in each node group. Different charges for different instance types and sizes.
   - **Commands:**
     ```bash
     # Create a new managed node group
     eksctl create nodegroup --cluster <ClusterName> --name <NodeGroupName> --node-type <InstanceType> --nodes 2
     ```

### 3. Pods
   - **Description:** The smallest deployable units in Kubernetes, encapsulating one or more containers. Pods share networking and storage resources.
   - **Architecture:** 
     - **Single Container Pod:** Runs a single container.
     - **Multi-Container Pod:** Multiple containers share the same network namespace and storage volumes.
   - **Use Case:** A backend API service running in a pod with multiple containers handling different layers (e.g., application logic, caching).
   - **Billing Details:** Indirect costs based on the EC2 instances running the pods and the resources consumed.
   - **YAML Code:**
     ```yaml
     apiVersion: v1
     kind: Pod
     metadata:
       name: my-pod
     spec:
       containers:
       - name: my-container
         image: nginx
         ports:
         - containerPort: 80
     ```

### 4. Services
   - **Description:** Define a set of pods and provide stable access endpoints (IP addresses and DNS names). Services manage network access to pods.
   - **Architecture:** 
     - **ClusterIP Service:** Exposes the service internally within the cluster.
     - **NodePort Service:** Exposes the service on a specific port on each node.
     - **LoadBalancer Service:** Exposes the service externally via an AWS ELB (Elastic Load Balancer).
   - **Use Case:** A LoadBalancer Service exposes an application to the internet, providing a stable IP address for external access.
   - **Billing Details:** Costs for ELB services, including charges for the public IP address and data transfer.
   - **YAML Code:**
     ```yaml
     apiVersion: v1
     kind: Service
     metadata:
       name: my-service
     spec:
       type: LoadBalancer
       selector:
         app: my-app
       ports:
         - protocol: TCP
           port: 80
           targetPort: 80
     ```

### 5. Ingress Controllers
   - **Description:** Manage external access to services, typically HTTP or HTTPS traffic. Ingress Controllers provide features like SSL termination and URL-based routing.
   - **Architecture:** 
     - **Ingress Resource:** Defines routing rules.
     - **Ingress Controller:** Implements the rules and manages traffic.
   - **Use Case:** An Ingress Controller routes traffic to different services based on URL paths (e.g., `/api` routes to one service, `/web` routes to another).
   - **Billing Details:** Costs associated with the resources used by the Ingress Controller, such as load balancers.
   - **YAML Code:**
     ```yaml
     apiVersion: networking.k8s.io/v1
     kind: Ingress
     metadata:
       name: my-ingress
     spec:
       rules:
       - host: myapp.example.com
         http:
           paths:
           - path: /api
             pathType: Prefix
             backend:
               service:
                 name: api-service
                 port:
                   number: 80
           - path: /web
             pathType: Prefix
             backend:
               service:
                 name: web-service
                 port:
                   number: 80
     ```

### 6. Persistent Volumes (PVs) and Persistent Volume Claims (PVCs)
   - **Description:** PVs are storage resources in Kubernetes. PVCs are requests for storage by pods.
   - **Architecture:** 
     - **Persistent Volume:** A storage resource provisioned in the cluster.
     - **Persistent Volume Claim:** A request for storage by a pod.
   - **Use Case:** A database pod uses a PVC to request storage, ensuring data persists beyond the pod's lifecycle.
   - **Billing Details:** Costs for PVs depend on the storage type and amount used (e.g., Amazon EBS, Amazon EFS).
   - **YAML Code:**
     ```yaml
     # Persistent Volume
     apiVersion: v1
     kind: PersistentVolume
     metadata:
       name: my-pv
     spec:
       capacity:
         storage: 5Gi
       accessModes:
         - ReadWriteOnce
       hostPath:
         path: /mnt/data

     # Persistent Volume Claim
     apiVersion: v1
     kind: PersistentVolumeClaim
     metadata:
       name: my-pvc
     spec:
       accessModes:
         - ReadWriteOnce
       resources:
         requests:
           storage: 5Gi
     ```

### 7. ConfigMaps and Secrets
   - **Description:** ConfigMaps store non-sensitive configuration data, while Secrets store sensitive data like passwords and API keys.
   - **Architecture:** 
     - **ConfigMap:** Holds configuration data that can be consumed by pods.
     - **Secret:** Stores sensitive data that is encrypted at rest and can be accessed by pods.
   - **Use Case:** A ConfigMap holds configuration settings for an application, while a Secret stores database credentials.
   - **Billing Details:** No additional costs for ConfigMaps and Secrets, but their storage impacts the overall storage costs of the cluster.
   - **YAML Code:**
     ```yaml
     # ConfigMap
     apiVersion: v1
     kind: ConfigMap
     metadata:
       name: my-config
     data:
       config.json: |
         {
           "key": "value"
         }

     # Secret
     apiVersion: v1
     kind: Secret
     metadata:
       name: my-secret
     type: Opaque
     data:
       password: cGFzc3dvcmQ=
     ```

### 8. Helm Charts
   - **Description:** Helm is a package manager for Kubernetes, using Charts to define, install, and manage applications.
   - **Architecture:** 
     - **Helm Chart:** A package containing Kubernetes manifests and configuration templates.
   - **Use Case:** Helm Charts simplify deploying complex applications, like a multi-tier web application, by packaging all necessary Kubernetes resources.
   - **Billing Details:** Costs associated with Helm Charts are included in the overall cost of resources deployed by the charts.
   - **Commands:**
```bash
     # Install a Helm Chart
     helm install my-release my-chart

     # Upgrade a Helm Chart
     helm upgrade my-release my-chart

     # Uninstall a Helm Chart
     helm uninstall my-release
```


# Setting Up AWS EKS
## Step-by-Step Guide

**Create an EKS Cluster:**
   - **Commands:**
```bash
eksctl create cluster --name <ClusterName> --region <Region> --nodegroup-name <NodeGroupName> --node-type <InstanceType> --nodes 3
```
**Update kubeconfig:**
   - **Commands:**
```bash
aws eks --region <Region> update-kubeconfig --name <ClusterName>
```

## Deploy Applications:
**Create a Deployment:**
   - **Commands:**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-container
        image: nginx
        ports:
        - containerPort: 80

```

**Apply the Deployment:**
   - **Commands:**
```bash
kubectl apply -f deployment.yaml
```

## Expose the Application:
**Create a Service:**
   - **Commands:**
```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  type: LoadBalancer
  selector:
    app: my-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80

```

 ### Apply the Service:
   - **Commands:**
```bash
kubectl apply -f service.yaml
```


## Configure Ingress:
**Create an Ingress Resource:**
   - **Commands:**
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-ingress
spec:
  rules:
  - host: myapp.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: my-service
            port:
              number: 80
```

 ### Apply the Service:
   - **Commands:**
```bash
kubectl apply -f ingress.yaml

```
## Billing Details

### Cost Factors

1. **Cluster Costs:**
   - **EKS Control Plane:** AWS charges a flat hourly rate for the managed Kubernetes control plane. This cost covers the API server, ETCD, and other critical components that AWS manages for you.
   - **Worker Nodes:** Costs for EC2 instances that run your Kubernetes workloads. Pricing varies based on the instance type and size you choose, including factors such as instance hours, storage, and any associated data transfer.

2. **Node Groups:**
   - **EC2 Instances:** The cost is determined by the number and type of EC2 instances in each node group. Different instance types have varying hourly rates. For example, compute-optimized instances cost more than general-purpose instances.
   - **Auto Scaling:** Costs may also include any additional charges for Auto Scaling groups, which automatically adjust the number of instances in your node group based on demand.

3. **Storage:**
   - **Amazon EBS:** Charges apply for Elastic Block Store (EBS) volumes used by your worker nodes to store data persistently. Pricing is based on the volume type (e.g., SSD, HDD), size, and IOPS (Input/Output Operations Per Second) provisioned.
   - **Amazon EFS:** If using Elastic File System (EFS) for shared storage, costs include storage capacity and data transfer rates. EFS pricing is based on the amount of data stored and the throughput required.

4. **Networking:**
   - **Data Transfer:** Costs for outbound data transfer from your EKS cluster to the internet or other AWS regions. Inbound data transfer is generally free, but outbound data incurs charges based on the amount of data transferred.
   - **Load Balancers:** Charges for AWS Elastic Load Balancers (ELB) used to expose services running on your EKS cluster. Pricing is based on the number of hours the load balancer is running and the amount of data processed.

5. **Additional Costs:**
   - **EKS Add-ons:** Costs for additional AWS services integrated with EKS, such as AWS CloudWatch for monitoring and logging, AWS Systems Manager for operational data management, and AWS Secrets Manager for handling sensitive information.
   - **Ingress Controllers:** If using services like AWS Application Load Balancer (ALB) for ingress, you may incur additional costs based on the ALB's usage and data processed.

### Example Cost Breakdown

- **EKS Control Plane:** $0.10 per hour
- **EC2 Worker Nodes:** $0.096 per hour (for a t3.medium instance, as an example)
- **EBS Storage:** $0.10 per GB per month (for General Purpose SSD)
- **Data Transfer Out:** $0.09 per GB (for data transferred to the internet)
- **ELB:** $0.0225 per hour and $0.008 per GB data processed (for Application Load Balancer)

### Cost Optimization Tips

1. **Choose Appropriate EC2 Instances:** Select EC2 instance types that match your workload requirements to avoid over-provisioning and reduce costs.
2. **Use Spot Instances:** Consider using EC2 Spot Instances for non-critical or batch processing workloads to take advantage of lower pricing.
3. **Monitor and Scale:** Regularly monitor your cluster’s performance and adjust the size of your node groups based on actual usage to optimize costs.
4. **Leverage Savings Plans:** Use AWS Savings Plans for reserved capacity to reduce long-term costs associated with your EC2 instances.

For detailed and up-to-date information on AWS EKS pricing, visit the [AWS EKS Pricing page](https://aws.amazon.com/eks/pricing/) and the [AWS Pricing Calculator](https://calculator.aws/#/).
