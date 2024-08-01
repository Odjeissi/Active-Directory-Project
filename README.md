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


