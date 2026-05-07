# Active Directory Home Lab (IT Support Demo)
This project demonstrates a basic enterprise IT environment using Active Directory.
It includes user management, organizational unit (OU) structure, Group Policy Objects (GPO), roaming profiles, and file sharing configuration.
The lab simulates real-world IT support tasks such as user setup, permissions management, and troubleshooting.

Lab Environment
- Windows Server 2025 (Domain Controller)
- Windows 11 Client (Domain Joined)
- Active Directory Domain Services (AD DS)
- VMware Workstation

Key Features
- Created Organizational Units (OU) for departments (IT, HR, etc.)
- Managed users and security groups
- Configured Group Policy (GPO) for drive mapping
- Implemented file server with NTFS permissions
- Set up roaming profiles
- Distribution of notepad++ & chrome

Simple Architecture Diagram
 <br>A  [Windows Server 2025 - DC] --> B  [Windows 11 Client 1]
 <br>A --> C  [Windows 11 Client 2]
 <br>A --> D  [File Server - Profiles$ / Shares]


## Skills Demonstrated
- Active Directory Administration
- User and Group Management
- NTFS Permissions
- Share Permissions
- Group Policy Management
- Windows Networking
- DNS Configuration
- Troubleshooting

## Part 1 - Organizational Hierarchy & Identity

