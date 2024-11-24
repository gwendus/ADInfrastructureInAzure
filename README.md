<p align="center">

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/a8/Microsoft_Azure_Logo.svg/320px-Microsoft_Azure_Logo.svg.png" alt="Azure logo"/>
 
 <h1>#Active Directory Setup</h1>
This tutorial outlines the creation of our network environment in Microsoft Azure, the first step in deploying Active Directory.
<br />


<h2>Environments and Technologies</h2>

- <b>Microsoft Azure</b> 
- <b>Remote Desktop</b>
- <b>PowerShell</b>

<h2>Operating Systems</h2>

- <b>Windows 10</b> (22H2)
- <b>Windows Server</b> (2022)
  <br />

<h2>List of Prerequisites</h2>

- <b>Azure Resource Group</b> - acts as a folder for our resources
- <b>Azure Virtual Network and Subnet</b> - functions as our network environment

<h2>Installation Steps:</h2>
<b>Our first objective is to set up our Domain Controller in Azure.</b> We begin by creating Resource Group to contain our Virtual Network and Subnetwork, which we then also create.
  <br>
  <br>
<img src="https://i.imgur.com/ygAGHf9.png" height="80%" width="80%" alt="Azure Resource group, v net and subnet"/>
<br />
<br />

Next, we create the Domain Controller (DC) Virtual Machine (VM). Name it "DC-1" and make sure to use Windows Server 2022 so we can install our dependencies in the next part of this lab. Configure the username and password.

<img src="https://i.imgur.com/gZkurIb.png" height="80%" width="80%" alt="DC-1 machine"/><br />
<br />
<br />

After the VM is created, we need to make the NIC's Private IP address static. We can navigate to this page under Network Settings>IP configuration. Static entries help maintain network reliability.

<img src="https://i.imgur.com/wT15lFV.png" height="70%" width="70%" alt="Make IP static"/>
<br />
<br />


Next, we will access the VM through a remote connection in order to disable the Windows Firewall (to test connectivity). Retrieve the public IP address we just made static and enter the login credentials you created in a new Remote Desktop Connection session.  <br/>

<img src="https://i.imgur.com/Ix15SnQ.png" height="50%" width="50%" alt="Connect to DC-1 through RDP"/>
<br />
<br />

Next, we will disable the firewall. Right click the "Start" Icon and select "Run" so we can enter "wf.msc" to summon Windows Defender. Browse to the settings.

<br />

<img src="https://i.imgur.com/OkS1vfX.png" height="50%" width="50%" alt="Windows Defender in Run"/>

<br />

<img src="https://i.imgur.com/u64qCkH.png" height="70%" width="70%" alt="Windows Defender Settings"/>
<br />
<br />

<b>Our next objective is to set up our Client Machine in Azure.</b> 
  <br>
Create another VM within the same region, Resource Group, and VNet. Make it run on Windows 10 and name it "Client-1". Configure the username and password. <br />


After it deploys, set Client-1’s DNS settings to DC-1’s Private IP address. We can accomplish this through Network Settings>DNS servers and writing in the *private* IP address associated with DC-1.<br/>
<img src="https://i.imgur.com/W8obnBo.png" height="80%" width="80%" alt="MySQL and root configuration"/>
<br />
<br />

Restart Client-1 from the Azure portal.<br/>
<img src="https://i.imgur.com/4yVA1T1.png" height="50%" width="50%" alt="Restart client-1 vm."/>
<br />
<br />

Then, login via remote connection. We will attempt to ping DC-1's private IP address. Open the command line and run ping 10.0.0.4. Ensure the ping succeeded.<br/>
<img src="https://i.imgur.com/WSkaTGa.png" height="80%" width="80%" alt="Ensure ping succeeded"/>
<br />
<br />


Lastly, open PowerShell and run ipconfig /all. The output for the DNS settings should show DC-1's private IP address. <br/>
<img src="https://i.imgur.com/ZpjzuJm.png" height="70%" width="70%" alt="Register new PHP version."/>
<br />
<br />

Finish the lab, but do not delete the VMs in Azure. We will use them for upcoming labs.
If you are done for the day and want to save money, simply “Stop”/turn off the VMs within the Azure Portal
