Active Directory Homelab Project


<img width="600" height="500" alt="Screenshot 2025-09-29 at 12 15 56 AM" src="https://github.com/user-attachments/assets/1640f8e2-023e-487f-858d-528aff03abc6" />


Overview

This project is a hands-on homelab setup where I built and managed an Active Directory (AD) environment to simulate a real-world enterprise network. The goal was to strengthen my skills in identity and access management, domain administration, and automation with PowerShell.


Key Features

Configured a Windows Server as a Domain Controller.

Created and managed Active Directory users and groups.

Automated user creation and management tasks using PowerShell scripts.

Connected a client workstation to the domain to test authentication and group policy functionality.

Practiced fundamental administration tasks such as login, permissions, and security configurations.


Tools & Technologies

Windows Server (Active Directory Domain Services)

PowerShell

VirtualBox / VMware (for virtualization)

Windows 10 (client machine)


Key Takeaways

Setting up and administering Active Directory in a controlled environment.

Automating repetitive admin tasks with PowerShell.

Understanding how domain-joined machines interact with Active Directory.

Practical skills applicable to system administration, and cybersecurity roles.


Lab Walk-Through

To accomodate my Domain Controller (DC) on the Virtual Machine, Two network adapters are required. Firstly, a NAT adapter utilizing my home router's IP address to facilitate external connectivity , and secondly, an Internal Network Adapter (VMnet0) to  enable communication with other Virtual Machines. Diplayed in the image below.
<img width="600" height="500" alt="Screenshot 2025-09-29 at 2 59 57 AM" src="https://github.com/user-attachments/assets/23c4eeb8-591b-441e-be96-fdb3b486e3fb" />
<img width="600" height="500" alt="Screenshot 2025-09-29 at 3 00 33 AM" src="https://github.com/user-attachments/assets/db93849a-7ff1-4635-9f6d-2cc05f1e69f9" />

After installing Windows Server 2019 ISO on the Virtual Machine, I did network configuration by renaming the network adapters (External and Internal), that way I can differentiate NAT adapter utilizing my home router's IP address, which is the external network adapter from the internal one which is the Virtual Machine network.
<img width="600" height="5000" alt="VirtualBox_DC_26_09_2025_20_48_56" src="https://github.com/user-attachments/assets/f09a9f0d-dd9a-4e54-bcd7-37deb9824111" />

Next, I configured the Internal network Adapter, by assigning the IP address in the first image (172.16.0.1). I left the default gateway blank since the Domain Controller serves as the gateway. For DNS server configuration, I allocated the IP address in the first image, anticipating Active directory installation, which automatically installs DNS.
<img width="1280" height="720" alt="VirtualBox_DC_26_09_2025_20_49_59" src="https://github.com/user-attachments/assets/3b4cbb8a-6180-4d84-8848-411593e9729b" />

After configuring the network adapters, I move on to renaming the PC from its current default name to "DC" (Domain Controller). This action requires the PC to restart.
<img width="1440" height="599" alt="Screenshot 2025-09-29 at 5 16 17 AM" src="https://github.com/user-attachments/assets/4ef630a0-b828-4bc1-be6c-229d85fc833b" />

After the restart, I then proceed to intalling the active directory domain services (AD DS), to create the domain
<img width="1280" height="720" alt="VirtualBox_DC_26_09_2025_20_56_07" src="https://github.com/user-attachments/assets/147409ca-4f93-486a-8ec3-2d82bc6ed200" />
<img width="1280" height="720" alt="VirtualBox_DC_26_09_2025_21_03_06" src="https://github.com/user-attachments/assets/aae7a0a0-c33f-4a4a-ac66-88496449ea4d" />

After Active Directory Domain Services installation, I have to set up the Post-Deployment Configuration, by promoting the server to the domain controller which is creating the domain, by adding new forest.
<img width="1280" height="720" alt="VirtualBox_DC_26_09_2025_20_59_05" src="https://github.com/user-attachments/assets/3613247a-7f33-4b40-8355-e8be174213c3" />
<img width="1280" height="720" alt="VirtualBox_DC_26_09_2025_20_59_53" src="https://github.com/user-attachments/assets/fad4d8f1-6495-4599-a67c-0ea7782f7989" />

After the server is being promoted to the domain, it enforced a restart, after the restart, you will notice the domain has been successfully created as Ridwan has been added to the admin account, as it now display RIDWAN\Administrator.
<img width="1152" height="864" alt="VirtualBox_DC_26_09_2025_21_14_17" src="https://github.com/user-attachments/assets/bf9326ff-d0c8-46ed-b580-4cbf12e918dd" />

