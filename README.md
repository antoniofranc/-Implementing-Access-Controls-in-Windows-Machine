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

6- Right-click the domain  `NDE.com ` and navigate to  `New ` -->  `Organizational Unit `.


<img width="400" height="481" alt="image" src="https://github.com/user-attachments/assets/4ec781c4-4d05-48c8-b4b4-ec12da544582" />

<img width="400" height="556" alt="image" src="https://github.com/user-attachments/assets/20f53a65-6b42-4af3-9f32-27f6bbbc60b0" />

---

7- A `New Object` - `Organizational` Unit pop-up appears. Type `NetworkAdmin` in the `Name` field and click `OK`.

8- Right-click `NetworkAdmin` Organizational Unit, navigate to `New` --> `User`.


<img width="400" height="766" alt="image" src="https://github.com/user-attachments/assets/74fcc8db-74b4-4d7f-b4cf-9a868b7e1dad" />

<img width="400" height="766" alt="image" src="https://github.com/user-attachments/assets/c6e8ff14-127d-44ed-9759-ae360e880031" />

----

9-  `New Object - User ` window appears, enter below details and click  `Next`:

First name: IT

Last name: Head

User logon name: IT_Head

10- Enter test@123 in both the  `Password` and  `Confirm Password ` fields. Uncheck the option  `User must change password at next logon ` and check the option  `Password never expires`. Click Next.

11- In the next window, click `Finish`.

<img width="400" height="665" alt="image" src="https://github.com/user-attachments/assets/d5121348-8803-40bb-93c5-95e184f3c9cf" />

<img width="400" height="657" alt="image" src="https://github.com/user-attachments/assets/911e9db8-ba21-4137-b9b7-f09ae390eba9" />

----

12- Create a global security group within the `NetworkAdmin` Organizational Unit.

13- Right-click the  `NetworkAdmin ` Organizational Unit and navigate to  `New --> Group`.

14- A `New Object - Group` window appears, type `TechSupport` in the `Group name` and click `OK`.



<img width="400" height="685" alt="image" src="https://github.com/user-attachments/assets/0f83a606-0e40-4a02-8e13-9ad0aa02aa82" />

<img width="400" height="684" alt="image" src="https://github.com/user-attachments/assets/a15e2e67-5341-4cbf-b6d9-08a4d8bf1ccf" />

----

15- Now, add the `IT_Head` account to the `TechSupport` group. To do so, right-click `IT_Head` and select `Add to a group`

16- `Select Groups` window appears, in the field `Enter the object names to select`, type `Tech` and click `Check Names` button. The name `TechSupport` appears, click `OK`.

<img width="400" height="687" alt="image" src="https://github.com/user-attachments/assets/9b62c7f6-b4f3-428c-a5c2-efca8fa408ab" />

<img width="400" height="683" alt="image" src="https://github.com/user-attachments/assets/25d189c4-0bc5-488a-84b5-347dca08e59b" />

----

17- A pop-up appears, indicating a successful addition of a user to the group. Click `OK`.

18- right-click the `FinanceOU` Organizational Unit and navigate to `New --> Computer`.

19- `New Object - Computer` window appears, type `Computer01` in the field `Computer Name` field and click `OK`.

20- Switch to the `Administrator: Windows PowerShell` window, type `get-adcomputer -filter * | out-file C:\useraccounts.txt` and press `Enter` to create a detailed report of all computer objects in the domain.

<img width="400" height="682" alt="image" src="https://github.com/user-attachments/assets/3a4475d8-ecc5-401f-b2c4-559d98d75d07" />

<img width="554" height="228" alt="image" src="https://github.com/user-attachments/assets/75a52317-f483-42bc-a1fd-87ce36ff48d2" />

----

21- Navigate to `C:` drive to check whether the file `useraccounts.txt` exists.

22- Double-click the file `useraccounts.txt` to see its contents. The newly created user account (`Computer01`) can be observed, as shown in the screenshot.

