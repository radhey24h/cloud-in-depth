# Azure DevOps

Azure DevOps is a set of development tools and services provided by Microsoft Azure to support the entire software development lifecycle. It offers a wide range of services, including source control, continuous integration and delivery, and project management, enabling teams to plan smarter, collaborate better, and ship faster.

## Azure DevOps Architecture

Azure DevOps is structured around several core services that facilitate different aspects of the software development lifecycle:

### 1. Azure Repos
   - **Description:** Provides version control for source code, supporting both Git and Team Foundation Version Control (TFVC).
   - **Architecture:**
     - **Git Repositories:** Distributed version control system for managing code.
     - **TFVC Repositories:** Centralized version control system.
   - **Use Case:** A development team uses Azure Repos to manage their application's source code, allowing for collaboration and version tracking.
   - **Billing Details:** Azure Repos is generally included with Azure DevOps Services. Charges apply based on user licenses.
   - **Commands:**
     ```bash
     # Clone a Git repository
     git clone <repo-url>

     # Commit changes
     git commit -m "Commit message"

     # Push changes
     git push
     ```

### 2. Azure Pipelines
   - **Description:** A cloud service for continuous integration and delivery (CI/CD) that supports building, testing, and deploying code to any platform.
   - **Architecture:**
     - **Build Pipelines:** Automate the compilation and testing of code.
     - **Release Pipelines:** Manage deployments to different environments.
   - **Use Case:** An organization uses Azure Pipelines to automatically build and test code whenever changes are made, and to deploy applications to production environments.
   - **Billing Details:** Offers a certain amount of free build minutes per month; additional charges apply beyond that.
   - **YAML Code:**
     ```yaml
     trigger:
     - main

     jobs:
     - job: Build
       pool:
         vmImage: 'ubuntu-latest'
       steps:
       - task: DotNetCoreCLI@2
         inputs:
           command: 'build'
           projects: '**/*.csproj'
     ```

### 3. Azure Boards
   - **Description:** Provides agile planning and project management tools, including Kanban and Scrum boards, backlogs, dashboards, and reporting.
   - **Architecture:**
     - **Work Items:** Track tasks, bugs, features, and user stories.
     - **Boards and Backlogs:** Organize and prioritize work.
   - **Use Case:** A product team uses Azure Boards to manage their backlog, track progress, and collaborate on features and bug fixes.
   - **Billing Details:** Azure Boards is included with Azure DevOps Services. Pricing is based on user licenses.
   - **Commands:** N/A (primarily accessed via the Azure DevOps web interface).

### 4. Azure Artifacts
   - **Description:** A package management solution that enables teams to create, host, and share packages, such as Maven, NPM, NuGet, and Python.
   - **Architecture:**
     - **Feeds:** Organize and manage packages.
     - **Package Management:** Support for multiple package types.
   - **Use Case:** A development team uses Azure Artifacts to manage dependencies and share internal packages across projects.
   - **Billing Details:** Free tier includes a certain amount of storage; additional charges apply based on storage and usage.
   - **Commands:**
     ```bash
     # Publish a package
     dotnet nuget push <package-file> -s <feed-url>

     # Install a package
     npm install <package-name> --registry <registry-url>
     ```

### 5. Azure Test Plans
   - **Description:** Provides tools for planned and exploratory testing to ensure quality throughout the development process.
   - **Architecture:**
     - **Test Suites:** Organize test cases for execution.
     - **Test Plans:** Define the scope and criteria for testing.
   - **Use Case:** A QA team uses Azure Test Plans to manage and execute test cases, ensuring that new releases meet quality standards.
   - **Billing Details:** Azure Test Plans are priced based on user licenses.
   - **Commands:** N/A (primarily accessed via the Azure DevOps web interface).

## Billing Details

### Cost Factors

1. **User Licenses:** Pricing is based on the number of users and access levels (Basic, Basic + Test Plans, etc.).
2. **Build and Release Pipelines:** Includes free tier build minutes, with additional charges for extra minutes and parallel jobs.
3. **Artifacts:** Charges apply based on storage and number of package downloads beyond the free tier.
4. **Test Plans:** Pricing based on user licenses and test execution requirements.

### Pricing Tiers

- **Basic Pricing:** Includes access to Azure Repos, Azure Boards, and Azure Pipelines with limited build minutes.
- **Advanced Features:** Additional charges for Azure Artifacts storage, Azure Test Plans, and extended build minutes.

For detailed and up-to-date pricing information, refer to the [Azure DevOps Pricing Page](https://azure.microsoft.com/en-us/pricing/details/devops/).

## Setting Up Azure DevOps

### Steps to Configure

1. **Create an Azure DevOps Organization:**
   - Navigate to the [Azure DevOps Portal](https://dev.azure.com/).
   - Sign in with your Microsoft account.
   - Create a new organization and project.

2. **Set Up Azure Repos:**
   - Navigate to Repos in your Azure DevOps project.
   - Create a new Git or TFVC repository.
   - Clone the repository locally using the Git URL.

3. **Configure Azure Pipelines:**
   - Navigate to Pipelines in your Azure DevOps project.
   - Create a new pipeline and connect it to your repository.
   - Define your build and release pipeline using YAML or the classic editor.

4. **Utilize Azure Boards:**
   - Navigate to Boards in your Azure DevOps project.
   - Create and manage work items, backlogs, and sprints.
   - Use Kanban or Scrum boards to track progress.

5. **Manage Packages with Azure Artifacts:**
   - Navigate to Artifacts in your Azure DevOps project.
   - Create a new feed to host your packages.
   - Publish and consume packages using supported package managers.

6. **Plan and Execute Tests with Azure Test Plans:**
   - Navigate to Test Plans in your Azure DevOps project.
   - Define test plans and create test cases.
   - Execute manual and exploratory tests.

This README provides a comprehensive overview of Azure DevOps, detailing its components, architecture, use cases, and billing information. It serves as a guide for effectively utilizing Azure DevOps services in your development workflow.
