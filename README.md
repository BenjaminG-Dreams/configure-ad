<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Setup Domain Controller in Azure
- Setup Client Machine in Azure
- Install and Configure Active Directory
- Configure Users, OUs, and Group Policies


<h2>Deployment and Configuration Steps</h2>




<p>
STEP 1 : To set up a basic Active Directory environment, begin by creating a Windows Server 2022 VM named "DC-1" as the Domain Controller, ensuring its NIC has a static private IP address, and noting the Resource Group and Virtual Network (Vnet) created. Next, create a Windows 10 VM named "Client-1" using the same Resource Group and Vnet as DC-1. Finally, verify that both VMs are in the same Vnet using Network Watcher and confirm connectivity between the client and Domain Controller, establishing the foundation for your Active Directory infrastructure.
</p>
<p>

<img width="1512" alt="create rs directory 2" src="https://github.com/user-attachments/assets/eda3996e-666c-4c5a-8d63-3f59c8eb2d09" />

<img width="1512" alt="Screenshot 2025-01-19 at 5 06 31 PM" src="https://github.com/user-attachments/assets/20a474d3-7c13-45b6-9926-5d73dc890b16" />


<img width="1512" alt="Screenshot 2025-01-18 at 5 27 21 PM" src="https://github.com/user-attachments/assets/2e1bb8cc-a105-44e3-a32d-dcf00f8de26f" />

</p>
<br />


<p>
STEP 2 : Log into the Domain Controller (DC-1) and install Active Directory Domain Services, promoting the server to a Domain Controller by creating a new forest with the domain name "mydomain.com". After restarting and logging back in as mydomain.com\labuser, use Server Manager to create an administrative account with elevated permissions and a standard user account for typical network access. These actions establish the foundational Active Directory infrastructure and user management framework for the network environment.

</p>
<p>
<img width="1512" alt="Screenshot 2025-01-18 at 8 10 47 PM" src="https://github.com/user-attachments/assets/a0089e37-11e3-4382-8a44-7b2fdeb94441" />

<img width="1512" alt="Screenshot 2025-01-18 at 8 11 48 PM" src="https://github.com/user-attachments/assets/3dd79458-e8e1-4e10-8dac-9108a3d78ee3" />

<img width="1512" alt="Screenshot 2025-01-19 at 2 36 12 PM" src="https://github.com/user-attachments/assets/a50c53b3-ef3c-403b-87b0-16a70b81fef9" />

<img width="1512" alt="Screenshot 2025-01-19 at 2 38 23 PM" src="https://github.com/user-attachments/assets/62812249-3d2d-46c2-82fa-1220c5e166ef" />


</p>
<br />




<p>
Step 3 Focuses on creating organizational units and user accounts in Active Directory, as well as joining a client to the domain. First, use Active Directory Users and Computers (ADUC) to create two organizational units named "_EMPLOYEES" and "_ADMINS", then create a new employee account for "Jane Doe" with the username "jane_admin" and add it to the "Domain Admins" Security Group. Finally, log out of DC-1, log back in as "mydomain.com\jane_admin", and use this account to join Client-1 to the domain (mydomain.com), establishing the basic Active Directory structure and demonstrating domain join functionality
</p>
<p>
<img width="1512" alt="Screenshot 2025-01-19 at 3 04 18 PM" src="https://github.com/user-attachments/assets/75de0c46-0cd6-425b-ad62-4ef74ef085e7" />


<img width="1512" alt="Screenshot 2025-01-19 at 3 12 20 PM" src="https://github.com/user-attachments/assets/119a958f-fdb4-418b-9987-a28d87487e39" />

<img width="1512" alt="Screenshot 2025-01-19 at 3 18 11 PM" src="https://github.com/user-attachments/assets/e4b13fa9-a6ca-4c1f-a873-79a257d69ac9" />

<img width="1512" alt="Screenshot 2025-01-19 at 3 36 03 PM" src="https://github.com/user-attachments/assets/1009a86a-c3a7-4722-a521-0c95b601f04d" />

<img width="1512" alt="Screenshot 2025-01-19 at 3 41 00 PM" src="https://github.com/user-attachments/assets/75b7ec19-e615-4879-a1f4-bae51118a82e" />


</p>
<br />



<p>
In Step 4, join Client-1 to the domain (mydomain.com) by logging in as the local admin (john), changing the computer's domain settings, and restarting the machine to complete domain integration. After the restart, log into the Domain Controller (DC-1) and verify Client-1's presence in Active Directory Users and Computers (ADUC), then create a new Organizational Unit named "_CLIENTS" and move Client-1 into this container for better network organization. Log back into Client-1 as mydomain.com\jane_admin to configure Remote Desktop settings, ensuring that domain users can access the machine remotely. This process establishes proper domain membership, organizational structure, and remote access permissions, creating a foundational network configuration for user connectivity and management.
</p>
<p>
<img width="1512" alt="Screenshot 2025-01-19 at 3 49 07 PM" src="https://github.com/user-attachments/assets/af994f59-5020-4792-95ff-4f95d2111dcd" />

<img width="1512" alt="Screenshot 2025-01-19 at 3 50 03 PM" src="https://github.com/user-attachments/assets/43aa685d-c361-42a4-89d5-3d7b6d4ffa59" />

<img width="1512" alt="Screenshot 2025-01-19 at 3 52 28 PM" src="https://github.com/user-attachments/assets/cb14b889-b45c-4a33-93af-eec7420a9fa7" />

<img width="1512" alt="Screenshot 2025-01-19 at 4 24 05 PM" src="https://github.com/user-attachments/assets/336ad6d4-14aa-44f6-8e03-97606ee615e8" />

</p>
<br />







<p>
In Step 5, log into the Domain Controller (DC-1) as jane_admin and open PowerShell ISE with administrator privileges to execute a user creation script that will generate multiple random user accounts across the domain. Run the script and carefully observe the account generation process, noting the details and passwords for each newly created user account. Open Active Directory Users and Computers (ADUC) to verify that the new accounts have been correctly placed in the appropriate Organizational Unit (OU) with the expected configurations. Finally, attempt to log into Client-1 using one of the newly created user accounts to validate domain connectivity, remote access permissions, and overall network infrastructure functionality.
</p>
<p>

<img width="1512" alt="Screenshot 2025-01-19 at 4 34 22 PM" src="https://github.com/user-attachments/assets/0227c1b5-6917-411e-9a86-4531f47b1217" />

<img width="1512" alt="Screenshot 2025-01-19 at 4 39 05 PM" src="https://github.com/user-attachments/assets/083eecaa-8762-4f05-a996-d9b58e27db8d" />

<img width="1512" alt="Screenshot 2025-01-19 at 4 44 23 PM" src="https://github.com/user-attachments/assets/7f190906-f4d9-4b16-bd5f-10cc01df1dd6" />


<img width="1512" alt="Screenshot 2025-01-19 at 4 47 59 PM" src="https://github.com/user-attachments/assets/7b8bc9b2-ec49-4781-932f-0cdb92a1f323" />

<img width="1512" alt="Screenshot 2025-01-19 at 4 53 32 PM" src="https://github.com/user-attachments/assets/b0e58e13-5594-4170-b889-c61154c90f61" />






</p>
<br />




























