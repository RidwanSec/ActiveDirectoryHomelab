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
After creating the dedicated admin account, it still lacks administrative privileges. To do that I have to go active directory to elevate this new user to Administrator status
<img width="1280" height="720" alt="VirtualBox_DC_26_09_2025_20_49_59" src="https://github.com/user-attachments/assets/67d55dd1-319e-4499-b4d9-ca01bec4bc4e" />
