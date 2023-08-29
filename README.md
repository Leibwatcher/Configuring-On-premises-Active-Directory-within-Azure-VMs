# Configuring-On-premises-Active-Directory-within-Azure-VMs
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

1. Domain Controller VM (Windows Server 2022) named “DC-1”

2. Domain Controller’s NIC Private IP address to be static

3. ICMPv4 (ping) was allowed on the Domain Controller

4. Create an Admin and Normal User Account in Active Directory

5. Join Client to domain

6. Attempt to login Client-1 with one of the users


<h2>Deployment and Configuration Steps</h2>

Before begining any lab you must create a Resource group so that the Vitrual Machines you create can be stored. Your VMs that will be created is for the Domain Controller(DC-1) and Virtual Machine(Client-1). The Domain Controller VM will be running Image: Windows Server 2022 Datacenter-x64 Gen2.

![Screenshot 2023-08-24 173900](https://github.com/Leibwatcher/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/137578446/842ba903-dc28-4425-bc2c-10ee3a0c8b38)
For the next create a VM for the Client(Windows 10) name "Client-1" with the same Resource Group and same Vnet. The RG and Vnet must match DC-1

![Screenshot 2023-08-24 173523](https://github.com/Leibwatcher/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/137578446/fa109a2b-de01-499e-befe-5b1dd4793de2)

![Screenshot 2023-08-24 173650](https://github.com/Leibwatcher/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/137578446/7cf26ea9-1108-4615-a6ad-b50e5e2b4aa2)
After both VMs are done creating go to DC-1,Private IP address and set to static. This will allow the IP to stay the same.

![Screenshot 2023-08-10 175951](https://github.com/Leibwatcher/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/137578446/9f4c7a19-751e-460f-9b04-f3a372236d24)

To check for a connection between the client and domain controller by logging in with your username and PW to Client-1 with Remote Desktop Connection(RDP) and ping the DC-1 Private IP address using "-t"(Perpetual ping). The ICMPv4 (ping) was showing it was allowing on Domain Controller's(DC-1) Firewall in Windows Firwall(Core Networking Diagnostics). Then logging back into Client-1 to see if the ping is succesful.

![Annotation 2023-08-10 220707](https://github.com/Leibwatcher/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/137578446/ba9a1848-86bc-4c9e-81e3-f7f2e0ab63be)

Here in this example that shows that the ICMP rule has been allowed on the Windows firwall for inbound traffic:

![Screenshot 2023-08-10 181434](https://github.com/Leibwatcher/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/137578446/15c5a83d-d806-4a5b-af7c-88e238db3330)

Back in DC-1, go and select add roles and features to enable the "Active Directory Domain Services". This promotes the Domain Controller(DC) a new forest as mydomain.com setup. Your Remote Desktop will restart and then you can log back in DC-1 as 
user: mydomain.com/username*

![Screenshot 2023-08-10 182444](https://github.com/Leibwatcher/Configuring-On-premises-Active-Directory-within-Azure-VMs/assets/137578446/72dc078a-e50b-4374-a967-48a13afcb351)

Next, we can create and configure the Organizational units for the admins and employees in Actice Directory(AD)
