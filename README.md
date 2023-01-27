<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>
<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
    <div>This lab demonstrates the implementation of on-premises Active Directory within Azure Virtual Machines.</div>
<h2>Environments and Technologies Used</h2>
    <ul>
        <li>Microsoft Azure (Virtual Machines/Compute)</li>
        <li>Remote Desktop</li>
        <li>Active Directory Domain Services</li>
        <li>PowerShell</li>
    </ul>
<h2>Operating Systems Used</h2>
    <ul>
        <li>Windows Server 2022</li>
        <li>Windows 10 (21H2)</li>
    </ul>
<h2>High-Level Deployment and Configuration Steps</h2>
    <ul>
        <li>Setup Resources in Azure</li>
        <li>Ensure Connectivity between the Client and Domain Controller</li>
        <li>Install Active Directory</li>
        <li>Create an Admin and Normal User Account in AD</li>
        <li>Join Client-1 to your Domain (my domain.com)</li>
        <li>Setup Remote Desktop for Non-Administrative Users on Client-1</li>
        <li>Create a Bunch of Additional Users and Attempt to Log Into Client-1 as One of Those Users</li>
<h2>Deployment and Configuration Steps</h2>
<h3>Step 1: Setup Resources in Azure</h3>
    <p>- In this first step, we go into our Azure portal to create a new virtual machine.</p>
        <img src="https://i.imgur.com/q7GGaoS.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
        <img src="https://i.imgur.com/qGKcLpa.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
    <br>
    <p>- We make sure to create a Domain Controller VM using Windows Server 2022 and named it "DC-1".</p>
    </br>
     <img src="https://i.imgur.com/udM6ozR.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
    <p>
    Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
    </p>
    </br>
