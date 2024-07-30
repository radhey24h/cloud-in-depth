# Azure active directory Roles, RBAC, Custom Roles

## Azure AD Roles
The roles that can manage only azure AD resource, like if you remember in on premises in Active directory we have a role that called Domain Admin that role manage the domain controller in Active directory, that basically create the user manage the password and manage the group policies, Similarly azure AD roles manage azure AD.

Azure AD roles have there own responsibilities, it never impact any other roles responsibilities.
1) **Global Administrator**: 
Manage access to all administrative feature as well as service that are dependent to azure AD.
Assign administrator roles to others.
Reset the password for any used and all other administrator.

2) **User administrator**:
Create and manage all user and groups.
Manage support tickets
Monitor health Service
Change passwords for user, helpdesk administrator and other user administrators

2) **Billing administrator**:
Create subscriptions
Manage subscriptions
Manage support tickets
Monitor health Service

## Azure AD RBAC
Azure role-based access control (Azure RBAC) helps us to manage the access of Azure resources, means what all access is required for a resource read or write, and at what level  access is required role based or group based or subscription level.

A role assignment consists of three elements: security principle, role definition and scope.

1) Security principle
A security principle is an object that represents a **user, group, service principle or managed identity** that is requesting access to azure resources. We can assign a role to any of these security principles.
![Security principle](images/security_principle.png)

2) Role definition
A role definition is a collection of permission and it is JSON based document, it is typically just called a role. A role definition lists the operations that can be performed such as read write and delete, Roles can be high level like owner or specific like virtual machine reader.

![Role definition](images/role_definition.png)
So let us say if we have created a role so which type of definition (owner, reader, contributor) we are going to provide that comes under role definition.

3) Scope
Scope is the set of resources where the access applies to, when we create a role we can further limit the actions allowed by a definition scope.
![alt text](images/scope.png)

This is helpful if you want to make someone a website Contributor, but only for one resource group.

In Azure we can specify a scope at four levels.
1) Management group
2) Subscription
3) Resource group
4) Resource
Scopes are structured in a parent-child relationship

# Lab - 1
## Create an user and provide a role on different level
1) **Step 1**: Create an user(tom) from azure active directory
2) **Step 2**: Create a resource group
3) **Step 3**: Go on resource group -> Access control(IAM)->Add> Add role Assignment->Role(Contributor)->Assign Access to(User, group, or service principle)->Select(created username tom)
4) **Step 4**:We can create another resource group and it will be not accessible to (tom)

We can also create a custom role.

## Custom Roles
If the Azure built-in roles don't meet the specific needs of our organization we can create our own custom roles, just like built in roles and we can assign custom roles to users, groups and service principles at management group, subscription and resource group scopes.
Custom roles can be shared between subscription that trust the same azure AD directory, there is a limit of 5000 custom roles per directory.

- **Prerequisites**
To create custom roles we need :
- Permission to create custom role, such as Owner or User Access Administrator

**use case** - customized laptop, customised clothe

# Lab - 2
## Create a custom Role
1) **Step 1**: Go to Subscription-> Roles (here all built-in roles are available)->Add->Add Custom Role
2) **Step 2**: Add Custom Role->Basics->Custom Role Name->Start from Scratch->Next
3) **Step 3**: Add permission->Compute(Microsoft Compute)->go to virtual machine section(Start Virtual Permission)
4) **Step 4**: Add permission->Compute(Microsoft Storage)->go to Storage section(Delete Storage Account)
5) **Step 5**: Add scope (Management Group, Subscription level, resource group or resource)

## Create a custom Role using PowerShell
We have to write the below commands to create the new custom role

first we need to open local PowerShell in admin mode

**Step 1**: connect-AzAccount -> need to put credentials

**Step 2**: New-AzRoleDefinition -InputFile "custom-role.JSON"

Below command will assign the permissions to the user on newly created custom role on the resource group

**Step 3**: New-AzRoleAssignment -ResourceGroupName "RGNAME" -SignInName USER ID -RoleDefinitionName "ROLE NAME"

Now we can go in resource group -> IAM and we can see the assigned roles here.

