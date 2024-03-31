![Screenshot 2024-03-31 at 1 32 39 PM](https://github.com/G-Code6/Configuring-Active-Directory./assets/163748328/9eba4a1a-b462-40f2-9425-4ab924743cb6)

# Configuring Active Directory



<h3>1. Azure Subscription:</h3> 

- Ensure you have an active Azure subscription. If not, sign up for one.
- Create the Domain Controller VM (Windows Server 2022) named “DC-1”
-  Take note of the Resource Group and Virtual Network (Vnet) that get created at this time
- Set Domain Controller’s NIC Private IP address to be Static
- Create the Client VM (Windows 10) named “Client-1”. 
  Use the same Resource Group and Vnet that was created in Step 1.a
- Ensure that both VMs are in the same Vnet (you can check the topology with Network Watcher

![Screenshot 2024-03-31 at 2 58 34 PM](https://github.com/G-Code6/Configuring-Active-Directory./assets/163748328/0cf44a08-a730-420b-a592-d4ee5a7b9265)

