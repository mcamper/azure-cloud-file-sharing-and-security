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

<h2>High-Level Deployment, Configuration and Management Steps</h2>

- Step 1: A-Record Exercise
- Step 2: Local DNS Cache Exercise
- Step 3: CNAME Record Exercise

<h2>Step 1: A-Record Exercise</h2>
<p>
  <ol>
    <li>Inspect DNS A-Records on the Server</li>
      <ul><li>Connect/log into DC-1 as your domain admin account (mydomain.com\jane_admin)</li></ul>
      <ul><li>Connect/log into Client-1 as an admin (mydomain\jane_admin)</li></ul>
      <ul><li>From Client-1, try to ping "mainframe". Notice that it fails</li></ul>
      <ul><li>Nslookup "mainframe". Notice that it fails (no DNS record)</li></ul>
    <li>Create an A-Record on the server and observe from the client</li> 
      <ul><li>Create a DNS A-Record on DC-1 for "mainframe" and have it point to DC-1' Private IP address</li></ul>
      <ul><li>Go back to Client-1 and try to ping it. Observe that it works</li></ul>
          
</ol>

<h2>Step 2: Local DNS Cache Exercise</h2>
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
<h2>Step 3: Create CNAME Record</h2>
<p>
  <ol>
     <li>Go back to DC-1 and create a CNAME record that points the host "search" to "www.google.com"</li>
     <li>Go back to Client-1 and attempt to ping "search". Observe the results of the CNAME record</li>
     <li>On Client-1, nslookup "search". Observe the results of the CNAME record</li>
       
  </ol>
<p>