![image alt](https://github.com/louis00650/ActiveDirectory-Lab-ITSupport/blob/a172d3c5b20eb9daa6948085cd1686df79cfa1c3/Computer.png) 
<br>In this view of Active Directory Users and Computers (ADUC), I established a logical Organizational Unit (OU) structure for the HappySystem.local domain. By categorizing objects into dedicated OUs for Departments, Groups, and Computers, I created a framework that allows for precise Group Policy targeting and simplified administrative delegation.

![image alt](https://github.com/louis00650/ActiveDirectory-Lab-ITSupport/blob/a172d3c5b20eb9daa6948085cd1686df79cfa1c3/Group%26DistributionList.png) 
<br>Here, I managed the distinction between Security Groups (used for assigning NTFS and Share permissions) and Distribution Lists (used for departmental communication). This demonstrates an understanding of Role-Based Access Control (RBAC), ensuring that users only receive the access levels required for their specific job functions.

![image alt](https://github.com/louis00650/ActiveDirectory-Lab-ITSupport/blob/a172d3c5b20eb9daa6948085cd1686df79cfa1c3/Users_HRDDept.png) 
![image alt](https://github.com/louis00650/ActiveDirectory-Lab-ITSupport/blob/a172d3c5b20eb9daa6948085cd1686df79cfa1c3/Users_ITDept_Sales.png)
<br>These screenshots show the populated user accounts within their respective departmental OUs. Creating standardized user objects is the first step in centralizing identity management, allowing for automated provisioning of resources like email and home folders based on the user's location in the directory.

## Part 2 - Security & Governance

![image alt](https://github.com/louis00650/ActiveDirectory-Lab-ITSupport/blob/a172d3c5b20eb9daa6948085cd1686df79cfa1c3/PasswordPolicy.png) 
<br>Security starts with identity protection. I configured the Default Domain Password Policy to enforce modern security standards, including password complexity, a 180-day maximum age, and history enforcement. This ensures the environment is resilient against basic brute-force and credential-stuffing attacks.

![image alt](https://github.com/louis00650/ActiveDirectory-Lab-ITSupport/blob/a172d3c5b20eb9daa6948085cd1686df79cfa1c3/DisableUSB.png) 
<br>To mitigate the risk of data exfiltration and the introduction of unauthorized software via hardware, I implemented a Group Policy Object (GPO) to disable Removable Storage Access. This endpoint security measure restricts USB storage devices while still allowing essential peripherals like keyboards and mice.

![image alt](https://github.com/louis00650/ActiveDirectory-Lab-ITSupport/blob/a172d3c5b20eb9daa6948085cd1686df79cfa1c3/GroupPolicyOverview.png)
<br>The Group Policy Management Console (GPMC) acts as the "brain" of the domain. This overview shows the various GPOs I’ve authored and linked to specific OUs. It highlights the centralized nature of Windows Administration—changing a single setting here updates security and configurations across every machine on the network instantly.

## Part 3 - Automation & Resource Provisioning

![image alt](https://github.com/louis00650/ActiveDirectory-Lab-ITSupport/blob/a172d3c5b20eb9daa6948085cd1686df79cfa1c3/MapShareDrive.png)  
<br>To improve user productivity, I used Group Policy Preferences (GPP) to automatically map a shared network drive (Y:) upon login. This replaces the need for manual mapping or legacy login scripts, ensuring that every employee has immediate access to their team's data as soon as they sign in.

![image alt](https://github.com/louis00650/ActiveDirectory-Lab-ITSupport/blob/a172d3c5b20eb9daa6948085cd1686df79cfa1c3/SoftwareInstallPolicy.png) 
<br>This illustrates "Zero-Touch" deployment using GPO Software Installation. I configured the server to automatically push and install essential applications—such as Google Chrome and Notepad++—to all client workstations. This ensures a standardized software environment across the entire organization.

![image alt](https://github.com/louis00650/ActiveDirectory-Lab-ITSupport/blob/a172d3c5b20eb9daa6948085cd1686df79cfa1c3/VmMachine.png) 
<br>This high-level view of the VMware Workstation environment shows the lab's infrastructure. It includes the Windows Server 2025 Domain Controller and Windows 11 client machines. Building this virtual network required configuring virtual switches and static IP addressing to ensure seamless communication between the server and its clients.

## Part 4 - Data Mobility (Roaming Profiles)

![image alt](https://github.com/louis00650/ActiveDirectory-Lab-ITSupport/blob/a172d3c5b20eb9daa6948085cd1686df79cfa1c3/RoamingProfilesPolicy.png) 
<br>I configured the User Profile Path policy to enable Roaming Profiles. This ensures that a user’s desktop, documents, and application settings "follow" them to any computer they log into within the domain, which is a critical feature for hot-desking or multi-office environments.

![image alt](https://github.com/louis00650/ActiveDirectory-Lab-ITSupport/blob/a172d3c5b20eb9daa6948085cd1686df79cfa1c3/ADRoamingProfile2.png) 
![image alt](https://github.com/louis00650/ActiveDirectory-Lab-ITSupport/blob/a172d3c5b20eb9daa6948085cd1686df79cfa1c3/ADRoamingProfile3.png) 
<br>These windows show the critical balance between Share Permissions and NTFS Permissions. By setting the share to "Everyone: Full Control" and using advanced NTFS permissions for "Authenticated Users," I created a secure root folder where the system can create individual user profiles while preventing users from accessing each other's private data.

![image alt](https://github.com/louis00650/ActiveDirectory-Lab-ITSupport/blob/a172d3c5b20eb9daa6948085cd1686df79cfa1c3/ADRoamingProfile1.png) 
<br>This is the server-side verification of the roaming profile system. You can see the .V6 profile folders automatically generated by the system as users log in. This confirms that the synchronization between the Windows 11 clients and the Server 2025 storage is functioning

## Part 5 ShareDrive

![image alt](https://github.com/louis00650/ActiveDirectory-Lab-ITSupport/blob/a172d3c5b20eb9daa6948085cd1686df79cfa1c3/BerryShareDrive.png) 
A client-side "Proof of Concept." This view from a user workstation confirms that the Mapped Drive is visible and that the user can only see and access the specific folders permitted by their group memberships.Access-based enumeration enabled to hide the folders that the user had no permission.

## What I Learned ?
- How to design OU structure
- How to apply GPOs safely
- How NTFS inheritance works
- How roaming profiles behave
- How to secure file share

