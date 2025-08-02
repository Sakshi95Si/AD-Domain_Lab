# Active Directory Lab

**Objective**

This project aims to set up a basic Active Directory (AD) environment with a domain controller and a client machine joined to the AD domain. The goal is to understand user authentication, group policies, and centralized management of resources within a Windows domain network.

---

**Skills Learned**

* Installing and configuring Windows Server as a Domain Controller  
* Setting up and managing Active Directory Domain Services (AD DS)  
* Joining client machines to an AD domain  
* Creating and managing user accounts, security groups, and organizational units  
* Implementing Group Policies for centralized management  
* Understanding authentication and access control mechanisms in an AD environment

---

**Tools Used**

* Windows Server (for Domain Controller)  
* Windows 10/11 or other client OS (for domain-joined machines)  
* Active Directory Domain Services (AD DS)  
* Active Directory DHCP Services.  
* Remote Desktop Connection (for administration)  
* Virtualization software (Oracle VirtualBox)

![Diagram](screenshots/image1.png) 

**Steps for VM Creation:**

1. Open Oracle virtualbox and click on new to create a virtual machine. In the window give the virtual machine name, select the ISO image from the drop-down and check the skip unattended installation box.  
   ![VMbox](screenshots/image2.png)

2. Next, In hardware allocate base memory and processor for the VM.  
   ![VMbox](screenshots/image3.png) 
     
3. In The Hard Disk, create a virtual hard disk for VM and click Finish.  
     
   ![VMbox](screenshots/image4.png) 
     
     
4. VM will be created with a powered off state. Go to Settings\> Advanced\> in the drop down select bidirectional.  
   ![VMbox](screenshots/image5.png)
     
     
     
5. Next, to the network setting,Enable network adapter attached to NAT. Select Adapter 2 and enable network adapter for internal network. Click OK.  
   ![VMbox](screenshots/image6.png)  
   ![VMbox](screenshots/image7.png)

6. You can view the VM's settings as below. Double click on VM to power it ON.  
   ![VMbox](screenshots/image8.png)

7. VM first powered ON.  
   ![VMbox](screenshots/image9.png) 
     
     
     
     
8. Select the language to install and make sure to select desktop experience in the proceedings.  
   ![VMbox](screenshots/image10.png) 
     
     
     
     
     
   ![VMbox](screenshots/image11.png) 
     
   ![VMbox](screenshots/image12.png)
     
   ![VMbox](screenshots/image13.png)  
     
9. Select the custom option on the screen below and click next to proceed.  
   ![VMbox](screenshots/image14.png) 
     
     
     
     
     
     
     
     
     
     
10. Installation would take some time to complete. Once it's complete you will get a screen to set up the administrator password for the VM.  
    ![VMbox](screenshots/image15.png) 
      
11. Press Ctrl+Alt+Del on the screen below and enter the admin login password on the screen below.  
    ![VMbox](screenshots/image16.png)  
      
12. Rename the machine. Go to windows\>settings\>about\>rename PC. After renaming reboot once.

---
    

**Steps to configure IP Addressing:**

We have 2 NICs for this setup. The internet NIC will get the IP from the home router and for the internal NIC, IP needs to be set up.

1. Go to Networks \> Change network adaptor option  
   ![VMbox](screenshots/image17.png) 
   ![VMbox](screenshots/image18.png) 
     
     
     
     
2. Rename the network adapter accordingly. Here the first one is getting IP from the home router. Rename it to ‘Internet’  
   ![VMbox](screenshots/image19.png) 
   ![VMbox](screenshots/image20.png)

3. For the second adapter, as seen below its not getting any IP, hence it assigned itself the IP address. Rename it to ‘INTERNAL’  
   ![VMbox](screenshots/image21.png)  
     
   ![VMbox](screenshots/image22.png)
     
4. Again, right click on the Internal adapter and select IPV4 option to set IP address.  
   ![VMbox](screenshots/image23.png) 
     
5. Manually enter the IP address as below and click ok.  
   ![VMbox](screenshots/imageX1.png)

---    
   

**Steps to setup Active Directory Domain Services:**

1. Open server manager\>Add roles & Features\> proceed with next until you reach below screen. Select Active directory domain services and DNS service to add features and click next.  
   ![VMbox](screenshots/image25.png)

   Click install.

   ![VMbox](screenshots/image26.png)

   

2. Installation would take some time. After completion, reboot the server once.  
   ![VMbox](screenshots/image27.png) 
     
3. Click on the flag and select promote the server to domain controller.  
   ![VMbox](screenshots/image28.png)
     
     
     
     
     
     
4. Select add new forest and fill the domain name and click next.  
   ![VMbox](screenshots/image29.png) 
     
5. At the below step, set the password.  
   ![VMbox](screenshots/image30.png) 
     
6. Proceed with next until you reach the prerequisite check section and click install.

7. After the installation is complete, the server will restart again.  
   ![VMbox](screenshots/image31.png)

8. After the reboot you’ll see below login window with your domain.  
   ![VMbox](screenshots/image32.png)
     
     
---   
   

**Steps to create domain admin account:**

1. Click on windows\>administrator tools\>Active Directory Users & Computers  
   ![VMbox](screenshots/image33.png)

2. Create an organization unit: domain\>right click(new)\>Organizational unit  
   ![VMbox](screenshots/image34.png)
     
     
   ![VMbox](screenshots/image35.png)
     
