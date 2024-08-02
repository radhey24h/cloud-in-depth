# Azure Event Grid

Azure Event Grid is a fully managed event routing service that allows you to easily build event-driven architectures.

## Architecture

- **Event Sources**: The origin of events, such as Azure services or custom applications.
- **Event Grid Topics**: Endpoints where events are published.
- **Event Grid Subscriptions**: Define how events are delivered, such as to a webhook or Azure Function.

## Use Cases

### Event-Driven Architecture

- **Scenario**: An application needs to trigger workflows based on various events, such as file uploads or data changes.
- **Solution**: Use Event Grid Topics to publish events and Event Grid Subscriptions to trigger Azure Functions or Logic Apps.

### Real-Time Notifications

- **Scenario**: A content management system needs to send notifications to subscribers when new content is published.
- **Solution**: Use Event Grid to publish events when content is published and route notifications to subscribers via webhooks or email.

### Integration with SaaS Applications

- **Scenario**: Integrate with third-party SaaS applications to handle specific events.
- **Solution**: Use Event Grid to route events to external systems via HTTP endpoints.

## Billing Details

- **Pricing Model**: Charges are based on the number of operations, such as event ingress and event delivery.
- **Cost Factors**: The cost depends on the number of events published and the number of event deliveries.

## Commands
```bash
# Create an Event Grid Topic
az eventgrid topic create --resource-group <ResourceGroupName> --name <TopicName> --location <Location>

# Create an Event Grid Subscription
az eventgrid event-subscription create --resource-group <ResourceGroupName> --topic-name <TopicName> --name <SubscriptionName> --endpoint <EndpointURL>

# Send a test event
az eventgrid event publish --topic-name <TopicName> --resource-group <ResourceGroupName> --event-type "CustomEvent" --subject "test" --data '{"message": "Hello, Event Grid!"}'

```
## YAML Configuration (Example for Event Grid Subscription)
```yaml
apiVersion: "2021-01-01"
kind: EventGridTopic
metadata:
  name: my-eventgrid-topic
spec:
  location: eastus

apiVersion: "2021-01-01"
kind: EventGridSubscription
metadata:
  name: my-eventgrid-subscription
  topic: my-eventgrid-topic
spec:
  destination:
    endpointType: WebHook
    properties:
      endpointUrl: https://mywebhook.endpoint
  filter:
    subjectBeginsWith: /events/
    subjectEndsWith: .json
```