![Screenshot 2024-03-31 at 1 32 39 PM](https://github.com/G-Code6/Configuring-Active-Directory./assets/163748328/9eba4a1a-b462-40f2-9425-4ab924743cb6)

# Configuring Active Directory Step-by-Step Tutorial

<h3> Prerequisites:</h3>

- Azure Account
- Virtual Machine: Create a VM on Azure
- A Windows Server installed (preferably Windows Server 2022 or later).
- Administrative access to the server.
- Static IP address configured on the server.


<h2>Operating Systems Used </h2>

- Windows 10 / MacOs </b> 

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Computer)
- Remote Desktop
- Windows PowerShell ISE
- Command Prompt


<h3>1. Azure Subscription:</h3> 

- Ensure you have an active Azure subscription. If not, sign up for one.
- Create the Domain Controller VM (Windows Server 2022) named “DC-1”
-  Take note of the Resource Group and Virtual Network (Vnet) that get created at this time
- Set Domain Controller’s NIC Private IP address to be Static
- Create the Client VM (Windows 10) named “Client-1”. 
- Use the same Resource Group and Vnet that was created in "DC-1"
- Ensure that both VMs are in the same Vnet (you can check the topology with Network Watcher

![Screenshot 2024-03-31 at 2 58 34 PM](https://github.com/G-Code6/Configuring-Active-Directory./assets/163748328/0cf44a08-a730-420b-a592-d4ee5a7b9265)

<h3>2. Ensure Connectivity between the client and Domain Controller:</h3>

- Login to Client-1 with Remote Desktop and ping DC-1’s private IP address with ping -t <ip address> (perpetual ping)


![Screenshot 2024-03-31 at 5 03 27 PM](https://github.com/G-Code6/Configuring-Active-Directory./assets/163748328/a399f013-2f29-4fa0-b4aa-6e7bce343f42)


- Login to the Domain Controller and enable ICMPv4 in on the local Windows firewall
![Screenshot 2024-03-31 at 5 19 26 PM](https://github.com/G-Code6/Configuring-Active-Directory./assets/163748328/ed4301a6-9dee-4a5a-b334-613363b7a102)

- Check back at Client-1 to see the ping succeed

<h3>3. Install Active Directory:</h3> 

- Login to DC-1 and install Active Directory Domain Services
- Promote as a DC: Setup a "New Forest" as mydomain.com (can be anything, just remember what it is)
- Restart and then log back into DC-1 as user: mydomain.com\labuser


![Screenshot 2024-03-31 at 6 24 32 PM](https://github.com/G-Code6/Configuring-Active-Directory./assets/163748328/8c39d6f0-1968-448c-bd43-73dccf45d1a8)
![Screenshot 2024-03-31 at 6 26 26 PM](https://github.com/G-Code6/Configuring-Active-Directory./assets/163748328/f37c8575-2736-455e-99a7-98712979f134)

<h3>4. Create an Admin and Normal User Account in AD:</h3> 

- In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”
- Create a new OU named “_ADMINS”
- Create a new employee named “Jane Doe” (same password) with the username of “jane_admin”
- Add jane_admin to the “Domain Admins” Security Group
- Log out/close the Remote Desktop connection to DC-1 and log back in as “mydomain.com\jane_admin”
- User jane_admin as your admin account from now on

![Image 4-1-24 at 7 27 PM (1)](https://github.com/G-Code6/Configuring-Active-Directory./assets/163748328/a2ba4143-f332-4838-a03e-11e07259d97d)
![Image 4-1-24 at 7 47 PM](https://github.com/G-Code6/Configuring-Active-Directory./assets/163748328/9a6769f5-6896-47ed-8be3-b29c3a4a42d0)

<h3>5. Join Client-1 to your domain (mydomain.com):</h3>

- From the Azure Portal, set Client-1’s DNS settings to the DC’s Private IP address
- From the Azure Portal, restart Client-1
- Login to Client-1 (Remote Desktop) as the original local admin (labuser) and join it to the domain (computer will restart)
- Login to the Domain Controller (Remote Desktop) and verify Client-1 shows up in Active Directory Users and Computers (ADUC) inside the “Computers” container on the   root of the domain
- Create a new OU named “_CLIENTS” and drag Client-1 into there

![Image 4-1-24 at 8 15 PM](https://github.com/G-Code6/Configuring-Active-Directory./assets/163748328/58b2ab6f-1418-45a8-9ffe-4b5685a552f6)

<h3>6. Setup Remote Desktop for non-administrative users on Client-1</h3>

- Log into Client-1 as mydomain.com\jane_admin and open system properties
- Click “Remote Desktop”
- Allow “domain users” access to remote desktop
- You can now log into Client-1 as a normal, non-administrative user now

![Screenshot 2024-04-01 at 8 45 09 PM](https://github.com/G-Code6/Configuring-Active-Directory./assets/163748328/c2eff8f4-2bc9-4d39-9ebd-bc786667d9d4)
![Screenshot 2024-04-01 at 8 57 28 PM](https://github.com/G-Code6/Configuring-Active-Directory./assets/163748328/ff5aecb1-042e-4954-bf80-d6a1ee33b50b)

<h3>7. Create a bunch of additional users and attempt to log into client-1 with one of the users</h3>

- Login to DC-1 as jane_admin
- Open PowerShell_ise as an administrator
- Create a new File and paste the contents of the script into it
- Run the script and observe the accounts being created
- When finished, open ADUC and observe the accounts in the appropriate OU
- Attempt to log into Client-1 with one of the accounts (take note of the password in the script)

![Screenshot 2024-04-02 at 8 42 07 PM](https://github.com/G-Code6/Configuring-Active-Directory./assets/163748328/11b6c518-c041-4c1f-bab6-a1a506c9978f)
![Screenshot 2024-04-02 at 8 55 58 PM](https://github.com/G-Code6/Configuring-Active-Directory./assets/163748328/695bb037-3d16-4747-89fc-3aa84f7a1ca6)




