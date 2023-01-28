<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>
<h1><u>On-premises Active Directory Deployed in the Cloud (Azure)</u></h1>
    <div>This lab demonstrates the implementation of on-premises Active Directory within Azure Virtual Machines.</div>
    <h2><em>Environments and Technologies Used</em></h2>
        <ul>
            <li>Microsoft Azure (Virtual Machines/Compute)</li>
            <li>Remote Desktop</li>
            <li>Active Directory Domain Services</li>
            <li>PowerShell</li>
        </ul>
    <h2><em>Operating Systems Used</em></h2>
        <ul>
            <li>Windows Server 2022</li>
            <li>Windows 10 (21H2)</li>
        </ul>
    <h2><em>High-Level Deployment and Configuration Steps</em></h2>
        <ul>
            <li>Setup Resources in Azure</li>
            <li>Ensure Connectivity between the Client and Domain Controller</li>
            <li>Install Active Directory</li>
            <li>Create an Admin and Normal User Account in AD</li>
            <li>Join Client-1 to your Domain (my domain.com)</li>
            <li>Setup Remote Desktop for Non-Administrative Users on Client-1</li>
            <li>Create a Bunch of Additional Users and Attempt to Log Into Client-1 as One of Those Users</li>
    <h2><u>Deployment and Configuration Steps</u></h2>
        <h3>Step 1: Setup Resources in Azure</h3>
            <p>- In this first step, we go into our Azure portal so we can create a new virtual machine.</p>
                <img src="https://i.imgur.com/q7GGaoS.png" height="50%" width="50%" 
                    alt="Disk Sanitization Steps"/>
                <img src="https://i.imgur.com/qGKcLpa.png" height="50%" width="50%" 
                    alt="Disk Sanitization Steps"/>
            <p>- We make sure to create a Domain Controller VM using Windows Server 2022 and named it "DC-1".</p>
             <img src="https://i.imgur.com/udM6ozR.png" height="50%" width="50%" 
                    alt="Disk Sanitization Steps"/>
            <p>- Once we  have created our Domain Controller, we go into it's NIC (Network Interface Card) and we make sure we go in to change it's Private IP address so that it is static, and not dynamic. We do this so we can be assured that the IP address will not change, so that our Client PCs can reliability stay connected it's network.</p>
                <img src="https://i.imgur.com/XOE3PAN.png" height="50%" width="50%"/>
            <p>- Next, we create our Client VM running Windows 10. This is what we are going to use to connect to the Domain Controller, and act as an user utilizing the Domain Controller's Services.
                <hr>- Here you can see our Client VM has been created.
            </p>
                <img src="https://i.imgur.com/riABdCo.png" height="50%" width="50%"/>
        <h3>Step 2: Ensure Connectivity Between the Client and Domain Controller</h3>    
                <p>- First, to do this, we'll log into Client-1 with Remote Desktop.</p>
                    <img src="https://i.imgur.com/MYT73js.png" height="20%" width="20%"/>
                    <div><img src="https://i.imgur.com/Nsd1lMf.png" height="50%" width="50%"/></div>
                <p>- Next, we'll open the command prompt and ping DC-1's private IP address with "ping -t 10.0.0.4", which result in a perpetual ping so we can monitor it. (10.0.0.4 is DC-1's private IP)</p>    
                    <img src="https://i.imgur.com/BP5qyZK.png" height="50%" width="50%"/>
                    <hr>
                    <img src="https://i.imgur.com/t5yaPoD.png" height="50%" width="50%"/>
                <p>- As you can see, we are getting a Request Time Out error, because ICMP4 is not enabled on the local windows firewall for DC-1 (The Domain Controller). </p>
                    <br>
                <p>- Our next step would be to log into DC-1 and enable ICMP4 in the local windows firewall settings. Since ping uses the ICMP4 protocol, that's what we will enable.</p>
                    <img src="https://i.imgur.com/1SXZFpJ.png" height="20%" width="20%"/>
                    <div><img src="https://i.imgur.com/TOpe3jp.png" height="50%" width="50%"/></div>
                    <img src="https://i.imgur.com/v0t162J.png" height="50%" width="50%"/>
                    <img src="https://i.imgur.com/EtKPxSK.png" height="50%" width="50%"/>
                <p>- We can now check back on Client-1, our Client VM, and see now that the pings are successfully echoing back.</p>
                    <img src="https://i.imgur.com/fJFJa6b.png" height="50%" width="50%"/>
        <h3>Step 3: Install Active Directory</h3>
            <p>- To do this, we go inside of Server Manager on DC-1 and click on "Add Roles and Features".</p>
                <img src="https://i.imgur.com/UEn5o58.png" height="50%" width="50%"/>
                <img src="https://i.imgur.com/lB23ih8.png" height="50%" width="50%"/>
                <img src="https://i.imgur.com/3eixrSx.png" height="50%" width="50%"/>
                <img src="https://i.imgur.com/DUXB1tb.png" height="50%" width="50%"/>
                <img src="https://i.imgur.com/mFb81mg.png" height="50%" width="50%"/>
            <hr>
            <p>- Our next step is to promote this server into a domain controller, then setting up a new forest as freeyourmind.com.</p>
                <img src="https://i.imgur.com/TO5vQv1.png" height="50%" width="50%"/>
                <img src="https://i.imgur.com/ZC3r4Zh.png" height="50%" width="50%"/>
                <img src="https://i.imgur.com/0gmTswf.png" height="50%" width="50%"/>
        <h3>Step 4: Create an Admin and Normal User Account in AD</h3>
            <p>- To achieve this, first we go to Active Directory Users and Computers under the Tools menu.</p>
                <img src="https://i.imgur.com/F1WaKhV.png" height="50%" width="50%"/>
            <hr>    
            <p>- Here you can see our domain that we created, freeyourmind.com.</p>
                <img src="https://i.imgur.com/IjFQ9h5.png" height="50%" width="50%"/>
            <p>- In here, we will create an Organizational Unit (OU) called "_EMPLOYEES" and "_ADMINS".</p>
                <img src="https://i.imgur.com/fF5IF6C.png" height="50%" width="50%"/>
                <img src="https://i.imgur.com/scr4094.png" height="50%" width="50%"/>
            <hr>    
            <p>- Next we'll create a new user as an Admin under the name "Trinity 3", with the username "trinity_admin".</p>
                <img src="https://i.imgur.com/kyzK2Br.png" height="50%" width="50%"/>
                <img src="https://i.imgur.com/Bf8X0W9.png" height="%0%" width="50%"/>
            <p>- Next we want to give the user "Trinity 3" admin rights. That is achieved by adding the user to the "Domain Admins" Security Group.</p>
                <img src="https://i.imgur.com/EE0kYGA.png" height="50%" width="50%"/>
                <img src="https://i.imgur.com/LsmPyn8.png" height="50%" width="50%"/>
                <img src="https://i.imgur.com/N4zVcSM.png" height="50%" width="50%"/>
            <p>- Now that's created, our next step is to log out, and for now we are using "Trinity 3" as our admin account.</p>
                <img src="https://i.imgur.com/vu4ippZ.png" height="50%" width="50%"/>
        <h3>Step 5: Join Client-1 to your domain (freeyourmind.com)</h3>
            <p>- First, we need to start back in the Azure Portal, and set Client-1's DNS settings to the Domain Controller's Private IP address.</p>
                <img src="https://i.imgur.com/KqNrj79.png" height="50%" width="50%"/>
            <p><em>- Since 10.0.0.4 is the Domain Controller's Private IP Address, he added that in the DNS configuration for Client-1 to make sure that it is pointing to the Domain Controller for it's resources.</em></p>
            <hr>
            <p>- Next, we'll restart Client-1 from the Azure Portal in order to flush the dns cache and assure the settings were configured.</p>
                <img src="https://i.imgur.com/3AK0sBn.png" height="50%" width="50%"/>
            <p>- After this, we'll login to Client-1 (Remote Desktop) as the original local admin (labuser) and join it to the domain. (After this computer will restart)</p>
                <img src="https://i.imgur.com/qqtk8bk.png" height="20%" width="20%"/>
            <br>
                <img src="https://i.imgur.com/XJRXe2x.png" height="20%" width="20%"/>
            <br>
                <img src="https://i.imgur.com/BozcxvI.png" height="50%" width="50%"/>
            <p>- As you can see, our DNS Servers are in Client-1 are pointing to the private IP address of our Domain Controller.</p>
                <img src="https://i.imgur.com/CEpYuQ0.png" height="50%" width="50%"/>
                <img src="https://i.imgur.com/F0hHXVq.png" height="50%" width="50%"/>
            <p>- Next step is to join it to the domain. (After this computer will restart)</p>
                <img src="https://i.imgur.com/uXxIN98.png" height="50%" width="50%"/>
                <img src="https://i.imgur.com/1BbsgXj.png" height="50%" width="50%"/>
                <img src="https://i.imgur.com/cXLLZoi.png" height="50%" width="50%"/>
                <img src="https://i.imgur.com/bZ25Slv.png" height="50%" width="50%"/>
            <p>- Next, we'll login to the Domain Controller (Remote Desktop) and verify Client-1 shows up in Active Directory Users and Computers (ADUC) inside the “Computers” container on the root of the domain.</p>
                <img src="https://i.imgur.com/vLvxttz.png" height="20%" width="20%"/>
            <br>
                <img src="https://i.imgur.com/uKgMTvz.png" height="20%" width="20%"/>
            <br>
                <img src="https://i.imgur.com/ocY9cDN.png" height="50%" widt="50%"/>
            <p>- Lastly, we'll create a new OU name "_CLIENTS" and drag Client-1 into there.</p>
                <img src="https://i.imgur.com/2aLy47q.png" height="50%" width="50%"/>
                <img src="https://i.imgur.com/rYBhGBV.png" height="50%" width="50%"/>
        <h3>Step 6: Setup Remote Desktop for Non-Administrative Users on Client-1</h3>
            <p>- First, we'll log back into Client-1 as freeyourmind.com\trinity_admin, and open System Properties.</p>
                <img src="https://i.imgur.com/pZL2aZT.png" height="20%" width="20%"/>
            <br>
                <img src="https://i.imgur.com/FD3Zmil.png" height="20%" width="20%"/>
            <br>    
                <img src="https://i.imgur.com/ZM8N95x.png" height="50%" width="50%"/>
            <p>- Click "Remote Desktop".</p>   
                <img src="https://i.imgur.com/Zn63TlE.png" height="50%" width="50%"/>
            <p>- Allow Domain Users access to Remote Desktop.</p>
                <img src="https://i.imgur.com/I2i2p8c.png" height="50%" width="50%"/>
            <p>- You can now log into Client-1 as a normal, non-administrative user now.</p>
        <h3>Step 7: Create a bunch of additional users and attempt to log into client-1 with one of the users.</h3>
            <p>- Firstly, to do this, we'll login to the Domain Controller, DC-1, as trinity_admin.</p>
                <img src="https://i.imgur.com/tMQTYTW.png" height="20%" width="20%"/>
            <br>
                <img src="https://i.imgur.com/xBo8CSS.png" height="20%" width="20%"/>
            <br>
            <p>- To continue, we will use PowerShell to implement a script that will create a bunch of users for us as if we were using a real user database.</p>
                <img src="https://i.imgur.com/AbU5nrc.png" height="50%" width="50%"/>
            <hr>
            <p><em>"This script was received from an outside source." Source: <a>https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1</a></em></p>
                <img src="https://i.imgur.com/ghDjg2Z.png" height="50%" width="50%"/>
            <p>- We'll run the script and observe all the accounts/users being created.</p>
                <img src="https://i.imgur.com/y5redmp.png" height="50%" width="50%"/>
                <img src="https://i.imgur.com/ACL9Tdw.png" height="50%" width="50%"/>
            <p>- When finished, open ADUC and observe the accounts in the appropriate OU.</p>
                <img src="https://i.imgur.com/Hji4FxP.png" height="50%" width="50%"/>
            <p>- Can now attempt to log into Client-1 with one of the random accounts (take note of the password in the script).</p>
                <img src="https://i.imgur.com/DAiP0GS.png" height="20%" width="20%"/>
            <br>
                <img src="https://i.imgur.com/3P2HOIz.png" height="20%" width="20%"/>
            <br>
                <img src="https://i.imgur.com/cmvfM1u.png" height="50%" width="50%"/>
                <img src="https://i.imgur.com/UTURCRR.png" height="50%" width="50%"/>
        <h2><strong><em> (Bonus) Demonstration of Changing a Users Password in Active Directory.</em></strong></h2>
                <img src="https://i.imgur.com/Dpozpmq.png" height="50%" width="50%"/>
                <img src="https://i.imgur.com/X4xhlvS.png" height="50%" width="50%"/>
                <img src="https://i.imgur.com/0c6XR86.png" height="50%" width="50%"/>
                <img src="https://i.imgur.com/MOaYNxd.png" height="50%" width="50%"/>  
                <img src="https://i.imgur.com/aGl4nzj.png" height="50%" width="50%"/>
