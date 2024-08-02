# Amazon Elastic Kubernetes Service (EKS)

Amazon Elastic Kubernetes Service (Amazon EKS) is a fully managed service that makes it easy for you to use Kubernetes on AWS without having to be an expert in managing Kubernetes clusters. EKS simplifies running Kubernetes on AWS without needing to manage the control plane.

## Key Features of Amazon EKS

- **Upstream Kubernetes**: Amazon EKS runs the upstream version of the open-source Kubernetes software, so you can use all the existing plugins and tooling from the Kubernetes community. Applications running on Amazon EKS are fully compatible with applications running on any standard Kubernetes environment, whether running in on-premises data-centers or public clouds. This means you can easily migrate your Kubernetes application to Amazon EKS with zero code changes.
- **High Availability and Resiliency**: Amazon EKS automatically runs Kubernetes with three masters across three AWS Availability Zones (AZs) to protect against a single point of failure. This multi-AZ architecture delivers resiliency against the loss of an AWS Availability Zone.
- **Automated Management**: Amazon EKS automatically detects and replaces unhealthy masters and provides automated version upgrades and patching for the masters.
- **Integration with AWS Services**: EKS is integrated with a number of key AWS features such as Elastic Load Balancing for load distribution, IAM for authentication, Amazon VPC for isolation, AWS PrivateLink for private network access, and AWS CloudTrail for logging.

## Benefits of Using Amazon EKS

- **Fully Managed**: EKS automatically manages the availability and scalability of the Kubernetes control plane nodes responsible for scheduling containers, managing application availability, storing cluster data, and other key tasks.
- **Security and Compliance**: EKS uses IAM for authentication and leverages network policies to restrict communication at the pod level, ensuring compliance with security standards.
- **Cost Efficiency**: You only pay for the EKS clusters and the AWS resources (such as EC2 instances) you use. There is no upfront cost for using EKS.
- **Seamless Upgrades**: EKS provides easy and seamless upgrades to new Kubernetes versions with minimal downtime.

## How Amazon EKS Works

1. **Create a Cluster**: Use the AWS Management Console, CLI, or API to create a Kubernetes cluster with EKS. EKS manages the Kubernetes control plane for you.
2. **Connect Worker Nodes**: Add Amazon EC2 instances or AWS Fargate as worker nodes to your EKS cluster. The worker nodes run your application containers.
3. **Deploy Applications**: Use kubectl, Helm, or any Kubernetes-compatible tooling to deploy and manage your applications on EKS.
4. **Monitor and Maintain**: Use CloudWatch, CloudTrail, and other AWS monitoring tools to keep track of your EKS cluster's health and performance.

## Important Terms

- **Cluster**: A set of control plane nodes that manage Kubernetes worker nodes where containers are deployed.
- **Worker Nodes**: EC2 instances or Fargate tasks that run your containerized applications.
- **Pod**: The smallest deployable unit in Kubernetes, consisting of one or more containers.
- **Control Plane**: The collection of processes that manage the state of a Kubernetes cluster, including the API server, ETCD, and scheduler.
- **Node Group**: A group of worker nodes in an EKS cluster with the same configuration and management settings.

## AWS Fargate – A Compute Engine for ECS and EKS

AWS Fargate is a compute engine for Amazon Elastic Container Service (ECS) and Amazon EKS that allows you to run containers without having to provision, configure, and scale clusters of VMs that host container applications.

### Key Features of AWS Fargate

- **No Server Management**: AWS Fargate eliminates the need for users to manage the EC2 instances on their own. In fact, users don’t need to use EC2 instances at all. Fargate itself will act as a compute engine.
- **Focus on Applications**: It lets you focus on elements like designing and constructing your application instead of managing the infrastructure that runs them.
- **Easy Scaling**: AWS Fargate makes it easy to scale your applications. Once you define all your application requirements, AWS Fargate manages all the scaling and infrastructure needed to run your containers in a highly-available manner.
- **Seamless Integration**: It seamlessly integrates with Amazon ECS and EKS, launches, and manages your containers for you.

### How AWS Fargate Works

With the Fargate launch type, all you need to do is package your application in containers, specify the memory and CPU requirements, define IAM policies, and launch your application. Fargate takes care of the rest, ensuring high availability and managing the required resources.

## Security and Compliance

- **IAM Integration**: EKS uses IAM roles and policies to control access to Kubernetes resources.
- **Network Policies**: You can define rules to control traffic flow between pods and services in your EKS cluster.
- **Data Encryption**: EKS supports encryption of data at rest and in transit for secure communication and storage.

## Use Cases for Amazon EKS

- **Microservices Architecture**: EKS is ideal for deploying and managing microservices-based applications.
- **Machine Learning**: Run and scale machine learning workloads using Kubernetes operators and frameworks.
- **CI/CD Pipelines**: Automate your application deployment processes using EKS with tools like Jenkins or GitLab.
- **Hybrid Deployments**: Use EKS to run Kubernetes clusters in a hybrid cloud environment, leveraging on-premises and cloud resources.

## Limitations of Amazon EKS

- **Complexity**: While EKS simplifies managing Kubernetes, understanding Kubernetes concepts is necessary to optimize your deployments.
- **Cost**: Managing large-scale clusters can incur significant costs, especially when using EC2 instances as worker nodes.

## Getting Started with Amazon EKS

1. **Set Up AWS CLI**: Install and configure the AWS CLI to interact with your AWS account.
2. **Create an EKS Cluster**: Use the AWS Management Console, CLI, or eksctl tool to create your first EKS cluster.
3. **Configure kubectl**: Install and configure kubectl to manage your Kubernetes cluster.
4. **Deploy Applications**: Use Kubernetes manifests or Helm charts to deploy applications to your EKS cluster.

By using Amazon EKS, you can run Kubernetes applications on a fully managed, secure, and highly available platform that integrates seamlessly with other AWS services.

## EKS Architecture

### 1. Kubernetes Cluster
   - **Description:** A Kubernetes cluster consists of a control plane and worker nodes. The control plane is managed by AWS and includes components like the API server, ETCD, and scheduler. Worker nodes are EC2 instances that run the containerized applications.
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
   - **Description:** Node groups in EKS (Elastic Kubernetes Service) are collections of Amazon EC2 instances that provide the compute capacity for running your Kubernetes workloads. Each node group consists of one or more EC2 instances, which Kubernetes uses to run pods (smallest deployable units in Kubernetes)
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
