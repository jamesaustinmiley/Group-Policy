<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Managing Active Directory Accounts through Group Policy</h1>
This tutorial outlines the modification of the client-1 VM so that non-administrative users can log in, the creation of these users, and the configuration of Group Policy so it can manage the Active Directory accounts of these users, specifically the account lockout policies. Active Directory is Microsoft software designed to manage user accounts and their associated properties, such as passwords and permissions, at scale. Group Policy is a feature within AD that is used for configruration. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure 
- Remote Desktop
- Windows PowerShell ISE
- Active Directory Users and Computers
- Group Policy Management Console
- Command Prompt

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 11 (25H2)

<h2>  Steps </h2>

<p>
Log in to the client-1 VM as mydomain.com\jane_admin.
</p>
<p>
<img src="https://imgur.com/tz17RAb.png" alt="client-1"/>
</p>
<p>
Go to Settings, via the Start Menu, and click System. Scroll down and click About. 
</p>
<p>
<img src="https://imgur.com/lkZTIiv.png" alt="System"/>
</p>
<p>
Click Remote Desktop and then Remote Desktop Users. 
</p>
<p>
<img src="https://imgur.com/D3Uc27a.png" alt="Remote Desktop Users"/>
</p>
<p>
Click Select Users that can Remotely Access this PC and click Add.
</p>
<p>
<img src="https://imgur.com/kwW6JJA.png" alt="Select Users"/>
</p>
<p>
Enter Domain Users and click OK twice to allow any non-administrative users who are domain members to log into client-1.
</p>
<p>
<img src="https://imgur.com/fm5mWhC.png" alt="Domain Users"/>
</p>
<p>
<img src="https://imgur.com/uje25l9.png" alt="Remote Desktop Users"/>
</p>
<br />

<p>
Log in to the dc-1 VM as jane_admin.
</p>
<p>
<img src="https://imgur.com/O9H3Soc.png" alt="dc-1"/>
</p>
<p>
Type PowerShell in the Windows Start Menu search bar. Right-click Windows PowerShell ISE and choose Run as Administrator. 
</p>
<p>
<img src="https://imgur.com/WeG0wOs.png" alt="Windows PowerShell ISE"/>
</p>
<p>
Click on the Script down arrow to unveil a text box. Create a new Desktop File in the text box called create-users. Copy a script with code and paste it in the create-users file.  
</p>
<p>
<img src="https://imgur.com/O9SmvVw.png" alt="create-users"/>
</p>
<p>
<img src="https://imgur.com/pB6hx61.png" alt="Code"/>
</p>
<p>
<img src="https://imgur.com/ZEdy7Op.png" alt="text box"/>
</p>
<p>
Click the Run Script button (the yellow arrow) to start creating new users to join Active Directory. Open Active Directory Users and Computers to see the new user accounts in the _EMPLOYEES folder. 
</p>
<p>
<img src="https://imgur.com/zMT6hpp.png" alt="Run Script"/>
</p>
<p>
<img src="https://imgur.com/KiV7Vlv.png" alt="New Users"/>
</p>
<p>
Log in to the client-1 VM with one of the new user accounts (mydomain.com\badaca.ros) to verify the accounts are working. You will see the password for each of the new users is included in the script (Password1). Log out once you are finished. 
</p>
<p>
<img src="https://imgur.com/DidS6Xw.png" alt="Password1"/>
</p>
<p>
<img src="https://imgur.com/MhDKdH6.png" alt="badaca.ros"/>
</p>
<br />

<p>
In dc-1, open the Group Policy Management Console (gpmc.msc), via the Start Menu. GPMC is the control center for rules and settings that get assigned to users and computers across a domain. 
</p>
<p>
<img src="https://imgur.com/w8Hhlin.png" alt="GPMC"/>
</p>
<p>
Right-click Default Domain Policy and click Edit to open the Group Policy Management Editor. 
</p>
<p>
<img src="https://imgur.com/GRAiBXh.png" alt="Group Policy Management Editor"/>
</p>
<p>
Expand Computer Configuration and navigate to the Account Lockout Policy. Click on it to view the primary settings. Click each setting to configure them. 
</p>
<p>
<img src="https://imgur.com/4BDMkV3.png" alt="Account Lockout Policy"/>
</p>
<p>
<img src="https://imgur.com/z4XvRH4.png" alt="ALP Settings"/>
</p>
<p>
Set the Account Lockout Duration to 30 minutes. This is the time that an account remains locked before it is automatically unlocked. 
</p>
<p>
<img src="https://imgur.com/8awVbi5.png" alt="Duration"/>
</p>
<p>
Set the Account Lockout Threshold to 5 invalid logon attempts. This is the number of failed logon attempts that will trigger an account lockout.
</p>
<p>
<img src="https://imgur.com/FkaruHZ.png" alt="Threshold"/>
</p>
<p>
Set the Reset Account Lockout After setting to 10 minutes. This is the  time in minutes after which the failed logon attempts counter is reset to 0, assuming there are no additional failed logon attempts.
</p>
<p>
<img src="https://imgur.com/CXNMKgN.png" alt="Reset"/>
</p>
<p>
<img src="https://imgur.com/32ByPW0.png" alt="ALP Settings 2"/>
</p>
<p>
Log back in to the client-1 VM as jane_admin. 
</p>
<p>
<img src="https://imgur.com/Yxy8bRP.png" alt="Client-1"/>
</p>
<p>
Open Command Prompt, via the Start Menu search bar, and type gpupdate /force to force the update of the account lockout policy for all user accounts. Close Command Prompt when this is done.  
</p>
<p>
<img src="https://imgur.com/c1CPvKD.png" alt="gpupdate"/>
</p>
<p>
Open Command Prompt again and Run as Administrator. Type gpresult /r to see that Default Domain Policy is listed as an Applied Group Policy Object. This means that the account lockout policy was sucessfully applied. 
</p>
<p>
<img src="https://imgur.com/34qZErT.png" alt="Command Prompt Admin"/>
</p>
<p>
<img src="https://imgur.com/ueVvXbs.png" alt="gpresult"/>
</p>
<p>
<img src="https://imgur.com/gLtD306.png" alt="AGPO"/>
</p>
<br />

<p>
