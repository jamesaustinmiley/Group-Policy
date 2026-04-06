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
Log in to the client-1 VM with one of the new user accounts (mydomain.com\badaca.ros). You will see the password for each of the new users is included in the script (Password1). 
</p>
<p>
<img src="https://imgur.com/DidS6Xw.png" alt="Password1"/>
</p>
<p>
<img src="https://imgur.com/MhDKdH6.png" alt="badaca.ros"/>
</p>
<br />

<p>

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

