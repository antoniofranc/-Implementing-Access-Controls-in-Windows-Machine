<img width="400" height="400" alt="image" src="https://github.com/user-attachments/assets/ba293d46-c3a5-4be2-81ac-12e20ba00fcc" />



# Active Directory Access Control Implementation

## Project Overview
This project demonstrates the implementation of enterprise-level access controls in a Windows Server environment using Active Directory (AD) and Group Policy Objects (GPO). The project showcases critical security administration skills including user management, organizational structure design, and password policy enforcement.

## Technical Environment
- Platform: Windows Server with Active Directory Domain Services
- Domain: NDE.com
- Tools Used:
  - Active Directory Users and Computers (ADUC)
  - Group Policy Management Console (GPMC)
  - PowerShell for automation and reporting
  - pfSense Firewall
  

1- Before implementing access control policies, we will firstly examine the properties of the current Administrator account.

2 - Click `Start` icon in the `Desktop`, right-click `Windows Powershell` and navigate to `More-->Run as Administrator`.

<img width="400" height="497" alt="image" src="https://github.com/user-attachments/assets/b7183888-7f4d-4605-b5f4-999413819d9e" />

---

3- In the Powershell, type whoami /user and press Enter to display details regarding Security ID (SID) and other additional information of the current user.
- User accounts are identified in the system by their unique numbers. In Windows, this number is the Security Identifier (SID). In Linux, it is the User Identifier (UID).

<img width="400" height="497" alt="image" src="https://github.com/user-attachments/assets/5535c06d-10a8-4166-87f0-d5a78c2eb025" />

---
4- Click the `Start` icon in the `Desktop` and select `Server Manager`.

5- The `Server Manager` window appears, click `Tools` and select `Active Directory Users and Computers` option.

6 - Right-click the domain  `NDE.com ` and navigate to  `New ` -->  `Organizational Unit `.


<img width="775" height="481" alt="image" src="https://github.com/user-attachments/assets/4ec781c4-4d05-48c8-b4b4-ec12da544582" />

<img width="775" height="556" alt="image" src="https://github.com/user-attachments/assets/20f53a65-6b42-4af3-9f32-27f6bbbc60b0" />


















