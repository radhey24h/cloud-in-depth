# Azure Kubernetes Service (AKS)
Azure Kubernetes Service (AKS) is a managed Kubernetes container orchestration service provided by Microsoft Azure. It simplifies deploying, managing, and scaling containerized applications using Kubernetes.

AKS is highly available, secure and fully managed kubernates service, as on today it is available in 36 regions and growing daya by day, so if we will copare with other cloud AKS is available in heighest number of regions.

AKS is able to run any type of workloads:-
  Windows based application .net application
  Linux supported application like Java, dotnet core, nodeJS
  IOT device deployment and management on demand
  Machine learing model training with AKS

## AKS Architecture
Azure Kubernetes Service (AKS) architecture consists of several key components that work together to manage and orchestrate containerized applications:

### 1. Kubernetes Cluster
   - **Description:**
   
   A Kubernetes cluster includes a control plane and worker nodes or node pools. The control plane is managed by Azure and includes components like the API server, scheduler, and ETCD. 
   
   The worker nodes run the containerized applications.
   - **Architecture:** 
     - **Control Plane:** Managed by Azure, Handles API requests, schedules workloads, and maintains cluster state.


     - **Worker Nodes:** Virtual machines that execute the containerized workloads. They are part of one or more node pools.



   - **Use Case:** A company wants to deploy a microservices-based application. AKS provides a Kubernetes cluster where each microservice runs in its own pod on the worker nodes.
   - **Billing Details:** Charges based on the underlying VM sizes and the number of worker nodes. The control plane is provided at no additional cost.
   - **Commands:**
     ```bash
     # Create an AKS cluster
     az aks create --resource-group <ResourceGroupName> --name <ClusterName> --node-count 1 --enable-addons monitoring --generate-ssh-keys
     
     # Get cluster credentials
     az aks get-credentials --resource-group <ResourceGroupName> --name <ClusterName>
     ```

### 2. Node Pools
   - **Description:** Groups of virtual machines (VMs) in a Kubernetes cluster. Each node pool can have different VM sizes, operating systems, and scaling rules.
   - **Architecture:** 
     - **Primary Node Pool:** Default node pool where most workloads run.
     - **Additional Node Pools:** Can be configured for specialized workloads (e.g., GPU-enabled nodes for high-performance computing).
   - **Use Case:** An organization has both general-purpose and high-performance workloads. They create separate node pools for each type, optimizing cost and performance.
   - **Billing Details:** Costs depend on the VM sizes and the number of nodes in each pool. Additional charges for specialized VMs like GPU-enabled instances.
   - **Commands:**
     ```bash
     # Add a new node pool
     az aks nodepool add --resource-group <ResourceGroupName> --cluster-name <ClusterName> --name <NodePoolName> --node-count 2 --node-vm-size <VMSize>
     ```

### 3. Pods
   - **Description:** The smallest deployable units in Kubernetes, encapsulating one or more containers. Pods share networking and storage resources.
   - **Architecture:** 
     - **Single Container Pod:** Runs a single container.
     - **Multi-Container Pod:** Multiple containers share the same network namespace and storage volumes.
   - **Use Case:** A web application running in a pod with multiple containers handling different tasks (e.g., frontend, backend, and database).
   - **Billing Details:** Indirect costs based on the VM instances running the pods and the resources consumed.
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
     - **LoadBalancer Service:** Exposes the service externally via a cloud load balancer.
   - **Use Case:** A LoadBalancer Service is used to expose a web application to the internet, providing a stable IP address for external access.
   - **Billing Details:** Costs for LoadBalancer services include charges for the public IP address and data transfer.
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
   - **Billing Details:** Costs for PVs depend on the storage type and amount used (e.g., standard SSD, premium SSD).
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

## Billing Details

### Cost Factors

1. **Cluster Costs:** Charges are based on the virtual machines (VMs) used for worker nodes. The control plane is managed by Azure and incurs no additional cost.
2. **Node Pools:** Costs depend on the number and size of VMs in each node pool. Specialized VMs like GPU-enabled instances incur higher costs.
3. **Storage:** Charges for persistent storage used by applications and data, such as SSDs and standard storage.
4. **Networking:** Costs for outbound data transfer, load balancers, and public IP addresses.
5. **Additional Services:** Charges for additional features like Azure Monitor, Application Insights, and Azure Container Registry.

### Pricing Tiers

- **Basic Pricing:** Includes standard AKS cluster costs and virtual machine pricing.
- **Advanced Features:** Additional charges for features like Azure Monitor and Azure Security Centre.

For detailed and up-to-date pricing information, refer to the [Azure Pricing Calculator](https://azure.microsoft.com/en-us/pricing/calculator/) and the [Azure AKS pricing page](https://azure.microsoft.com/en-us/pricing/details/kubernetes-service/).

This README provides a thorough overview of Azure Kubernetes Service (AKS), including its components, architecture, use cases, billing details, and relevant commands and YAML code. It serves as a comprehensive guide for understanding and managing AKS in Azure environments.