Now instead of using the built admin account, I created a dedicated admin account, by clicking on start, the clicked on Active Directory Users and Computers. Then right clicked on the created domain (Ridwan), then go to 'New', then 'Organization unit'
<img width="1152" height="864" alt="VirtualBox_DC_26_09_2025_21_20_54" src="https://github.com/user-attachments/assets/3c9429fa-37e2-4e80-a3f0-19cae010f812" />
<img width="1152" height="864" alt="VirtualBox_DC_26_09_2025_21_22_02" src="https://github.com/user-attachments/assets/f1ef628a-5098-4b4b-a0d4-5583d8c7e031" />
Then create a new user under the newly created admin
<img width="1152" height="864" alt="VirtualBox_DC_26_09_2025_21_25_14" src="https://github.com/user-attachments/assets/8d0148cd-3670-43ae-a348-090ae4244b1e" />
After inputing the new user informations, hit 'Next', then set a password for the new user. After password input, click on 'Next', then 'Finish'.
<img width="1152" height="864" alt="VirtualBox_DC_26_09_2025_21_26_52" src="https://github.com/user-attachments/assets/f4585d6c-d7c4-4034-b4ff-9729a6e67b4d" />
<img width="1024" height="750" alt="VirtualBox_DC_27_09_2025_00_11_50" src="https://github.com/user-attachments/assets/4295e034-559b-483e-956c-0c6f00e64b99" />
<img width="1024" height="750" alt="VirtualBox_DC_27_09_2025_00_15_20" src="https://github.com/user-attachments/assets/16de664c-ce01-41de-bb83-707b9a6c4e27" />
After creating the dedicated admin account, it still lacks administrative privileges. I have to elevate this new user to Administrator status. To do that, I right clicked on the new user, go to 'Properties', then clicked on 'Member Of', then 'Add', then input 'domain admins' for the object name, then click on 'Check Names', then 'Okay' and 'Apply'.
<img width="1024" height="750" alt="VirtualBox_DC_27_09_2025_00_13_59" src="https://github.com/user-attachments/assets/905ce222-bf6b-461d-a63a-5a9908cc26ae" />
<img width="1024" height="750" alt="VirtualBox_DC_27_09_2025_00_14_38" src="https://github.com/user-attachments/assets/26904ee2-324b-4301-9c0b-26675ba4c6a6" />

To use the new user account, I have to log out of the the domain controller, and sign-in as other user, and log in the domain admin account.
<img width="1024" height="750" alt="VirtualBox_DC_27_09_2025_00_17_33" src="https://github.com/user-attachments/assets/fcf4e4ab-ae42-4890-a4c7-e5882af6da9c" />

Next, I have install and set up the RAS/NAT to allow the windows 10 client to be on the virtual private network and still be able to access internet through the Domain Controller (DC). To do this i will click on add roles and features on the Server Manager, hit 'Next', 'Next', I should be able to see the server, then click on 'Next' again and choose 'Remote Access' for the role, hit 'Next' again, then install routing, by checking 'Routing', then hit 'Add Features', hit 'Next', 'Next', then 'Install'.
<img width="1024" height="750" alt="VirtualBox_DC_27_09_2025_00_19_45" src="https://github.com/user-attachments/assets/0b61e944-3c73-4dbc-8670-e981ade41976" />
<img width="1024" height="750" alt="VirtualBox_DC_27_09_2025_00_20_54" src="https://github.com/user-attachments/assets/7aa23016-f527-4abc-a0d9-430ba01cd856" />
<img width="1024" height="750" alt="VirtualBox_DC_27_09_2025_00_24_17" src="https://github.com/user-attachments/assets/499b6511-ec6b-4b6b-8167-5e6461fb82e8" />
<img width="1024" height="750" alt="VirtualBox_DC_27_09_2025_00_32_01" src="https://github.com/user-attachments/assets/1149c1c1-90d3-476b-ab13-4596f30d9b1c" />



After Roles has been intalled successfully, now, I have to configure the Routing and Remote Access functionality by going to 'Tools', then 'Routing and Remote Access', right click on Domain Controller (DC), then click on 'Configure and Enable Routing and Remote Access', then 'Next', then choose 'Network address translation (NAT)', then click on 'Next'
<img width="1024" height="750" alt="VirtualBox_DC_27_09_2025_00_34_33" src="https://github.com/user-attachments/assets/133e44b8-bb09-4f4c-b573-e010f8aeb835" />

Then under 'Use this public interface to connect to the internet:', choose the internet for the  Network interface, the 'Next', then hit 'Finish'.
<img width="1024" height="750" alt="VirtualBox_DC_27_09_2025_00_36_45" src="https://github.com/user-attachments/assets/8c5e8a50-4efd-45bf-bead-15e6ed2dc3af" />

