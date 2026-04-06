<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Managing Active Directory Accounts through Group Policy</h1>
This tutorial outlines the modification of the client-1 VM so that non-administrative users can log in, the creation of these users, and the configuration of Group Policy so it can manage the Active Directory accounts of these users, specifically the account lockout policies. Active Directory is Microsoft software designed to manage user accounts and their associated properties, such as passwords and permissions, at scale. Group Policy is a feature within AD that is used for configruration. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure 
- Remote Desktop
- Active Directory Domain Services
- PowerShell

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