3. Right click on Admins(OU)\>new\>Users. Set the user details and password and click Finish to create a user account.  
   ![VMbox](screenshots/image36.png)
     
     
     
     
     
   ![VMbox](screenshots/image37.png) 
   ![VMbox](screenshots/image38.png) 
   ![VMbox](screenshots/image39.png)
     
4. To assign user rights: right click on user\>Properties\>Member Of\>Add\> type ‘Domain admin’\> check names\>Ok\>Apply.  
   ![VMbox](screenshots/image40.png)  
   Sign-off and login with the new account created. (L.Potter@Quantumspace.com)  
     
     
     
     
   ![VMbox](screenshots/image41.png)
   

**\*\*\*The Next component to configure is NAT(Network Address Translation). The purpose of setting this is because when we create a client machine and join it to the domain, we want it to be in the virtual private network of the domain but be able to access the internet as well.\*\*\***

---

**Steps to Create RAS/NAT:**

1. Go to server manager\>Add roles & Features\>Next\>Server roles(select Remote Access)  
   ![VMbox](screenshots/image42.png) 
2. At Role Services\> check routing\>Add features\>Click Next and proceed to the confirmation section (install).  
   ![VMbox](screenshots/image43.png)
      
3. On the server manager, go to Tools\>Routing and Remote Access\>Right click on server name\>Configure\>Next\>Select Network Address Translation\>Next\>Select use this interface to connect to internet option\>Select the internet adapter\>Finish.  
   ![VMbox](screenshots/image44.png)
     
     
     
   ![VMbox](screenshots/image45.png)
   ![VMbox](screenshots/image46.png)
     
     
     
     
     
     
   ![VMbox](screenshots/image47.png)

---


**Steps to create DHCP on Domain Controller:**

1. Server Manager\>Add roles & Features\>At server roles section(check DHCP server)\>Add feature\>Next\>At confirmation section(install).  
   ![VMbox](screenshots/image48.png)  
     
2. Go to Tools\>DHCP\>Expand at domain name\>IPV4\>Right click\>select New Scope\>Next\>Enter the desired name of the scope(here entered IP range)  
   ![VMbox](screenshots/image49.png) 
   ![VMbox](screenshots/image50.png)
     
     
     
     
     
   On the IP Address Range, give the start and end of IP address space, subnet mask and click Next. Skip the Add exclusion section.  
   ![VMbox](screenshots/image51.png) 
     
   Lease Duration section: At this section you Specify how long a client can use an IP address from the scope.  
   ![VMbox](screenshots/image52.png)
     
   In the Router(Gateway) section:Add the domain controller IP here as we have installed NAT & routing in the domain controller.  
   ![VMbox](screenshots/image53.png) 
   ![VMbox](screenshots/image54.png) 
     
   Proceed with Next and finish configuration.  
     
     
     
   Right click IPV4 server option\> Configure options\>select router\>Add DC IP as default gateway.  
   ![VMbox](screenshots/image55.png) 
   ![VMbox](screenshots/image56.png)
     
   After finishing, restart the service again. Right click on domain name\>all tasks\>restart  
     
 


3. Right click on the domain\> Authorize\>again right click and select refresh. You will start seeing the IPV4 in green with the scope assigned.  
   ![VMbox](screenshots/image57.png) 
   ![VMbox](screenshots/image58.png)
     
     
  ---
  

**Steps to create Client machine and domain joining:**

1. In a similar pattern as the windows server creation, follow the same steps for creating a client machine.  
   ![VMbox](screenshots/image59.png)
   ![VMbox](screenshots/image60.png) 
     
     
     
     
   Because we want this device into an internal virtual network of domain which will get its IP from DHCP, hence set the network adapter to internal Networks.  
   ![VMbox](screenshots/image61.png)  
   ![VMbox](screenshots/image62.png) 
     
   Select ‘I don’t have a key’ and in the next section select the win10 Pro option.  
     
     
     
     
   ![VMbox](screenshots/image63.png) 
   Select custom setting\>Next\>install.  
     
   ![VMbox](screenshots/image64.png) 
     
   Machine will be restarted after installation is finished. Once the machine back up, follow the selection as required and select ‘i don’t have internet’.  
     
   ![VMbox](screenshots/image65.png) 
   ![VMbox](screenshots/image66.png)  
   Skip password and uncheck all enabled options in privacy settings(optional)  
   ![VMbox](screenshots/image67.png)
   Run the below test to check the internet network connectivity from the client machine.  
   ![VMbox](screenshots/image68.png)  
   Rename and join the client to domain: Go to windows\>settings\>systems\>About\>Rename this PC(advanced)\>Change\>Rename:Client1 and select domain.  
   ![VMbox](screenshots/image69.png) 
     
   Enter the domain admin account created earlier. Restart the machine.  
     
     
   ![VMbox](screenshots/image70.png) 
   ![VMbox](screenshots/image71.png) 
     
   After joining the machine to domain, check in the DHCP Addresses leases if the machine is visible. Which means, the machine is getting its IP from the DHCP scope set for the domain.  
     
     
     
     
   ![VMbox](screenshots/image72.png)  
     
   On the Users & Computers Admin tool.  
   ![VMbox](screenshots/image73.png) 
     
   Create a normal user account and login in the client machine.  
     
     
     
   ![VMbox](screenshots/image74.png)  
   ![VMbox](screenshots/image75.png) 
     
   First time login will ask to reset the password as per policy.   
     
     
     
     
     
   ![VMbox](screenshots/image76.png)  
   ![VMbox](screenshots/image77.png) 
   
