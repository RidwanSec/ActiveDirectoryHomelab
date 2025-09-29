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

After installing Windows Server 2019 ISO on the Virtual Machine, I did the network configuration, by renaming the network adapters, that way I can differentiate the my home router from the internal on and I assigned the IP address




