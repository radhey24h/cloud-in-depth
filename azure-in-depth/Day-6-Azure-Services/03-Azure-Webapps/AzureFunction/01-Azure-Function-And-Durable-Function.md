# Azure Functions and Durable Functions

Azure Functions is a serverless event driven compute service provided by Microsoft Azure that enables you to run your code without managing infrastructure. 

Azure Durable Functions is an extension of Azure Functions that allows you to write stateful workflows in a serverless compute environment.

## Azure Functions
### Overview
Azure Functions lets you run small pieces of code, or "functions," in the cloud without provisioning or managing servers. It automatically scales based on demand and integrates with various Azure services.

### Architecture

- **Function App:** A container for one or more functions. It provides the execution context for the functions.
- **Function:** The individual piece of code that performs a specific task. Functions can be triggered by various events such as HTTP requests, messages in a queue, or timers.
- **Trigger:** An event that starts the execution of a function. Common triggers include HTTP requests, timer-based schedules, and messages from Azure Storage queues.
- **Binding:** Provides a way for your function to interact with other Azure services. Bindings can be input or output bindings.

### Use Cases

1. **HTTP-Triggered Functions**
   - **Scenario:** A web application needs to process incoming HTTP requests and perform operations based on the request data.
   - **Solution:** Create an HTTP-triggered Azure Function that processes the request and returns a response.
   - **Billing Details:** Charges based on execution time and the number of function invocations. Free grant includes up to 1 million requests and 400,000 GB-seconds of execution time per month.
   - **Commands:**
     ```bash
     # Create a new Function App
     az functionapp create --resource-group <ResourceGroupName> --consumption-plan-location <Location> --runtime <Runtime> --functions-version 3 --name <FunctionAppName> --storage-account <StorageAccountName>

     # Deploy a function to the Function App
     func azure functionapp publish <FunctionAppName>
     ```
   - **YAML Code:**
     ```yaml
     # Function.json for HTTP-triggered function
     {
       "bindings": [
         {
           "authLevel": "function",
           "type": "httpTrigger",
           "direction": "in",
           "methods": ["get", "post"]
         },
         {
           "type": "http",
           "direction": "out"
         }
       ]
     }
     ```

2. **Timer-Triggered Functions**
   - **Scenario:** A task needs to be executed at regular intervals, such as a daily data clean-up operation.
   - **Solution:** Use a timer-triggered Azure Function to execute the task based on a specified schedule.
   - **Billing Details:** Similar to HTTP-triggered functions, billing is based on execution time and invocation count.
   - **Commands:**
     ```bash
     # Create a new timer-triggered function
     func init MyFunctionApp --worker-runtime dotnet
     cd MyFunctionApp
     func new --name TimerFunction --template "Timer trigger"
     ```
   - **YAML Code:**
     ```yaml
     # Function.json for Timer-triggered function
     {
       "bindings": [
         {
           "name": "myTimer",
           "type": "timerTrigger",
           "direction": "in",
           "schedule": "0 */5 * * * *"
         }
       ]
     }
     ```

## Azure Durable Functions

### Overview

Azure Durable Functions is an extension of Azure Functions that enables writing stateful workflows in a serverless environment. It manages state, checkpoints, and restarts for you.

### Architecture

- **Orchestrator Function:** Manages the workflow and coordinates the execution of activity functions. It is responsible for defining the workflow logic.
- **Activity Function:** Performs a unit of work within the workflow. It is invoked by the orchestrator function.
- **Client Function:** Triggers the orchestrator function to start a new instance of the workflow.

### Use Cases

1. **Long-Running Workflows**
   - **Scenario:** An application needs to process a sequence of tasks that can take a long time to complete, such as processing large datasets or running batch jobs.
   - **Solution:** Use a Durable Function to define a workflow with multiple activity functions that can be executed sequentially or in parallel.
   - **Billing Details:** Charges based on the execution time of the orchestrator and activity functions, as well as the number of orchestration and activity function executions.
   - **Commands:**
     ```bash
     # Create a new Durable Function
     func init MyDurableFunctionApp --worker-runtime dotnet
     cd MyDurableFunctionApp
     func new --name OrchestratorFunction --template "Durable Functions Orchestration"
     func new --name ActivityFunction --template "Durable Functions Activity"
     ```
   - **YAML Code:**
     ```yaml
     # OrchestratorFunction.cs
     [FunctionName("OrchestratorFunction")]
     public async Task RunOrchestrator(
         [OrchestrationTrigger] IDurableOrchestrationContext context)
     {
         var outputs = new List<string>();
         var outputs.Add(await context.CallActivityAsync<string>("ActivityFunction", "Tokyo"));
         // other activities
         return outputs;
     }

     # ActivityFunction.cs
     [FunctionName("ActivityFunction")]
     public string Run([ActivityTrigger] string name, ILogger log)
     {
         log.LogInformation($"Hello {name}!");
         return $"Hello {name}!";
     }
     ```

2. **Human-in-the-Loop Workflows**
   - **Scenario:** A process requires manual intervention or approvals, such as processing insurance claims or handling user requests.
   - **Solution:** Use Durable Functions to define a workflow that waits for external input or user actions before proceeding with the next steps.
   - **Billing Details:** Similar to long-running workflows, billing is based on the execution time and number of orchestrations and activities.
   - **Commands:**
     ```bash
     # Initialize Durable Functions with human interaction
     func new --name HumanInteractionOrchestration --template "Durable Functions Orchestration"
     ```

## Billing Details

### Cost Factors

1. **Function Execution Costs:**
   - **Consumption Plan:** Charges based on the number of executions, execution time, and memory usage. Includes a free grant of up to 1 million requests and 400,000 GB-seconds of execution time per month.
   - **Premium Plan:** Provides enhanced performance, VNET integration, and unlimited execution duration. Charges based on the allocated compute resources and execution time.

2. **Durable Function Costs:**
   - **Execution Time:** Charges based on the time taken for orchestrator and activity functions to execute.
   - **Storage Costs:** Durable Functions use Azure Storage for state management, checkpoints, and history. Costs are based on the amount of storage used.

3. **Additional Costs:**
   - **Network Costs:** Data transfer costs associated with inbound and outbound traffic.
   - **Other Services:** Costs for using additional Azure services integrated with Functions, such as Application Insights for monitoring and logging.

For detailed and up-to-date pricing information, refer to the [Azure Pricing Calculator](https://azure.microsoft.com/en-us/pricing/calculator/) and the [Azure Functions pricing page](https://azure.microsoft.com/en-us/pricing/details/functions/).

This README provides a comprehensive overview of Azure Functions and Durable Functions, including their components, architecture, use cases, billing details, and relevant commands and code snippets. It serves as a guide for understanding and managing serverless applications in Azure environments.
