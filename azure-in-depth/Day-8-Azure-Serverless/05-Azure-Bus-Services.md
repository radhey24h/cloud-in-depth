# Azure Service Bus
Azure Service Bus is a fully managed enterprise messaging service from Microsoft Azure that enables reliable communication between distributed applications and services. It provides a scalable and secure way to send and receive messages between different parts of your application.

## Overview
Azure Service Bus is designed to handle complex messaging patterns and scenarios, including:

- **Queue-based Messaging**: Azure Service Bus queues allow you to send messages to a queue and receive them in a first-in, first-out (FIFO) manner. This ensures that messages are processed once and only once.
- **Publish/Subscribe**: Azure Service Bus topics and subscriptions support the publish/subscribe messaging pattern, allowing you to send messages to a topic and have them delivered to multiple subscribers. Each subscriber receives a copy of the message.
- **Message Sessions**: Azure Service Bus supports message sessions, which allow for stateful message processing. Sessions are used to handle messages that require a specific order of processing or need to maintain state.
- **Dead-lettering**: Azure Service Bus can move messages that cannot be processed to a dead-letter queue, where they can be inspected and handled separately.
- **Scheduled Messages**: You can schedule messages to be sent at a specific time in the future, providing a delay before the message is processed.

## Components
### Queues
- **Purpose**: Queues in Azure Service Bus enable one-to-one communication, where messages are sent by producers and consumed by a single consumer.
- **Characteristics**:
  - FIFO (First-In-First-Out) processing.
  - Messages are received and deleted by consumers.

### Topics and Subscriptions
- **Purpose**: Topics and subscriptions enable one-to-many communication, where messages are sent to a topic and then distributed to multiple subscriptions.
- **Characteristics**:
  - Multiple subscriptions can receive copies of the same message.
  - Each subscription can have its own filtering rules to determine which messages are received.

### Message Sessions
- **Purpose**: Message sessions provide a way to group related messages and maintain state between messages.
- **Characteristics**:
  - Sessions ensure messages are processed in order.
  - Useful for scenarios requiring message grouping and stateful processing.

### Dead-Letter Queues
- **Purpose**: Dead-letter queues hold messages that cannot be processed successfully by the application.
- **Characteristics**:
  - Messages in the dead-letter queue can be inspected and handled separately.
  - Helps in debugging and handling message processing errors.

### Scheduled Messages
- **Purpose**: Allows you to schedule messages to be sent at a future time.
- **Characteristics**:
  - Provides delay capabilities for message processing.
  - Useful for scenarios where messages need to be deferred.

## Security and Reliability
- **Security**: Azure Service Bus supports encryption at rest and in transit, ensuring that your messages are secure. It also supports role-based access control (RBAC) and shared access signatures (SAS) for fine-grained access management.
- **Reliability**: Azure Service Bus provides high availability and disaster recovery features, ensuring that your messaging system is robust and resilient to failures.

## Architecture

- **Namespaces:** Logical containers for Service Bus resources, such as queues and topics.
- **Queues:** Used for point-to-point messaging. Messages are sent to a queue and received by a single consumer.
- **Topics and Subscriptions:** Used for publish/subscribe messaging. Messages are sent to a topic and can be received by multiple subscriptions.
- **Relays:** Enable secure communication between on-premises applications and cloud services.

## Use Cases

1. **Decoupling Applications:**
   - **Scenario:** A retail application requires communication between its order processing system and inventory management system.
   - **Solution:** Use a Service Bus Queue to decouple the systems, ensuring reliable message delivery and processing.

2. **Pub/Sub Messaging:**
   - **Scenario:** An e-commerce platform needs to send notifications to various services (e.g., email, SMS) when an order is placed.
   - **Solution:** Use a Service Bus Topic with multiple Subscriptions to deliver messages to different services.

3. **Reliable Messaging:**
   - **Scenario:** A financial application needs guaranteed message delivery even in the event of temporary outages.
   - **Solution:** Use Service Bus Queues with message sessions to ensure reliable and ordered processing.

### Billing Details

- **Pricing Tiers:** Charges based on the tier selected (Basic, Standard, Premium).
- **Cost Factors:** Number of operations (e.g., sends, receives), message size, and throughput units.

### Commands

```bash
# Create a Service Bus namespace
az servicebus namespace create --resource-group <ResourceGroupName> --name <NamespaceName> --location <Location>

# Create a queue in the Service Bus namespace
az servicebus queue create --resource-group <ResourceGroupName> --namespace-name <NamespaceName> --name <QueueName>

# Create a topic in the Service Bus namespace
az servicebus topic create --resource-group <ResourceGroupName> --namespace-name <NamespaceName> --name <TopicName>

# Send a message to a queue
az servicebus queue message send --resource-group <ResourceGroupName> --namespace-name <NamespaceName> --queue-name <QueueName> --body "Hello, World!"
```

## YAML Configuration (Example for Topic and Subscription)

```yaml
apiVersion: "2021-01-01"
kind: ServiceBusNamespace
metadata:
  name: my-servicebus-namespace
spec:
  sku: Standard
  location: eastus

apiVersion: "2021-01-01"
kind: ServiceBusTopic
metadata:
  name: my-topic
  namespace: my-servicebus-namespace
spec:
  maxSizeInMegabytes: 1024
  defaultMessageTimeToLive: "P1D"

apiVersion: "2021-01-01"
kind: ServiceBusSubscription
metadata:
  name: my-subscription
  topic: my-topic
  namespace: my-servicebus-namespace
spec:
  maxSizeInMegabytes: 256
```
