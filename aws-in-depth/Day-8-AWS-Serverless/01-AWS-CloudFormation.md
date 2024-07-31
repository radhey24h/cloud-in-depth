# AWS CloudFormation

AWS CloudFormation is a service that allows you to model and set up your Amazon Web Services (AWS) resources so that you can spend less time managing those resources and more time focusing on your applications. With CloudFormation, you can define your infrastructure as code using templates, automate resource provisioning, and manage dependencies.

## CloudFormation Architecture

AWS CloudFormation uses a declarative approach to infrastructure management by defining resources in JSON or YAML templates. Here’s a detailed overview of CloudFormation components and architecture:

### 1. CloudFormation Stack
   - **Description:** A stack is a collection of AWS resources that you create, update, and delete as a single unit. It is based on a CloudFormation template.
   - **Architecture:** 
     - **Stack:** Contains a set of AWS resources specified in a template.
     - **Stack Resources:** The AWS resources that the stack manages, such as EC2 instances, S3 buckets, etc.
   - **Use Case:** Deploy a web application stack that includes EC2 instances, an RDS database, and an S3 bucket.
   - **Billing Details:** Charges are based on the AWS resources created and managed by the stack.
   - **Commands:**
     ```bash
     # Create a new stack
     aws cloudformation create-stack --stack-name <StackName> --template-body file://template.yaml --parameters ParameterKey=InstanceType,ParameterValue=t2.micro

     # Update an existing stack
     aws cloudformation update-stack --stack-name <StackName> --template-body file://template.yaml --parameters ParameterKey=InstanceType,ParameterValue=t2.large

     # Delete a stack
     aws cloudformation delete-stack --stack-name <StackName>
     ```

### 2. CloudFormation Templates
   - **Description:** Templates are JSON or YAML files that describe the AWS resources and their configurations. They define what resources are created and their relationships.
   - **Architecture:** 
     - **Template Structure:** Includes sections like `Resources`, `Parameters`, `Outputs`, and `Mappings`.
   - **Use Case:** Define a template to create an EC2 instance with an attached EBS volume and an S3 bucket.
   - **Billing Details:** No direct cost for templates; costs are incurred based on the resources specified in the template.
   - **YAML Code:**
     ```yaml
     AWSTemplateFormatVersion: '2010-09-09'
     Description: A simple template for creating an EC2 instance and an S3 bucket
     Resources:
       MyEC2Instance:
         Type: AWS::EC2::Instance
         Properties:
           InstanceType: t2.micro
           ImageId: ami-0c55b159cbfafe1f0
       MyS3Bucket:
         Type: AWS::S3::Bucket
         Properties:
           BucketName: my-unique-bucket-name
     ```

### 3. Parameters
   - **Description:** Parameters enable you to customize your template when you create or update a stack. They allow you to pass values into your template.
   - **Architecture:** 
     - **Parameter Definitions:** Include name, type, default value, and allowed values.
   - **Use Case:** Allow users to specify the EC2 instance type when deploying a stack.
   - **Billing Details:** No direct cost for parameters; costs are based on the resources that the parameters influence.
   - **YAML Code:**
     ```yaml
     Parameters:
       InstanceType:
         Description: EC2 instance type
         Type: String
         Default: t2.micro
         AllowedValues:
           - t2.micro
           - t2.small
           - t2.medium
     ```

### 4. Outputs
   - **Description:** Outputs are values that are returned whenever you view your stack's properties or describe it. They can be used to pass information to other stacks or to display information to users.
   - **Architecture:** 
     - **Output Definitions:** Include name, value, and description.
   - **Use Case:** Output the public IP address of an EC2 instance for easy access.
   - **Billing Details:** No direct cost for outputs; costs are associated with the resources output values refer to.
   - **YAML Code:**
     ```yaml
     Outputs:
       InstancePublicIP:
         Description: Public IP address of the EC2 instance
         Value: !GetAtt MyEC2Instance.PublicIp
     ```

