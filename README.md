<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Creating Users and Managing Active Directory Accounts</h1>
This tutorial outlines the modification of the client-1 VM so that non-administrative users can log in, the creation of these users, the configuration of Group Policy so it can manage the Active Directory accounts of these users, specifically the account lockout policies, and setting permissions for folders within Active Directory. Active Directory is Microsoft software designed to manage user accounts and their associated properties, such as passwords and permissions, at scale. Group Policy is a feature within AD that is used for configruration. <br />


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
Expand Computer Configuration and navigate to the Account Lockout Policy. 
</p>
<p>
<img src="https://imgur.com/4BDMkV3.png" alt="Account Lockout Policy"/>
</p>
<p>
Click on Account Lockout Policy to view the primary settings. Click each setting to configure them. 
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
Open Command Prompt again and Run as Administrator. Type gpresult /r to see that Default Domain Policy is listed as an Applied Group Policy Object. This means that the Account Lockout Policy was sucessfully applied. 
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
<p>
A way to test the Account Lockout Policy is to attempt to log into one of the user accounts (badaca.ros) five times with the wrong password. When you attempt to log in for a sixth time you should recieve a notice that the account has been locked. 
</p>
<p>
<img src="https://imgur.com/YLeluPI.png" alt="Lockout"/>
</p>
<p>
Double-click the user account name and click on the Account tab to be able to unlock the account by checking the box, clicking Apply, and clicking OK. 
</p>
<p>
<img src="https://imgur.com/aeOGKiw.png" alt="Unlock"/>
</p>
<p>
A quick way to find an account in Active Directory Users and Computers is to right-click mydomain.com, click Find, and enter the account name.
</p>
<p>
<img src="https://imgur.com/kXfhXXM.png" alt="Find"/>
</p>
<br />

<p>
To reset the password of a user account in ADUC, right-click the account name, click Reset Password, and enter the new password. 
</p>
<p>
<img src="https://imgur.com/BDUq39l.png" alt="Reset Password"/>
</p>
<p>
<img src="https://imgur.com/DgyGE3n.png" alt="New Password"/>
</p>
<p>
To disable a user account in ADUC, right-click the account name and click Disable Account. When you attempt to log in to the account you will recieve a message stating that the account is disabled. 
</p>
<p>
<img src="https://imgur.com/ahQXm9Y.png" alt="Disable Account"/>
</p>
<p>
<img src="https://imgur.com/yg5DFaE.png" alt="Account Disabled"/>
</p>
<p>
To enable the user account in ADUC, right-click the account name and click Enable Account. 
</p>
<p>
<img src="https://imgur.com/FAScbHG.png" alt="Enable Account"/>
</p>
<br />

<p>
Log in to the dc-1 VM as your domain admin account (mydomain.com\jane_admin).
</p>
<p>
<img src="https://imgur.com/iVYJU6m.png" alt="domain admin"/>
</p>
<p>
Open Active Directory Users and Computers and select a user account in the EMPLOYEES folder (badaca.ros).
</p>
<p>
<img src="https://imgur.com/4kksRGa.png" alt="badaca.ros"/>
</p>
<p>
Log in to the client-1 VM with the user account you selected (badaca.ros).
</p>
<p>
<img src="https://imgur.com/CLE52bF.png" alt="client-1"/>
</p>
<p>
Back in the dc-1 VM, open File Explorer and navigate to the Windows C Drive. 
</p>
<p>
<img src="https://imgur.com/090kzcl.png" alt="C Drive"/>
</p>
<p>
Create four new folders within Windows C Drive by right-clicking beneath the C Drive contents, clicking New, and then Folder. 
</p>
<p>
<img src="https://imgur.com/Z8IbZPC.png" alt="New Folder"/>
</p>
<p>
The four new folders will be called read-access, write-access, no-access, and accounting. 
</p>
<p>
<img src="https://imgur.com/lm4CbVD.png" alt="New Folders"/>
</p>
<p>
Set permissions to the read-access, write-access, and no-access folders by right-clicking the folder and selecting Properties. 
</p>
<p>
<img src="https://imgur.com/5bmwX4C.png" alt="Properties"/>
</p>
<p>
Navigate to the Sharing tab and click Share. 
</p>
<p>
<img src="https://imgur.com/Z6AStGr.png" alt="Share"/>
</p>
<p>
For the read-access folder, Domain Users will be allowed to read the contents of the folder. 
</p>
<p>
<img src="https://imgur.com/1lMLRzg.png" alt="Read"/>
</p>
<p>
For the write-access folder, Domain Users will be allowed to read the contents of the folder and make additions to the folder (write). 
</p>
<p>
<img src="https://imgur.com/RqEckli.png" alt="write-access properties"/>
</p>
<p>
<img src="https://imgur.com/pba5eae.png" alt="Users Read and Write"/>
</p>
<p>
For the no-access folder, Domain Admins will be allowed to read the contents of the folder and make additions to the folder (write). 
</p>
<p>
<img src="https://imgur.com/A1NKTcS.png" alt="no-access properties"/>
</p>
<p>
<img src="https://imgur.com/dMa3rcP.png" alt="Admins Read and Write"/>
</p>
<p>
In the client-1 VM, open File Explorer and type \\dc-1 in the Search bar to view the read-access, write-access, and no-access folders. 
</p>
<p>
<img src="https://imgur.com/TImXP0x.png" alt="\\dc-1"/>
</p>
<p>
<img src="https://imgur.com/jFHjICJ.png" alt="dc-1"/>
</p>
<p>
Since badaca.ros is a Domain User, you can view the contents of the read-access and write-access folders. However, since badaca.ros isn't a Domain Admin, you won't be able to view the contents of the no-access folder. 
</p>
<p>
<img src="https://imgur.com/Oud3Don.png" alt="read-access"/>
</p>
<p>
<img src="https://imgur.com/fEp8jjh.png" alt="write-access"/>
</p>
<p>
<img src="https://imgur.com/K2O6L65.png" alt="no-access"/>
</p>
<br />

<p>
