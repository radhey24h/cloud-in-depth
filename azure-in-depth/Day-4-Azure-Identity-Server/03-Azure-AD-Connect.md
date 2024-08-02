# On Premise AD vs Azure AD
On Premise AD uses NTDS(Jet database), it can add machine to domain, it can apply group policy.
On Premise AD require physical or VM to deploy, and replication is possible between DC's

Azure AD uses SQL database , there is no support to join machine except windows 10 for SSO also there is provision for group policy.
Azure AD  does not require physical or VM to deploy it comes PAAS, and replication is is managed by Azure across 3 region.

# Azure AD Connect
Synchronizing on premise AD users to Azure AD we use AD Connect, we can download this tool and install in any of the member server or any domain controller in our On-Premise Environment

Using the AD connect we can take advantage like:

- User can use a single identity to access on-premises application and cloud services such as Microsoft 365.
- Single tool provide an easy deployment experience for synchronizing and sign in.
- Provides the newest capabilities for your scenario. Azure AD connect replaces older version identity integration tools like DirSync and Azure AD Sync.

## Azure AD Connect Features
Azure AD Connect is a tool that connects on-premises directories with Azure Active Directory, providing a seamless identity experience across environments. Below are the key features of Azure AD Connect:

## 1. Password Hash Synchronization

**Description:**  
Password Hash Synchronization (PHS) synchronizes a hash of the on-premises Active Directory (AD) password to Azure AD. This allows users to use the same password for accessing both on-premises and cloud services like Microsoft Office 365.

**Simple Use Case:**  
Your employees can log in to cloud services like Office 365 using the same password they use for their office computers, making it easier for them to remember their credentials.

## 2. Pass-Through Authentication

**Description:**  
Pass-Through Authentication (PTA) allows users to sign in to both on-premises and cloud applications using the same password, without storing the password or hash in Azure AD. Authentication requests are validated directly against the on-premises AD.

**Simple Use Case:**  
Employees can use their usual office password to access cloud applications, and the verification happens directly on the office network, adding an extra layer of security without additional infrastructure.

## 3. Federated Integration

**Description:**  
Federated integration enables Azure AD to trust an external identity provider for authentication. This typically involves setting up a federation server on-premises, such as Active Directory Federation Services (AD FS).

**Simple Use Case:**  
If your company has complex login requirements, like using smart cards or advanced security methods, federated integration allows all those systems to work together seamlessly.

## 4. Synchronization

**Description:**  
Synchronization ensures that user accounts, groups, and other directory objects are kept in sync between on-premises AD and Azure AD. This includes attributes like usernames, email addresses, and passwords.

**Simple Use Case:**  
When you hire a new employee and add them to the office system, they automatically get access to cloud resources without setting up new accounts, saving time and reducing errors.

## 5. Health Monitoring

**Description:**  
Azure AD Connect Health provides monitoring, alerting, and insights for your on-premises identity infrastructure. It helps identify issues with synchronization, authentication, and overall system health.

**Simple Use Case:**  
IT staff receive alerts if there’s a problem with user logins, allowing them to fix issues before users even notice something is wrong.

## 6. Filtering

**Description:**  
Filtering allows organizations to select which objects (users, groups, etc.) are synchronized from on-premises AD to Azure AD. This can be based on attributes, organizational units, or domains.

**Simple Use Case:**  
You can choose to sync only certain departments or groups to the cloud, ensuring that only relevant users are given cloud access.

## 7. Password Writeback

**Description:**  
Password Writeback allows users to change or reset their passwords in Azure AD, with changes being written back to the on-premises AD. This feature supports self-service password reset capabilities.

**Simple Use Case:**  
Employees can reset their own passwords through a cloud portal, and it automatically updates their office computer login, reducing calls to IT support.

## 8. Device Writeback

**Description:**  
Device Writeback enables Azure AD-joined devices to be registered in on-premises AD. This allows on-premises resources to recognize Azure AD-joined devices and apply conditional access policies.

**Simple Use Case:**  
When employees use their personal devices to access work systems, those devices are recognized and can be managed like office devices, maintaining security.

## 9. Automatic Upgrade

**Description:**  
Automatic Upgrade keeps Azure AD Connect up to date by automatically applying new updates and features. This ensures that the tool remains secure and performs optimally without manual intervention.

**Simple Use Case:**  
Your IT team doesn’t have to worry about manually updating the system, as it automatically stays current with the latest security and feature updates.


## Azure AD Password hash technique.
## Lab 3
**Step 1**

## Azure AD Password Writeback technique.
## Lab 3
**Step 1**



