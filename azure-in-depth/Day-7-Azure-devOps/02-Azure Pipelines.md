# Azure Pipelines

Azure Pipelines is a cloud service that supports continuous integration and continuous delivery (CI/CD) to build, test, and deploy your code to any platform and cloud. It integrates with various source control systems and supports multiple programming languages and platforms.

## Azure Pipelines Architecture

Azure Pipelines is organized into several key concepts that define how builds and deployments are configured and executed:

### 1. Pipeline
   - **Description:** A pipeline defines the process of building and deploying applications.
   - **Components:**
     - **Stages:** Logical phases of the pipeline, such as Build, Test, and Deploy.
     - **Jobs:** A collection of steps that are executed together on the same agent.
     - **Steps:** Individual tasks or scripts executed in a job.
   - **Use Case:** A software development team sets up a pipeline to automate the build, test, and deployment of their application whenever code changes occur.
   - **Billing Details:** Azure Pipelines offers a free tier of build minutes; additional charges apply for extra minutes and parallel jobs.
   - **YAML Example:**
     ```yaml
     trigger:
     - main

     stages:
     - stage: Build
       jobs:
       - job: BuildJob
         pool:
           vmImage: 'ubuntu-latest'
         steps:
         - script: echo Building...
         - script: dotnet build

     - stage: Test
       jobs:
       - job: TestJob
         pool:
           vmImage: 'ubuntu-latest'
         steps:
         - script: echo Testing...
         - script: dotnet test
     ```

### 2. Stage
   - **Description:** A stage is a way to organize jobs in a pipeline and represents a major phase of the CI/CD process.
   - **Components:**
     - **Jobs:** Each stage can contain multiple jobs that run in parallel or sequentially.
   - **Use Case:** A company uses stages to separate different parts of the CI/CD pipeline, such as building the application in one stage and deploying it in another.
   - **YAML Example:**
     ```yaml
     stages:
     - stage: Build
       jobs:
       - job: BuildJob

     - stage: Deploy
       jobs:
       - job: DeployJob
     ```

### 3. Job
   - **Description:** A job is a collection of steps that run on the same agent. Jobs within a stage can run in parallel or sequence.
   - **Components:**
     - **Steps:** Define the specific tasks or scripts to execute.
   - **Use Case:** A team uses jobs to parallelize the testing of different application components to speed up the pipeline execution.
   - **YAML Example:**
     ```yaml
     jobs:
     - job: TestJob1
       steps:
       - script: echo Running tests for component 1

     - job: TestJob2
       steps:
       - script: echo Running tests for component 2
     ```

### 4. Step
   - **Description:** A step is an individual task or command within a job. Steps can be scripts, tasks, or predefined actions.
   - **Use Case:** A developer uses steps to execute a series of commands to build and package the application code.
   - **YAML Example:**
     ```yaml
     steps:
     - script: echo Compiling code...
     - script: dotnet build
     ```

## Key Concepts

- **Triggers:** Define when the pipeline should run, such as on code changes or scheduled intervals.
- **Agents:** Virtual machines or containers that run the jobs in a pipeline.
- **Artifacts:** Packages or files produced by the pipeline, used for deployments or as build outputs.
- **Variables:** Key-value pairs used to parameterize pipelines and tasks.

## Use Cases of Azure Pipelines

1. **Continuous Integration and Deployment**
   - **Scenario:** A development team wants to automate the building and testing of their application whenever code changes occur.
   - **Solution:** Azure Pipelines automatically triggers builds on code commits, runs tests, and deploys successful builds to production.

2. **Multi-Platform Builds**
   - **Scenario:** A software company develops applications for multiple platforms, including Windows, Linux, and macOS.
   - **Solution:** Azure Pipelines supports cross-platform builds using hosted agents for each platform, streamlining the build process for all environments.

3. **Automated Testing**
   - **Scenario:** A QA team needs to run automated tests on each code change to ensure quality before deployment.
   - **Solution:** Azure Pipelines integrates with testing frameworks to execute automated tests as part of the pipeline, ensuring only passing builds are deployed.

4. **Infrastructure as Code (IAC)**
   - **Scenario:** An organization wants to manage and deploy infrastructure using code.
   - **Solution:** Azure Pipelines can be configured to deploy infrastructure using tools like Terraform or ARM templates, ensuring consistent and repeatable deployments.

## Billing Details

### Cost Factors

1. **Build Minutes:** Charges apply for build minutes beyond the free tier. Parallel jobs are also considered.
2. **Self-Hosted Agents:** No cost for using self-hosted agents, but infrastructure costs are incurred by the user.

### Pricing Tiers

- **Free Tier:** Includes a certain number of build minutes per month for public and private repositories.
- **Additional Minutes:** Charged per minute beyond the free tier. Additional charges apply for concurrent job runs.

For detailed and up-to-date pricing information, refer to the [Azure Pipelines Pricing Page](https://azure.microsoft.com/en-us/pricing/details/devops/pipelines/).

## Setting Up Azure Pipelines

### Steps to Configure

1. **Create a Pipeline:**
   - Navigate to the Azure DevOps Portal.
   - Select your project and go to Pipelines > New Pipeline.
   - Choose your repository and configure the pipeline using YAML or the classic editor.

2. **Define Stages and Jobs:**
   - In your pipeline YAML file, define stages and corresponding jobs.
   - Use templates or inline definitions to specify the tasks for each job.

3. **Configure Triggers:**
   - Define triggers to specify when the pipeline should run, such as on pull requests or scheduled intervals.

4. **Set Up Agent Pools:**
   - Choose between Microsoft-hosted or self-hosted agents.
   - Configure agent pools as needed for different pipeline jobs.

5. **Deploy and Test:**
   - Run the pipeline to build, test, and deploy your application.
   - Monitor pipeline runs and view detailed logs for each step.

This README provides a comprehensive overview of Azure Pipelines, detailing its components, architecture, use cases, YAML examples, and billing information. It serves as a guide for effectively utilizing Azure Pipelines in your development and deployment workflow.
