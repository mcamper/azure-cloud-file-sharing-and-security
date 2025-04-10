<p align="center">
<img width="224" alt="image" src="https://github.com/user-attachments/assets/6b91a376-d039-458b-becb-ff416da3771d" />

</p>

<h1>Cloud File Sharing and Security Management in Azure</h1>
Building on a previously established domain controller and Client-1 VM, this tutorial focuses on stting up file shares and managing security permissions in the Azure cloud environment. You'll learn how to create file shares, assign permissions, and utilize Azure security groups without repeating the initial setup process. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>List of Prerequisites</h2>

- AzAD-DomainSetup(https://github.com/mcamper/AzAD-DomainSetup)

<h2>Requirements</h2>

- You've must have completed the last lab AzAD-DomainSetup(https://github.com/mcamper/AzAD-DomainSetup) and have the following setup:
  <ul><li>Active Directory running in Azure on a virtual machine (DC-1)</li>
  <li>A client machine running in Azure on a virtual machine (Client-1) and joined to the domain</li></ul>
    <img width="970" alt="image" src="https://github.com/user-attachments/assets/b07d1642-f32f-49f4-8e17-566308e6de88" />


<h2>Overview of Azure File Sharing and Security Management Steps</h2>

- Step 1: Create Sample File Shares with Various Permissions
- Step 2: Attempt to Access File Shares as a Normal User
- Step 3: Create a Security Group. Assign Permissions and Test Access

<h2>Step 1: Create Sample Files Shares with Various Permissions</h2>
<p>
  <ol>
      <li>Connect/log into DC-1 as your domain admin account (mydomain.com\jane_admin) password: Cyberlab123!</li>
          <img width="254" alt="image" src="https://github.com/user-attachments/assets/e7ca5f69-1497-4303-982a-ce31890442a6" />
      <li>Connect/log into Client-1 as a normal user (mydomain\banu.bij) password: Password1</li>
          <img width="302" alt="image" src="https://github.com/user-attachments/assets/c73d4839-c702-4a6f-83b2-15887bab7d8e" />
      <li>On DC-1, on the C:\drive, reate 4 folders: "read-access", "write-access", "no-access", "accounting"</li>
          <img width="272" alt="image" src="https://github.com/user-attachments/assets/42596134-aa9a-4bc2-a119-9270bb79ab55" />
          <img width="589" alt="image" src="https://github.com/user-attachments/assets/cea96a53-05e2-4a18-85be-ad4ecc237d36" />
          <img width="451" alt="image" src="https://github.com/user-attachments/assets/09b27a4d-e8a9-44de-917f-a70bcd4ca274" />
          <img width="502" alt="image" src="https://github.com/user-attachments/assets/3669d131-a51e-4d98-a35c-bb24129372af" />
      <li>Set the following permissions (share the folder)</li>
          <img width="437" alt="image" src="https://github.com/user-attachments/assets/06db095d-f52a-4bff-93b4-21bafe7610e2" />
          <ul><li>a. Folder: "read-access", Group: "Domain Users", Permission: "Read"</li></ul>
          <img width="254" alt="image" src="https://github.com/user-attachments/assets/c9c1d11f-352e-46ee-b7a1-9d40d69bc0b8" />
          <img width="354" alt="image" src="https://github.com/user-attachments/assets/b55e586e-3848-46a8-9bbd-e7fde045a5ea" />
          <img width="359" alt="image" src="https://github.com/user-attachments/assets/05b54f4c-9a6d-492f-a15a-42b88d397246" />
          <img width="361" alt="image" src="https://github.com/user-attachments/assets/c93e37f9-d0c2-4324-bea9-90fe7c4e9dd4" />

          <ul><li>b. Folder: "write-access", Group: "Domain Users", Permissions: "Read/Write"</li></ul>
          <ul><li>c. Folder: "no-access", Group: "Domain Admins", Permissions: "Read/Write"</li></ul>
          <ul><li>d. (Skip accounting for now)</li></ul>
          
  </ol>

<h2>Step 2: Attempt to Access File Shares as a Normal User</h2>
<p>
  <ol>
    <li>Go back to DC-1 and change mainframe's record address to 8.8.8.8</li>
    <li>Go back to Client-1 and ping "mainframe" again. Observe that it still pings the old address</li>
    <li>Observe the local DNS cache (iponfig /displaydns)</li>
    <li>Delete record(s) from server and observe the client DNS cache</li>
      <ul><li>Flush the DNS cache (ipconfig /flushdns)</li></ul>
      <ul><li>Observe that the cache is empty (iponfig /displaydns)</li></ul>
    <li>Attempt to ping "mainframe" again. Observe the address of the new record is showing up</li>
    
  </ol>
<p>
<h2>Step 3: Create a Security Group. Assign Permissions and Test Access</h2>
<p>
  <ol>
     <li>Go back to DC-1 and create a CNAME record that points the host "search" to "www.google.com"</li>
     <li>Go back to Client-1 and attempt to ping "search". Observe the results of the CNAME record</li>
     <li>On Client-1, nslookup "search". Observe the results of the CNAME record</li>
       
  </ol>
<p>
