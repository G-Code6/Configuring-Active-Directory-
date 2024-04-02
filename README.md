![Screenshot 2024-03-31 at 1 32 39 PM](https://github.com/G-Code6/Configuring-Active-Directory./assets/163748328/9eba4a1a-b462-40f2-9425-4ab924743cb6)

# Configuring Active Directory



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
- Promote as a DC: Setup a new forest as mydomain.com (can be anything, just remember what it is)
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