<img width="400" height="693" alt="image" src="https://github.com/user-attachments/assets/626ea880-f17c-4708-9324-a4cdb9fc205f" />

<img width="400" height="688" alt="image" src="https://github.com/user-attachments/assets/f45a8b1b-bcc6-4245-a4e9-f784c19f3e7f" />

---

22- Modify the existing GPO in order to set password requirements.

23- To launch `Group Policy Management`, click `Windows Start` icon and navigate to `Windows Administrative Tools` --> `Group Policy Management`.
Alternatively, Group Policy Management can be launched by typing `gpmc.msc` in `Run`. To open Run, right-click on Start and click Run.

24- The main window of `Group Policy Management `appears. Expand the `Forest: NDE.com>Domains>NDE.com ` and select `Default Domain Policy `, as shown in the screenshot.
(The Default Domain Policy is a single password policy that works for all members of a specific domain, it offers no flexibility to have different password polices for different kinds of users. It is recommended that password management is the only use of the Default Domain Policy).

25- `Group Policy Management Console`, click `OK`.

<img width="400" height="686" alt="image" src="https://github.com/user-attachments/assets/4c4f0b16-fe46-4e2b-8502-19119146165a" />

<img width="400" height="686" alt="image" src="https://github.com/user-attachments/assets/3cb34c45-6d0d-4bad-84bc-3bb233119a76" />

-----

26- Right-click `Default Domain Policy` node and select `Edit`

27- In the `Group Policy Management Editor` window, under `Computer Configuration`, expand `Policies --> Windows Settings -> Security Settings --> Account Policies`. Click on `Password Policy`; the password policies will be listed in the right pane.

<img width="400" height="687" alt="image" src="https://github.com/user-attachments/assets/b7a8ded9-3d2a-4b1f-a7bf-02270c511b12" />

<img width="400" height="683" alt="image" src="https://github.com/user-attachments/assets/2678d3ed-da7b-40c3-b106-1e42d530f5bc" />

---
28- Configure the policies to match the requirements are given below. To edit the policy, double-click each of them.

<img width="400" height="181" alt="image" src="https://github.com/user-attachments/assets/3b53fcd3-d801-4752-a2ab-45fa26607648" />

<img width="400" height="603" alt="image" src="https://github.com/user-attachments/assets/92d6ec6e-b90e-4dc9-9b76-5a53f7aa2d09" />

-----

29- Now, switch to the `Administrator: Windows PowerShell`, click to type `gpresult /H C:\passwords-policy-settings.html` and press `Enter` to generate report of the password policy settings to updating configuration documentation

30- Navigate to C: drive to see if passwords-policy-settings.html file exists.

<img width="400" height="400" alt="image" src="https://github.com/user-attachments/assets/729f1c2c-ea99-4120-a2d7-d77f3d7d499f" />

<img width="400" height="400" alt="image" src="https://github.com/user-attachments/assets/187a7a12-4267-49c5-a6e5-2a9cc172f0c2" />

-----

31- Navigate to `C:` drive to see if `passwords-policy-settings.html` file exists.

32- Double click `passwords-policy-settings.html` file.

33- A browser window appears displaying `Group Policy Results` file,

<img width="400" height="400" alt="image" src="https://github.com/user-attachments/assets/8d8ed243-f6e1-4d00-bd81-e9d886b504b3" />

<img width="400" height="400" alt="image" src="https://github.com/user-attachments/assets/75a8150e-f6f6-4b50-a814-7d0256f1dfbd" />

-------
This file displays a detailed report on the implemented account policies. You can explore it further.

# Business Value
This implementation provides:

- Enhanced Security Posture: Enforced strong authentication mechanisms
- Regulatory Compliance: Documented password policies meeting industry standards (NIST, ISO 27001)
- Operational Efficiency: Automated reporting reduces manual audit overhead
- Scalability: OU structure supports organizational growth
- Audit Readiness: Comprehensive logging and reporting capabilities






