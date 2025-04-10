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
          <img width="245" alt="image" src="https://github.com/user-attachments/assets/7845c8ce-f600-4a81-bf41-93a64d6eaf13" />
          <ul><li>b. Folder: "write-access", Group: "Domain Users", Permissions: "Read/Write"</li></ul>
          <img width="515" alt="image" src="https://github.com/user-attachments/assets/b1b7629a-b683-4cfb-9ced-caa8252f0b84" />
          <img width="341" alt="image" src="https://github.com/user-attachments/assets/6c4e020e-d877-4b90-abd1-dccd5b2ee568" />
          <img width="371" alt="image" src="https://github.com/user-attachments/assets/8a439c6f-2cb7-46d9-867a-3111d101df0d" />
          <img width="359" alt="image" src="https://github.com/user-attachments/assets/fa34ba3a-d194-4fea-922b-e8d03b1884ae" />
          <img width="241" alt="image" src="https://github.com/user-attachments/assets/1be5e5db-b35d-401c-a2ea-f62ee06110b7" />
          <ul><li>c. Folder: "no-access", Group: "Domain Admins", Permissions: "Read/Write"</li></ul>
          <img width="552" alt="image" src="https://github.com/user-attachments/assets/6e489642-1602-40bf-8a3d-11b7d62dfa57" />
          <img width="351" alt="image" src="https://github.com/user-attachments/assets/143492a0-7cc6-4896-b63e-16b2e3c2d0a8" />
          <img width="357" alt="image" src="https://github.com/user-attachments/assets/93007629-516e-4adb-b61b-d7b0225c17e4" />
          <img width="342" alt="image" src="https://github.com/user-attachments/assets/d4f589b1-b3fd-4311-be8c-5e0bbd3475f5" />
          <img width="352" alt="image" src="https://github.com/user-attachments/assets/1811e788-dc5d-411f-a51a-3f9d088697ea" />
          <img width="248" alt="image" src="https://github.com/user-attachments/assets/974c576a-53b0-42cc-9548-ffad595d80c6" />
          <ul><li>d. (Skip accounting for now)</li></ul>
          
  </ol>

<h2>Step 2: Attempt to Access File Shares as a Normal User</h2>
<p>
  <ol>
    <li>On Client-1, navigate to the shared folder (File Explorer, \\dc-1)</li>
    <img width="458" alt="image" src="https://github.com/user-attachments/assets/4244fbe3-8c45-4d2f-b047-c0b9fc1d016c" />
    <img width="233" alt="image" src="https://github.com/user-attachments/assets/828b46a2-3d29-4ec9-9876-6a62c6e1afb1" />
    <img width="713" alt="image" src="https://github.com/user-attachments/assets/f339a8ae-31c8-447e-ad3c-2517373ef420" />
    <li>Try to access the folders you just created. Which folders can you access? Which folders can you create stuff in ? Does it make sense?</li>
    <img width="682" alt="image" src="https://github.com/user-attachments/assets/8aaa9d4a-f7ea-433c-b6fa-507890e11bd8" />
    <img width="672" alt="image" src="https://github.com/user-attachments/assets/d5e24699-5b1c-4573-9da2-f306cc92a1d1" />
    <img width="278" alt="image" src="https://github.com/user-attachments/assets/5f19e4a2-5568-4d05-bae6-e9f416e38950" />
    <img width="711" alt="image" src="https://github.com/user-attachments/assets/630b9925-e25a-448e-82bb-851a036c6ff5" />
    <img width="697" alt="image" src="https://github.com/user-attachments/assets/3dc04074-12f2-4222-85f3-9e50ad3a1619" />
    <img width="701" alt="image" src="https://github.com/user-attachments/assets/9c451b76-4124-4584-a61b-7e3ff7300dbb" />
    <img width="701" alt="image" src="https://github.com/user-attachments/assets/930bf8c5-df08-4c8d-a453-a6e576c15de9" />
    <img width="616" alt="image" src="https://github.com/user-attachments/assets/cff24f98-6bcf-46e0-a93c-10da91e7c396" />

  </ol>
<p>
<h2>Step 3: Create a Security Group. Assign Permissions and Test Access</h2>
<p>
  <ol>
     <li>Go back to DC-1, in Active Directory, create a security group called "ACCOUNTANTS" </li>
        <img width="529" alt="image" src="https://github.com/user-attachments/assets/952245e7-e2b5-4505-9ad2-7b004b9637a0" />
        <img width="456" alt="image" src="https://github.com/user-attachments/assets/9b25f2b1-d095-4da9-897e-6b3641067741" />
        <img width="279" alt="image" src="https://github.com/user-attachments/assets/6bbcb10d-fca1-4338-9003-6dff5193f0f8" />
        <img width="277" alt="image" src="https://github.com/user-attachments/assets/abb1484f-2ad6-4ae6-ad43-430ab3587a2c" />
        <img width="474" alt="image" src="https://github.com/user-attachments/assets/f1e5b23a-7ddd-4746-aa4a-ac03f30f01a1" />
        <img width="282" alt="image" src="https://github.com/user-attachments/assets/fe2a7c0c-a2a3-4c76-9c30-c3aa0b40dcfc" />
        <img width="470" alt="image" src="https://github.com/user-attachments/assets/2aa0e374-8d50-4dcd-b355-abf2accc4ce8" />
     <li>On the "accounting" folder you created earlier, set the following permissions:</li> 
        <img width="631" alt="image" src="https://github.com/user-attachments/assets/6273887e-0219-4e30-8fde-88a68350d14d" />
       <ul><li>a. folder: "accounting", Group: "ACCOUNTANTS", Permissions: "Read/Write"</li></ul>
          <img width="239" alt="image" src="https://github.com/user-attachments/assets/9526beaf-88a5-4ad7-b741-17a2c4d42ecd" />
          <img width="353" alt="image" src="https://github.com/user-attachments/assets/dbf1af8c-1bf2-4c9a-874a-c1efd5092cc4" />
          <img width="371" alt="image" src="https://github.com/user-attachments/assets/e6da1919-d381-43ff-be24-3b9d038854e0" />
          <img width="356" alt="image" src="https://github.com/user-attachments/assets/51c408ff-c57c-4d24-952f-7c7121c2093c" />
          <img width="239" alt="image" src="https://github.com/user-attachments/assets/df553867-e516-432a-902b-3cad91585bea" />
    <li>On Client-1, as banu.bij, try to access the accountants folder. It should fail.</li>
          <img width="457" alt="image" src="https://github.com/user-attachments/assets/1d18d02e-7542-40da-8e94-6841b8deb367" />
         <img width="710" alt="image" src="https://github.com/user-attachments/assets/0c41b7be-d573-4208-8ae2-eae98472757b" />



    <li>Log out of Client-1 as banu.bij</li>
    <li>on DC-1, make banu.bij a member of the "ACCOUNTANTS" Security Group</li>
    <li>Sign back nto Client-1 as banu.bij and try to access the "accounting" share in \\dc-1.  Does it work now?</li>
       
  </ol>
<p>
