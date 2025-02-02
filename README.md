<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Configuring On-premises Active Directory within Azure VMs Part 1</h1>
This tutorial guides the implementation of Active Directory within Microsoft Azure Virtual Machines. For this tutorial to be completed, you must finish the prerequisites first and come back to this one as it builds upon those.  <br />

<h2>Prerequisites</h2>

- [Setup a Subscription and a Resource in Azure for Beginner Labs](https://github.com/bvongpradith/setup-azure-sub-and-resource)
- [Create Virtual Machines Within Azure and Observe The Network Topology](https://github.com/bvongpradith/creating-azure-vm)

<h2>Technologies and Enviroments Used</h2>

- Microsoft Azure
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Create resources in a resource group in Azure
- Ensure Connectivity between the client and Domain Controller
- Install Active Directory
- Create an Admin and Normal User Account in Active Directory
- Join Client-1 to your domain
- Setup Remote Desktop for non-administrative users on Client-1
- Create additional users and attempt to log into client-1 with one of the users

<h2>Deployment and Set Up</h2>

![Screenshot 2025-01-31 174629](https://github.com/user-attachments/assets/c5ab2be9-b483-4f83-b732-f51a22d2574a)

![Screenshot 2025-01-31 174733](https://github.com/user-attachments/assets/bed5eaa1-92c5-4c0b-8f13-635301ce3e2a)

<p>
First, we'll create the resources needed for this tutorial. I will be naming the resource group "ad-1", the virtual machine "DC-1" and then select the Windows Server 2022. Make sure the size is set to be 2 VCPUs and then create the VM.
</p>
<br />

![Screenshot 2025-01-31 183605](https://github.com/user-attachments/assets/efed5f5b-c607-4a15-aa05-c973ec759814)

![Screenshot 2025-01-31 183641](https://github.com/user-attachments/assets/d2ea1e88-8c85-41a0-9f48-b58df6150de9)

<p>
Make a virtual network for the resource group
</p>
<br />

![Screenshot 2025-01-31 183901](https://github.com/user-attachments/assets/074a82eb-b1ca-4b2b-9180-d9608b1e7349)

![Screenshot 2025-01-31 183943](https://github.com/user-attachments/assets/d6d94633-5b92-4ed8-a364-09afbe12720e)

![Screenshot 2025-01-31 184023](https://github.com/user-attachments/assets/b680c47f-ad77-4b9f-b2ba-af5e288567c6)

![Screenshot 2025-01-31 184050](https://github.com/user-attachments/assets/77ea4bac-0469-4e71-8aea-94ba3f386cc6)

<p>
Make a virtual machine named "dc-1" put in under the same resource group, region, and then select the Windows Server 2022. Make sure the size is set to be 2 VCPUs and at least 8 gb ram then create the VM.
</p>
<br />

![Screenshot 2025-01-31 184540](https://github.com/user-attachments/assets/613f3347-c58a-4057-97c1-7de281656ff9)

![Screenshot 2025-01-31 184611](https://github.com/user-attachments/assets/86a70676-ae38-40e4-a46d-6c4457aff039)

![Screenshot 2025-01-31 184637](https://github.com/user-attachments/assets/615c1524-adbe-4692-92c0-3e9d17b9788f)



<p>
Now we'll create the Windows 10 VM named "Client-1". We must ensure that it is made under the same resource group, region, and have the same size VCPUs and ram of the first VM. It will also need to be in the same Vnet as "DC-1".
</p>
<br />

![Screenshot 2025-01-31 185351](https://github.com/user-attachments/assets/37af0c7c-3110-40b1-83ed-4c8121ef3f27)

<p>
Now go into DC-1 and click into the NIC (network interface card) as shown above.
</p>
<br />

![Screenshot 2025-01-31 185607](https://github.com/user-attachments/assets/a87dad66-d705-4165-a760-8f26cdc04c73)

<p>
Then click into "IP Configurations" and click on "ipconfig1". And Set the IP to static and then click save in the bottom right.
</p>
<br />


![Screenshot 2025-01-31 192525](https://github.com/user-attachments/assets/21f8c0b2-ec7b-4a73-8feb-ee9504f42e5d)

![Screenshot 2025-01-31 192631](https://github.com/user-attachments/assets/0d8b0bbc-9aab-4b6d-bc29-a759661d53a6)

<p>
Now go to the "dc-1" virtual machine and Turn off the firewall in "Active Directory Domain Services", click "Add Features" and then continue to click next until you can install.
</p>
<br />

![Screenshot 2025-01-31 192949](https://github.com/user-attachments/assets/749cef13-d0a5-47b0-9a5b-7f9cbc0c37d5)

![Screenshot 2025-01-31 192849](https://github.com/user-attachments/assets/16b93d96-82c8-4686-91ca-60bcad1c3463)

![Screenshot 2025-01-31 193319](https://github.com/user-attachments/assets/9bd46602-4e18-43a5-8b9c-19b489c389db)

<p>
copy the private IP address of the "dc-1" and then go into client-1 and click into the NIC (network interface card) as shown above.Then go to the DNS server and put the private IP address.
</p>
<br />

![Screenshot 2025-01-31 194535](https://github.com/user-attachments/assets/be3bdf63-c83f-416d-8526-938975f1f557)

![Screenshot 2025-01-31 194719](https://github.com/user-attachments/assets/ab6ccab4-6285-4a84-9417-fc4b65d15ef2)

![Screenshot 2025-01-31 194936](https://github.com/user-attachments/assets/b4780da6-7f48-4004-ba33-1c104cdf70a7)

![Screenshot 2025-01-31 194936](https://github.com/user-attachments/assets/ecc60065-926c-4936-9b11-0610f61fd17c)

<p>
Now go into client-1 and open Powershell to test the connection(ping) with "dc-1".And if you put in ipconfig /all, you see the DNS servers.
</p>
<br />


![Screenshot 2025-01-31 195344](https://github.com/user-attachments/assets/d9a0dc9f-bc25-4c09-b651-96aece16a3f4)

<p>
Finally, we will install Active Directory inside of DC-1. Open up DC-1 and click into "Sever Manager". The first thing we will click is "Add roles and features", press next until we get into "Server Roles", check the box that says "Active Directory Domain Services", click "Add Features" and then continue to click next until you can install.
</p>
<br />

<h1>Stay Tuned for On-premises Active Directory within Azure VMs Part 2</h1>
