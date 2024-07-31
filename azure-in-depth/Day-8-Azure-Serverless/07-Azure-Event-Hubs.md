# Azure Event Grid and Azure Event Hubs

## Azure Event Hubs

Azure Event Hubs is a fully managed, real-time data ingestion service that can handle large amounts of data.

### Architecture

- **Event Hubs**: A highly scalable data streaming platform that ingests events and streams.
- **Consumer Groups**: Allow multiple consumers to read from an event hub independently.
- **Partitions**: Logical segments of an event hub that allow parallel processing of events.

### Use Cases

#### Real-Time Data Processing

- **Scenario**: A financial institution needs to process streaming data from transactions in real-time.
- **Solution**: Use Event Hubs to ingest transaction data and process it with Azure Stream Analytics or custom applications.

#### Telemetry and Log Data

- **Scenario**: Collect and analyse telemetry data from IoT devices.
- **Solution**: Use Event Hubs to collect telemetry data from devices and stream it to Azure Blob Storage or Azure Data Lake for analysis.

#### Large-Scale Event Streaming

- **Scenario**: A gaming company needs to process large volumes of game telemetry data for real-time analytics.
- **Solution**: Use Event Hubs to ingest and process game telemetry data, enabling real-time insights and analytics.

### Billing Details

- **Pricing Tiers**: Charges are based on throughput units, data retention, and data ingress/egress.
- **Cost Factors**: Consider the number of throughput units, amount of data ingested, and data retention period.

## Commands
```bash
# Create an Event Hub Namespace
az eventhubs namespace create --resource-group <ResourceGroupName> --name <NamespaceName> --location <Location>

# Create an Event Hub
az eventhubs eventhub create --resource-group <ResourceGroupName> --namespace-name <NamespaceName> --name <EventHubName> --message-retention 1

# Create a Consumer Group
az eventhubs consumer-group create --resource-group <ResourceGroupName> --namespace-name <NamespaceName> --eventhub-name <EventHubName> --name <ConsumerGroupName>

# Send a test event
az eventhubs eventhub send --resource-group <ResourceGroupName> --namespace-name <NamespaceName> --eventhub-name <EventHubName> --data '{"message": "Hello, Event Hubs!"}'
```

## YAML Configuration (Example for Event Hub and Consumer Group)
```yaml
apiVersion: "2021-01-01"
kind: EventHubNamespace
metadata:
  name: my-eventhub-namespace
spec:
  location: eastus

apiVersion: "2021-01-01"
kind: EventHub
metadata:
  name: my-eventhub
  namespace: my-eventhub-namespace
spec:
  partitionCount: 4
  messageRetentionInDays: 1

apiVersion: "2021-01-01"
kind: ConsumerGroup
metadata:
  name: my-consumer-group
  eventhub: my-eventhub
  namespace: my-eventhub-namespace
spec:
  id: my-consumer-group

```