<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Managing Active Directory Accounts through Group Policy</h1>
This tutorial outlines configuring Group Policy to manage Active Directory user accounts, specifically account lockout policies. Configuring an account lockout policy in Active Directory using Group Policy involves defining settings that control when an account is locked after multiple failed login attempts, how long the account remains locked, and how the lockout counter is reset. Active Directory is Microsoft software designed to manage user accounts and their associated properties, such as passwords and permissions, at scale. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure 
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 11 (25H2)

<h2> Configuration Steps</h2>

<p>
Log in to the DC-1 Virtual Machine, open Active Directory Users and Computers, and the _EMPLOYEES organizational unit. Pick an employee (mydomain.com\fox.civ) and purposefully use a password other than the correct one (Password1) to observe that there is no policy in place to lock an account after numerous attempts at logging in to the client-1 vm. Back in dc-1, right-click Start, click Run, and type gpmc.msc to open the Group Policy Management Console. The Group Policy Management Console (GPMC) is a Microsoft tool for creating, editing, managing, and troubleshooting Group Policy in Active Directory (AD) environments. Think of it as the control center for rules and settings that get pushed to users and computers across a domain.
</p>
<p>
<img src="https://imgur.com/ztlp3uP.png" alt="ADUC Employees"/>
</p>
<p>
<img src="https://imgur.com/KZHWqTm.png" alt="Run"/>
</p>
<p>
<img src="https://imgur.com/IhbNaFH.png" alt="GPMC Console"/>
</p>
<br />

<p>
Right-click Default Domain Policy and select Edit to modify it. Navigate to the Account Lockout Policy Settings. The three primary settings are Account Lockout Duration, Threshold, and the Reset counter. Account Lockout Duration is the time in minutes that an account remains locked before it is automatically unlocked. Account Lockout Threshold is the number of failed logon attempts that will trigger an account lockout. The Reset Account Lockout Counter is the time in minutes after which the failed logon attempts counter is reset to 0, assuming there are no additional failed logon attempts. After adjusting the three settings, go back to the Default Domain Policy to observe the new Account Lockout Policy along with the other Settings. To force an update of the Group Policy instead of waiting for it to do so automatically, you must log in to the client-1 vm, open Command Prompt as an Administrator, and type gpupdate /force.
</p>
<p>
<img src="https://imgur.com/YM0PjgU.png" alt="Default Domain Policy"/>
</p>
<p>
<img src="https://imgur.com/ljPWt10.png" alt="Account Lockout Policy"/>
</p>
<p>
<img src="https://imgur.com/zveVBKU.png" alt="New Account Lockout Policy"/>
</p>
<p>
<img src="https://imgur.com/p7bkZrA.png" alt="Command Prompt"/>
</p>
<br />

<p>
You can enable or disable user accounts in Active Directory Users and Computers. A quick way to find the account is to right-click mydomain.com, click Find, and type the name of the account. Double-click the account, then select Account to check whether it is locked or unlocked. Using Event Viewer (eventvwr.msc in the Start menu), you can view various logs, including a Security log that shows, among other things, both successful and unsuccessful account login activity. To find activity for a specific account, you can right-click Security, click Find, and type the name. This log can be viewed on both dc-1 and client-1. Although you must run eventvwr.msc as an Administrator and enter the mydomain.com\jane_admin credentials to view it in client-1.
</p>
<p>
<img src="https://imgur.com/A2wgisn.png" alt="Find Users"/>
</p>
<p>
<img src="https://imgur.com/BC2jjRg.png" alt="Unlock or Lock"/>
</p>
<p>
<img src="https://imgur.com/yH8Oyk0.png" alt="eventvwr.msc"/>
</p>
<p>
<img src="https://imgur.com/DG6tQ61.png" alt="Event Viewer"/>
</p>
<p>
<img src="https://imgur.com/Blslm1j.png" alt="Security"/>
</p>
<p>
<img src="https://imgur.com/NAYm6lD.png" alt="Find User"/>
</p>
<p>
<img src="https://imgur.com/YYGAh90.png" alt="fox.civ"/>
</p>
<p>
<img src="https://imgur.com/B5ku64I.png" alt="Administrator"/>
</p>
<p>
<img src="https://imgur.com/Zlqgeo7.png" alt="Jane"/>
</p>
<p>
<img src="https://imgur.com/GJGyvK2.png" alt="Client-1"/>
</p>

