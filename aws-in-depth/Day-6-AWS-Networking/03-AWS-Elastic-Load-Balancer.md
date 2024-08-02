## Load Balancers in AWS


### What is a Load Balancer?

A Load Balancer is a virtual machine or appliance that distributes incoming HTTP or HTTPS traffic across multiple web servers, ensuring that no single server becomes overwhelmed.

### Elastic Load Balancer (ELB)

ELB automatically manages the workload on your instances and distributes it to other instances in case of an instance failure.

### Application Load Balancer (ALB)

- **Launch Date**: AWS launched the Application Load Balancer (ALB) on August 11, 2016.
- **Purpose**: Directs user traffic to resources in the public AWS cloud.
- **Layer**: Operates at Layer 7 of the OSI Model, allowing it to identify incoming traffic and forward it to the appropriate resources. For example, traffic with API extensions in a URL is routed to the correct application resources.
- **Best Suited For**: Load balancing HTTP and HTTPS traffic.
- **Features**: ALBs are intelligent and can route specific requests to specific web servers.

  **Example**: Consider Tesla, which has three models: Model X, Model S, and Model 3, each with onboard computing facilities. A group of web servers might be dedicated to each model. An ALB can determine whether incoming traffic is for Model X, Model S, or Model 3 and route it to the appropriate group of servers.

### Network Load Balancer (NLB)

- **Layer**: Operates at Layer 4 of the OSI Model.
- **Routing**: Makes decisions at the transport layer (TCP/SSL) and can handle millions of requests per second.
- **Mechanism**: When a connection is received, the NLB selects a target from the target group using a flow hash routing algorithm. It opens a TCP connection to the selected target on the port and forwards the request without modifying the headers.
- **Best Suited For**: Load balancing TCP traffic where high performance is required.

### Classic Load Balancer (CLB)

- **Layer**: Operates at Layer 4 of the OSI Model.
- **Routing**: Routes traffic between clients and backend servers based on IP address.
- **Example**: An Elastic Load Balancer receives a request from a client on TCP port 80 and routes it to a specified port on the backend servers. The backend server sends the requested data back to the ELB, which then forwards the response to the client. To the client, the request appears to be fulfilled by the ELB rather than the backend server.
- **Legacy**: Classic Load Balancers are considered legacy ELBs.
- **Capabilities**: They can be used for load balancing HTTP or HTTPS traffic and support Layer 7-specific features such as X-Forwarded-For and sticky sessions. They also offer Layer 4 load balancing for applications relying purely on the TCP protocol.


## OSI Model Layers

The OSI (Open Systems Interconnection) model is a framework used to understand and standardize network communication. It consists of seven layers, each with specific functions.

### OSI Layers Overview

1. **Layer 1: Physical Layer**
   - Deals with the physical connection between devices, such as cables and switches.

2. **Layer 2: Data Link Layer**
   - Handles error detection and correction from Layer 1 and manages node-to-node data transfer.

3. **Layer 3: Network Layer**
   - Manages packet forwarding, including routing through different routers. Example protocols: IP (Internet Protocol).

4. **Layer 4: Transport Layer**
   - Provides end-to-end communication services for applications. It ensures complete data transfer and manages error correction and flow control.
   - **Protocols**:
     - **TCP (Transmission Control Protocol)**: Provides reliable, connection-oriented communication with error checking and flow control.
     - **UDP (User Datagram Protocol)**: Provides connectionless, faster communication without error checking and flow control.

5. **Layer 5: Session Layer**
   - Manages sessions or connections between applications. It establishes, maintains, and terminates communication sessions.

6. **Layer 6: Presentation Layer**
   - Translates data between the application layer and the network format. It is responsible for data encryption, compression, and translation.

7. **Layer 7: Application Layer**
   - Provides network services directly to end-user applications. It interacts with software applications and provides services such as email, file transfers, and web browsing.
   - **Protocols**:
     - **HTTP (Hypertext Transfer Protocol)**: Used for transferring web pages and resources.
     - **FTP (File Transfer Protocol)**: Used for transferring files between clients and servers.
     - **SMTP (Simple Mail Transfer Protocol)**: Used for sending emails.