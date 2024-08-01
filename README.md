# Active-Directory-Project-Home-Lab
## Diagram
![image](https://github.com/user-attachments/assets/9988a750-10fe-461a-ab14-3efd4d7e90aa)



## Download and install Oracle VirtualBox from the official website.
<a href="https://www.virtualbox.org/">Oracle Virtual Box</a>

## Download the ISO files
<a href="https://www.microsoft.com/en-us/software-download/windows10">Windows 10</a> &nbsp;&nbsp;&nbsp;&nbsp;
<a href="https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2022">Windows Server 2022</a> &nbsp;&nbsp;&nbsp;&nbsp;
<a href="https://ubuntu.com/download/server">Ubuntu Server</a> &nbsp;&nbsp;&nbsp;&nbsp;

## Installation (Windows, Kali, and Windows Server VM)
Below there are videos on how to install
</br>
<a href="https://www.youtube.com/watch?v=dGr0cyswGq0">Windows 10</a> 
</br>
<a href="https://www.youtube.com/watch?v=pcFrrt6o_cU">Windows Server 2022</a>

## Ubuntu Server Installation

Create a new virtual machine by clicking on "New" in VirtualBox, naming it "Splunk-Server" and selecting the "Ubuntu" ISO file as the boot media. Also, check the box saying <strong>"Skip unattended Installation"</strong> and click Next.
</br>
</br>
![image](https://github.com/user-attachments/assets/03104a14-a292-4603-9049-6c8c2fbfe772)

<ul>
  <li>Give this VM 8 GB (8000 MB) of Ram and 2 CPUs. We giving this VM more Ram and CPUs because it will be ingesting a lot of data.</li>
  <li>For Hard Diks give it 100 GB. And the click Finish</li>
  <li>Your VM should look like this:</li>
</ul>

![image](https://github.com/user-attachments/assets/417866e8-3159-4f37-976b-58ddc7283ca9)

After start the Splunk-Server, click "Try or Install Ubuntu Server"
<ul>
  <li> Press Enter until you get to the Step: Profile configuration, where you will type your name, the server name "splunk", username and password</li>
  <li>The press Enter again, again and wait for it to finish install.</li>
  <li>Then login using your credentials</li>
</ul>
Run the command : <strong>sudo apt-get update && sudo apt-get upgrade -y </strong>
</br>
We use this command to update and upgrade all our repositories.
</br>
</br>
Also before we go on the next step, make sure to change all your VMs network to NAT Network.
</br>
</br>

![image](https://github.com/user-attachments/assets/fad936c6-56e6-48c7-9098-d3cb0573e93f)

## Install and Configure Splunk
First, go on <a href="https://www.splunk.com/">Splunk</a> website and create a free account. After you login, go to Free Trials and download the Splunk Enterprise. Save it to a folder.

![image](https://github.com/user-attachments/assets/28f27467-69e1-4839-99c1-e82f0b669761)
![image](https://github.com/user-attachments/assets/8f709d8b-5f54-473e-b700-6a80e7fa4bf1)

Second, go to your Server VM and run these two commands:
<ul>
  <li><strong>sudo apt-get install virtualbox-guest-additions-iso -y</strong></li>
  <li><strong>sudo apt-get install virtualbox-guest-utils</strong></li>
</ul>

![image](https://github.com/user-attachments/assets/f8a0cd96-66df-4d14-b2ef-0584b8f10f00)

Third, Go to devices shared folders, and settings, add a folder, and pick the folder path where you save the Splunk iso ( read, auto, make)

![image](https://github.com/user-attachments/assets/7a3109ae-fa35-4b19-b3b0-2644ca24e2a0)
![image](https://github.com/user-attachments/assets/8e952341-6a42-42fc-8b5c-3949e673b3b1)
</br>
Then use the command: <strong>sudo reboot</strong> 
</br>to reboot the machine

Now we want to add our user to the vboxsf group. To do that type the command: <strong>sudo adduser "Your user Name" vboxsf</strong>
</br>
</br>
![image](https://github.com/user-attachments/assets/2d3bcc12-0fd9-48c7-b518-47683905978d)

Once the user is added to the group, the next step is to create a folder on the VM named "share." To do this, use the command <strong>mkdir share</strong>, and then use the command <strong>ls</strong> to confirm that the directory was created.
</br>
</br>
![image](https://github.com/user-attachments/assets/672366b3-f8a1-4cc8-be5f-44b92e6c6eb0)

Now that we have our directory created, we have to run the following command to mount our share folder into the directory called share. 
</br>
<ul>
  <li><strong> sudo mount -t vboxsf -o uid=1000,gid=1000 "the name of the folder" share/ </strong></li>
</ul>
</br>

![image](https://github.com/user-attachments/assets/05529ee9-378f-46e9-879d-936e7d57c795)

To install Splunk, use the command </br><strong>sudo dpkg -i splunk-9.2.0...</strong> You can use the Tab keyboard to complete the name. Press Enter, and wait for it to install.
</br>
</br>
![image](https://github.com/user-attachments/assets/ee19bcbd-9468-42e8-b92c-d6e15fd19ddd)

In order to start Splunk, we have to change the directory to where it is located. For this, run the command: </br>
<strong>cd /opt/splunk</strong>
</br>
Then
</br>
<strong>sudo -u splunk bash</strong>
</br>
To change to the user called splunk
</br>
</br>
![image](https://github.com/user-attachments/assets/8b696afe-d74c-4b6e-a79f-51e47383c047)

After, use the command: </br>
<strong>cd bin</strong>
</br>
Then </br>
<strong>./splunk start</strong> </br>
To start splunk
</br>
</br>
Afterward, press the space keyboard until the step where it asks if you agree with the license. Type "y", then create a username and password.
To facilitate our job, we will run a command to start Splunk every time our VM reboots. So that way, we do not have to do all those steps to start Splunk again. First type <strong>exit</strong> to close Splunk, then run the command: </br>
<strong>cd bin</strong></br>
then </br>
<strong>./splunk enable boot-start -user splunk</strong>

![image](https://github.com/user-attachments/assets/a6443248-7d1a-40e3-87ad-c847457a776e)

Before we do anything else, let's check if our Splunk is working. For this, go on the Splunk VM and type the following command: </br>
<ul> <li><strong>ip addres<strong></li></ul></br>

![image](https://github.com/user-attachments/assets/7a2dd961-03fe-41b5-970f-3cae1dd58bc1)

Copy the IP address, go to your Windows VM, Microsoft Edge, and paste the ip:8000. Example 192.168.10.10:8000
</br>
</br>
![image](https://github.com/user-attachments/assets/f8c43574-c85a-4bbd-8598-112fc3e7f1a0)

## Now, we will install the Universal Forwarder both in our Windows target VM and Windows Server. But I will only show how to do it on the Windows target VM, the other one you can do it :)
Just follow the steps

Using the account you created login on <a href="https://www.splunk.com/">Splunk</a>, go to
products > free trial > universal forwarder > windows 64

![image](https://github.com/user-attachments/assets/707b96fb-4197-4f62-b14d-56f2048c49e1)

After you download it, double-click on it to start the installation. Click next, username can be "admin", click next twice

![image](https://github.com/user-attachments/assets/35cd99d1-48f8-4997-ab3a-9895831774ff)

![image](https://github.com/user-attachments/assets/43d66c88-bc24-4422-8bbd-87ee92264302)

When you come to this step, you have to type the IP addres of you splunk server VM and the default port, then click next, and install.
</br>

![image](https://github.com/user-attachments/assets/29cf1b1f-cd3d-44a7-8199-d12d180df1fb)

## Install and Configure Sysmon
Go to website <a href="https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon">Sysmon</a> and download it.
</br>
</br>
For this project, we will be using the Sysmon olaf config, so click the <a href="https://github.com/olafhartong/sysmon-modular">link</a>, and select sysmonconfig.xml.
Click Raw, then right click save as to Download folder.

![image](https://github.com/user-attachments/assets/a657f1c4-aeac-4411-9cc2-3c94521194ef)
![image](https://github.com/user-attachments/assets/e248f07d-7d8b-44fc-bfc0-3ef03f4d347c)

Now go back to the Download folder, extract the Sysmon folder, and copy the path of the location. Open PowerShell as Admin and cd to the folder

![image](https://github.com/user-attachments/assets/be9216f2-53ef-49c9-8e43-79d04ec88d45)
![image](https://github.com/user-attachments/assets/af2898cc-890d-4502-8c44-9bdc27349da5)

Now use this command to install it</br>
<strong>.\sysmon64.exe -i ..\symonconfig.xml </strong>
</br>
and press enter ( then -i is to specify the configuration we want to use)

![image](https://github.com/user-attachments/assets/661713de-3513-4240-b2df-59ea5f22af94)

## THIS IS THE MOST IMPORTANT PART!!!
We have to instruct our Splunk forwarder on what we want to send over to our Splunk server. For this, we must configure a filled called inputs.conf
<ul>
  <li>Open Notepad as admin, type the following:</li>
</ul>

![image](https://github.com/user-attachments/assets/b9c46852-fd0e-40e4-b06e-1419036ac253)

<ul>
  <li>Save the file to:
    <li>c:\Program Files\SplunkUniversalForwarder\etc\system\local with name inputs.conf</li>
  </li>
</ul>

![image](https://github.com/user-attachments/assets/1108701b-2e69-45c6-bbc8-89a7ca66d6ce)

After doing this, we must restart the Splunk universal forwards. Search for services, look for Splunk forwarder, on the column, log on As, change it to the local system, and click apply. Then click restart

![image](https://github.com/user-attachments/assets/84c1c14a-3ff7-4a1d-b0f6-45ce9a0cca96)
![image](https://github.com/user-attachments/assets/7ea8a031-ba02-4f10-81bb-9a0abc1f9376)
![image](https://github.com/user-attachments/assets/5f0d68b6-1b21-475d-89f4-2d3fbf0eb9d1)

Now. we can finalize our Splunk server configuration. Go to the Splunk web portal and log in using your credentials. Click settings, index, create New index > type endpoint, and save it.

![image](https://github.com/user-attachments/assets/b6716412-478a-4db6-bee5-ee6302896a2a)
![image](https://github.com/user-attachments/assets/2f4dfe76-46f9-4b4d-83e7-39d6f7581b1c)

Click settings again, go to Forwarding and receiving, configure receiving > add new, port 9997, and save it.

![image](https://github.com/user-attachments/assets/3a7cc75a-2c01-43ff-9621-5c7483de688e)
![image](https://github.com/user-attachments/assets/9a35c15f-04be-4d92-9987-3961581ca1d5)

To check if everything is good, click apps, search, and reporting, and search for index="endpoint". After doing the same steps on the Windows server machine, you should have 2 hosts.

![image](https://github.com/user-attachments/assets/c040e944-27d1-4760-ab96-1bbe0b710adf)
![image](https://github.com/user-attachments/assets/213b7ec0-d670-4593-9b37-86d296f77851)

## Install and configure Active Directory
To Install and configure Active Directory, head over to the server manager, click manage, and add roles and features.

![image](https://github.com/user-attachments/assets/5bd5bfff-9a99-4522-a2a4-601564f5bcc3)

Click next, next, until this step where you select Active Directory Domain Services. Then Keep clicking next until finishing installing it.

![image](https://github.com/user-attachments/assets/c506b528-524b-4edb-8d4f-2e65460449e6)
![image](https://github.com/user-attachments/assets/26e64171-f50a-45a4-9616-1559423c33f9)

After installation, we need to promote the server to a domain controller. To do this, click the flag in the top right corner. Add a new forest, and pick a name for the domain. The domain must have a top-level domain, it can be whatever name you picked "dot" something. For example work<strong>.local</strong>

![image](https://github.com/user-attachments/assets/36b6d1b5-229d-4f53-bdef-23b856fe26ff)
![image](https://github.com/user-attachments/assets/f35518d6-dafb-4362-9c1a-3e5aec437fce)

Then click next and choose a password. Keep clicking next until installation is done, and wait for the server to reboot.

![image](https://github.com/user-attachments/assets/aad5ab23-c496-47e6-ade1-036063a7d246)

## How to create users

After successfully promoting the server to a domain, login, go to tools, and click on Active Directory users and computers.

![image](https://github.com/user-attachments/assets/3287e159-3297-4637-bd2a-92e17c9f0cf7)

For this project, we will only create two users, but you can create more if you want. Right-click on the domain, select "new," then "organizational unit," and name it "IT." Next, right-click on "IT," choose "new," then "user." Then follow the steps to choose the username and password. Repeat the same process for the other department. In my case, I created one called HR, and a user.

![image](https://github.com/user-attachments/assets/22c06d2e-15ed-456a-a0f0-7635c4027dc8)
![image](https://github.com/user-attachments/assets/03941859-8c35-4755-a964-9cbee40cfac2)

Now that we have our active directory set up and our server. We will go to our Windows target machine, add it to the domain, and log in as one of the users that we created.
But before we go to the Windows target machine, go to PowerShell on the Active Directory VM, and type <strong>ipconfig.<strong> We will need our IP address for the following steps. After copying the IP or memorizing it, go to the Windows target machine.

![image](https://github.com/user-attachments/assets/f2cf8e04-d575-44da-b9ef-5b3e61cc2c7a)

On the Windows target machine, click on the Network & Internet settings, Change adapter options, double click on the Ethernet, Properties, double click on the IPV 4, and select "use the following DNS serve address." Type the IP address of your active directory here, and click Ok.

![image](https://github.com/user-attachments/assets/867e4ba5-6800-4cd2-aa52-9f3744f80f20)

Now, we will add it to the domain. For this, search for about, then click advanced system settings, computer name, change, and type your domain name. Then click okay, and use the administrator credentials.

![image](https://github.com/user-attachments/assets/707e74b5-0b8d-4990-9bbd-8b566ad6974e)

After the computer reboots, we will use one of the users to log in. In my case, I will use user Bob as an example.

![image](https://github.com/user-attachments/assets/bf33eed5-e5f8-4295-ba73-4322aeb60079)

## Perform Brute Force Alerts on Splunk

For this final part of the project, you can use Kali Linux tools to perform brute force. But since the project is getting too long, I will log out of my Active Directory VM and log in again, typing in the wrong password to generate an alert on Splunk.

![image](https://github.com/user-attachments/assets/a260e71d-8397-4808-8b3b-7d41bca24a54)

As we can see in the image provided below, there are six consecutive occurrences of events with the event code 4625.
4625 is a failed logon event that can indicate a brute force attack, dictionary attack, or other password guess attack. A sudden increase in failed logins can be a sign of a brute-force attack.

![image](https://github.com/user-attachments/assets/81dbee5c-3093-4271-91ac-66a5998c6109)