Now, I need to set up the DHCP server, to allow Windows 10 Client to get an IP address that will let it get on the internet and browse the internet, while on the private internal network. 
To set up the DHCP, I will go back to Domain Controller, click on 'Add Roles and Features ', hit 'Next', confirm the server name, hit 'Next' again, then select 'DHCP Server', and 'Add Features', then, 'Next', 'Next', 'Next', and click 'Install'.
<img width="1024" height="750" alt="VirtualBox_DC_27_09_2025_00_47_59" src="https://github.com/user-attachments/assets/5afc7124-4d99-4900-bc48-3eaf554453c2" />
<img width="1024" height="750" alt="VirtualBox_DC_27_09_2025_00_47_21" src="https://github.com/user-attachments/assets/e85d04ef-93a8-455b-8f13-7f1de096c617" />
<img width="1024" height="750" alt="VirtualBox_DC_27_09_2025_01_12_40" src="https://github.com/user-attachments/assets/cbbde169-4b7c-4e77-92c5-8a1025881c75" />

Now, let's configure the DHCP and establish a scope. DHCP's primary function is to automatically assign IP addresses to computers on the network. The scope I'm creating will allocate IP addresses within the range of 192.168.1.100 to 192.168.1.200, providing DHCP the capability to assign 100 IP addresses effectively. Additionally, I've set the lease duration to 8 days. This lease ensures that once an IP address is assigned, it remains reserved for that device for a specified period. Without it, new devices couldn't obtain IP addresses, hindering their ability to connect to the internet.

To illustrate, consider a scenario like a library offering Wi-Fi access. If patrons typically spend around 2 hours inside, it wouldn't be practical to lease an IP address for 8 days. This would tie up the IP address unnecessarily. In such a case, it's advisable to set the lease duration to under 4 hours and allocate a broader range. However, for a virtual environment like ours, where usage is temporary, the lease duration isn't crucial

To set up the DHCP scope, go to 'Tools', then click 'DHCP', right click the 'IPv4', click 'New Scope', hit 'Next', give it a name, its ideal to  name it after the IP range, so I named is '172.16.0.100-200', then hit 'Next', then enter the IP Address ranges.
<img width="1024" height="750" alt="VirtualBox_DC_27_09_2025_01_19_01" src="https://github.com/user-attachments/assets/32e72920-5781-4895-b7b4-2c49e41557b4" />
<img width="1024" height="750" alt="VirtualBox_DC_27_09_2025_01_21_04" src="https://github.com/user-attachments/assets/864b13aa-a6d9-42cb-a9e2-383f7aa9d6d6" />

After inputing the IP ranges, then hit 'Next', then add IP Address exclusions (which basically means forbidden IP Addresses), then set the Lease Duration (means how long the client computer can have an IP Adrress before it needs to be refreshed), but i didn't set both, since this is just a lab, so I hit 'Next' on both.
<img width="1024" height="750" alt="VirtualBox_DC_27_09_2025_01_24_03" src="https://github.com/user-attachments/assets/115ce74f-1197-4d02-92fc-50a92a7fb558" />
Then I choose Yes to configure DHCP options for the scope, to tell the client computer which server to use for DNS and which one to use for Gateway, for them to be able to get on the internet
<img width="1024" height="750" alt="VirtualBox_DC_27_09_2025_01_25_11" src="https://github.com/user-attachments/assets/5901ca43-65c7-406b-84f5-d4fc9cfa6f24" />
Then I added The domain controller IP Address, which is the IP Address I want the Client's Router to use to connect to the domain.
<img width="1024" height="750" alt="VirtualBox_DC_27_09_2025_01_27_16" src="https://github.com/user-attachments/assets/b6ba204b-9ba9-4df9-829a-ccb49888b63b" />
If the right domain controller IP is added, the domain name and DNS Server should pop-up automatically, which is 'ridwan.com', hit 'Next', then choose 'Yes, I want to activate the scope now', then 'Next' and 'Finish'.
<img width="1024" height="750" alt="VirtualBox_DC_27_09_2025_01_28_22" src="https://github.com/user-attachments/assets/098f5f16-890d-4e2e-9764-94a99b19ef73" />
<img width="1024" height="750" alt="VirtualBox_DC_27_09_2025_01_29_17" src="https://github.com/user-attachments/assets/6084b652-ea54-44ed-be0e-1604f51e2e17" />
Now, we can see that the scope is added.
<img width="1024" height="750" alt="VirtualBox_DC_27_09_2025_01_32_31" src="https://github.com/user-attachments/assets/ff7a6d4a-07a3-468e-9b48-10cfa1b716a6" />

With Active Directory and my Domain Controller properly configured, I utilize a PowerShell script to generate more than 1000 user accounts. 
<img width="1152" height="720" alt="VirtualBox_DC_27_09_2025_02_15_40" src="https://github.com/user-attachments/assets/1638e21a-b2b6-4ad3-91a8-6d67f49b2249" />