### 5. Mappings
   - **Description:** Mappings are fixed variables within your template. They are used to match keys to specific values, useful for conditional logic.
   - **Architecture:** 
     - **Mapping Definitions:** Define key-value pairs for use in the template.
   - **Use Case:** Define mappings for different regions to select the appropriate AMI ID for EC2 instances.
   - **Billing Details:** No direct cost for mappings; costs are based on the resources and their configurations.
   - **YAML Code:**
     ```yaml
     Mappings:
       RegionMap:
         us-east-1:
           AMI: ami-0c55b159cbfafe1f0
         us-west-1:
           AMI: ami-0abcdef1234567890
     ```

### 6. Conditions
   - **Description:** Conditions allow you to create resources based on certain criteria. They enable conditional resource creation or property assignment.
   - **Architecture:** 
     - **Condition Definitions:** Include conditions that evaluate to true or false.
   - **Use Case:** Create an S3 bucket only if a certain parameter is set to `true`.
   - **Billing Details:** No direct cost for conditions; costs are associated with the resources conditionally created.
   - **YAML Code:**
     ```yaml
     Conditions:
       CreateBucket: !Equals [ !Ref Environment, production ]

     Resources:
       MyS3Bucket:
         Type: AWS::S3::Bucket
         Condition: CreateBucket
         Properties:
           BucketName: my-production-bucket
     ```

### 7. Change Sets
   - **Description:** Change sets allow you to preview changes to your stack before applying them. They show what changes will occur and help avoid unintended modifications.
   - **Architecture:** 
     - **Change Set Creation:** Shows the differences between the current stack and the updated template.
   - **Use Case:** Review changes to an EC2 instance type before applying updates to a stack.
   - **Billing Details:** No direct cost for change sets; costs are incurred based on the changes applied to the stack.
   - **Commands:**
     ```bash
     # Create a change set
     aws cloudformation create-change-set --stack-name <StackName> --change-set-name <ChangeSetName> --template-body file://template.yaml --parameters ParameterKey=InstanceType,ParameterValue=t2.large

     # Describe the change set
     aws cloudformation describe-change-set --change-set-name <ChangeSetName> --stack-name <StackName>
     ```

### 8. Stack Sets
   - **Description:** Stack Sets extend the functionality of stacks by allowing you to create and manage stacks across multiple accounts and regions.
   - **Architecture:** 
     - **Stack Set Definition:** Includes the template and parameters to apply across multiple target accounts and regions.
   - **Use Case:** Deploy a common infrastructure setup to multiple AWS accounts and regions.
   - **Billing Details:** Costs include those for creating and managing stacks in multiple regions and accounts.
   - **Commands:**
     ```bash
     # Create a stack set
     aws cloudformation create-stack-set --stack-set-name <StackSetName> --template-body file://template.yaml

     # Create a stack instance
     aws cloudformation create-stack-instances --stack-set-name <StackSetName> --accounts <AccountId> --regions <Region>
     ```

## Billing Details

### Cost Factors

1. **Stack Resources:** Costs are based on the AWS resources created and managed by the stack. This includes EC2 instances, RDS databases, and S3 buckets.
2. **Change Sets:** No direct cost, but the resources affected by change sets are billed according to their usage.
3. **Stack Sets:** Charges for the resources created in each account and region where the stack set is applied.
4. **Template Storage:** No cost for storing templates in S3; however, the resources created by the templates incur costs.

### Pricing Tiers

- **Basic Pricing:** Includes standard charges for the AWS resources used by the stack.
- **Advanced Features:** Additional costs may apply for features like AWS Config or AWS Systems Manager integrations.

For detailed and up-to-date pricing information, refer to the [AWS Pricing Calculator](https://calculator.aws/#/) and the [AWS CloudFormation pricing page](https://aws.amazon.com/cloudformation/pricing/).

This README provides a comprehensive overview of AWS CloudFormation, including its components, architecture, use cases, billing details, and relevant commands and YAML code. It serves as a guide for deploying and managing AWS infrastructure using CloudFormation.
