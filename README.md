# Active-Directory-Project-Home-Lab
## Diagram
![image](https://github.com/user-attachments/assets/bdbde590-e36b-46c9-85c8-aed76cc29512)


## Download and install Oracle VirtualBox from the official website.
<a href="https://www.virtualbox.org/">Oracle Virtual Box</a>

## Download the ISO files
<a href="https://www.microsoft.com/en-us/software-download/windows10">Windows 10</a> &nbsp;&nbsp;&nbsp;&nbsp;
<a href="https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2022">Windows Server 2022</a> &nbsp;&nbsp;&nbsp;&nbsp;
<a href="https://www.kali.org/get-kali/#kali-virtual-machines">Kali Linux</a> &nbsp;&nbsp;&nbsp;&nbsp;
<a href="https://ubuntu.com/download/server">Ubuntu Server</a> &nbsp;&nbsp;&nbsp;&nbsp;

## Installation (Windows, Kali, and Windows Server VM)
Below there are videos on how to install
</br>
<a href="https://www.youtube.com/watch?v=dGr0cyswGq0">Windows 10</a> 
</br>
<a href="https://www.youtube.com/watch?v=iqTm5TgO-Nw">Kali Linux</a> 
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

## Install and Configure Splunk and Sysmon
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

