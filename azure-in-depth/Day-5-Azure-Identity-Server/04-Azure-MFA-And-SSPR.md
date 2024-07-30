
## Multifactor Authentication
Multifactor Authentication is a process where a user is prompted during the sign-in process for an additional form of identification, such as to enter a code on their cell phone or to provide a fingerprint scan.
If we only use a password to authenticate an user , it leave an insecure vector for attack.

Azure multi-factor authentication works by requiring two or more of the following authentication method. 
1) password
2) any trusted device that is not easily duplicated like a phone or a hardware key.
3) biomatrices like a fingerprint or face scan.

**Use Case**: Like security in our office, when we enter in our office there is main gate security, after one level of scan we use another level of scan to enter in project development area.

## Lab 4a
**Step 1** Azure Active Directory-> Users-> Create An User -> Select Multifactor Authentication
**Step 2** Select User -> Enable
**Step 3** now open incognito and login with new user

## Lab 4b Advance Settings
**Step 1** Azure Active Directory-> Users-> Create An User -> Select Multifactor Authentication
**Step 2** Select User -> Enable
**Step 3** now open incognito and login with new user

## Custom Domain
We can add custom domain name in 
## Lab 
**Step 1** Add new custom domain-> create txt type record and map with domain provider in DNS section


## Azure AD join
We can join and register devices with azure AD join, this is good when employee bring their own devices.
We can configure azure AD registered device with WINDOWS 10, IOS, Android and MacOS (Except Windows Server).

**Enterprise state roaming** - This feature is only available with premium tier, using this feature user can securely synchronize their user settings and application setting data to the cloud.
## Lab 
**Step 1** Add 

## Azure AD dynamic groups

## Azure Active Directory Self-Service Password Reset (SSPR)

Azure Active Directory Self-Service Password Reset (SSPR) is a feature that allows users to reset their passwords without needing to contact the IT helpdesk. This feature enhances security and user experience by providing a simple, secure method for users to manage their own passwords.

### Key Features

- **User Empowerment**: Users can reset their passwords and unlock their accounts anytime, anywhere.
- **Secure Authentication**: SSPR uses multi-factor authentication (MFA) to verify user identity before allowing a password reset.
- **Customizable Policies**: Organizations can configure the reset process to meet their security and compliance requirements.

### Simple Use Case

**Scenario:**  
A medium-sized company has many remote employees who occasionally forget their passwords. These employees often need to contact IT support, which can delay their ability to work, especially outside of regular business hours.

**Solution:**  
With Azure AD SSPR, remote employees can reset their passwords themselves through a secure web portal. The system asks for additional verification, such as a code sent to their phone or an email link. Once verified, they can set a new password.

**Benefits:**

- **Reduced IT Burden**: Fewer password reset requests allow IT staff to focus on more critical tasks.
- **Improved Productivity**: Employees can quickly regain access to their accounts without waiting for IT support.
- **Enhanced Security**: By using MFA, SSPR ensures that only the rightful owner of the account can reset the password.

### How It Works

1. **Verification**: When a user forgets their password, they visit the SSPR portal and verify their identity using predefined methods (e.g., phone, email).
   
2. **Reset**: After successful verification, the user is allowed to reset their password.

3. **Confirmation**: The system confirms the password change and notifies the user, ensuring they can immediately regain access to their account.

By enabling SSPR, organizations can enhance their security posture while providing users with a more convenient way to manage their credentials.

## Lab SSPR
**Step 1**: Prerequisite
1) MFA should be enabled
2) Azure AD Premium licence should be active as AD level
3) Azure AD Premium licence should be assigned at user level
4) User should be member of Azure AD Group
**Step 2**:Active Directory-> User


## Azure AD Create/Delete bulk Users
## Lab ->
**Step 1**: Azure Active directory -> users -> Bulk Operation Create-> Import and edit the file and upload.
**Step 1**: Azure Active directory -> users -> Bulk Operation Delete-> Import and edit the file and upload.


## Azure AD Conditional Access
## Lab ->
**Step 1**: Need to enable Premium P2


## Azure Application Proxy

Azure Application Proxy is a service that allows you to provide secure remote access to on-premises web applications. It acts as a bridge between users and your internal resources, ensuring secure connectivity without the need for a traditional VPN.

### Key Features

- **Secure Remote Access**: Provides users with secure access to on-premises applications from anywhere in the world.
- **Integration with Azure AD**: Leverages Azure Active Directory for authentication, enabling single sign-on (SSO) and multi-factor authentication (MFA).
- **Easy Deployment**: Requires no changes to your on-premises applications and can be set up quickly.
- **Security and Compliance**: Protects against malicious attacks and helps meet compliance requirements by controlling access to internal resources.

### Simple Use Case

**Scenario:**  
A company has an internal HR application that employees need to access remotely. Traditionally, this required setting up a VPN, which was complex and required additional resources to maintain.

**Solution:**  
The company uses Azure Application Proxy to make the HR application available over the internet. Employees can access it securely without needing a VPN by logging in through a web portal using their Azure AD credentials.

**Benefits:**

- **Reduced Complexity**: Eliminates the need for a complex VPN setup, reducing maintenance and infrastructure costs.
- **Improved Security**: By using Azure AD, the application benefits from advanced security features like MFA, protecting sensitive HR data.
- **Enhanced User Experience**: Employees enjoy seamless access to the HR application with SSO, improving productivity and satisfaction.

### How It Works

1. **User Access**: Users log in to a web portal using their Azure AD credentials.
   
2. **Authentication**: Azure AD authenticates the users, applying any configured security policies, such as MFA.

3. **Proxy Request**: Azure Application Proxy routes the request to the on-premises application, maintaining a secure connection.

4. **Access Granted**: Users can now interact with the application as if they were on the internal network, without needing a VPN.

Azure Application Proxy simplifies remote access to on-premises applications while enhancing security and user experience.