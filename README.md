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

# Ensure Connectivity between the client and Domain Controller

- Login to Client-1 with Remote Desktop and ping DC-1’s private IP address with ping -t <ip address> (perpetual ping)
![Screenshot 2024-03-31 at 5 03 27 PM](https://github.com/G-Code6/Configuring-Active-Directory./assets/163748328/a399f013-2f29-4fa0-b4aa-6e7bce343f42)


- Login to the Domain Controller and enable ICMPv4 in on the local windows Firewall
![Screenshot 2024-03-31 at 5 19 26 PM](https://github.com/G-Code6/Configuring-Active-Directory./assets/163748328/ed4301a6-9dee-4a5a-b334-613363b7a102)

- Check back at Client-1 to see the ping succeed

