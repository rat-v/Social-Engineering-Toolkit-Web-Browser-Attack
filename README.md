# Social-Engineering-Web-Browser-Attack

## Objective
In this lab, I am setting up a fake Facebook website, then sending the
link to that fake website via email to the target. The target will login
to the fake facebook which will run an exploit through metasploit to
connect to the target machine

## Skills Learned
Setting up a fake Facebook website using SET (Social Engineering Toolkit)<br>
Using the Facebook web template and Metasploit reverse TCP meterpreter shell<br>
Using Metasploit commands to list and interact with active sessions once the exploit is triggered<br>
Practiced working with a Meterpreter shell to navigate directories and download/upload files <br>
Downloading a directory and specific files, including flag files<br>
Using background to manage sessions and noting the persistence of the exploit<br>

## **Casting the Net - Setting up the fake website**

In the given machine, I was just able to type 'setoolkit' in the
terminal to launch the SET application

I selected (1) for Social-Engineering Attacks

\(2\) for Website Attack Vectors

\(2\) for Metasploit Browser Method

\(1\) to use Web Templates

I'm not sure what the next step meant, but I put in "no" for using
NAT/port forwarding

I typed my host IP address which was "175.45.176.199"

\(3\) to use the Facebook web template

\(46\) for the Metasploit browser exploit

\(2\) for Reverse TCP Meterpreter Shell

{Enter} for using the default port of 443

Waited for a bunch of messages from Metasploit starting the server w/
exploits

Waited until "Done, found x exploit modules"

![image7](https://github.com/user-attachments/assets/02c84419-4212-45cf-92f4-ae91eb8386c5)

## **Getting Attacked - Using the Target System**

I logged in to the target server

I'm not sure how, but there was already an email sent.

The hyperlink to "facebook.com" sent the browser to the fake website

I, as the target, signed in with whatever credentials I was given but I
believe literally anything would work, as long as they hit enter which
will send them to another page. This exploit page will seem to "hang" as
the exploit begins

![image12](https://github.com/user-attachments/assets/126b776f-8795-4687-818c-bae98beb9635)
![image2](https://github.com/user-attachments/assets/1afaf3d9-754b-4ff0-8f03-6b291c2a31b3)


## **Connecting to the Machine**
![image8](https://github.com/user-attachments/assets/82418c34-4a27-4c7c-9d31-fb120307d29c)

Now back the attacker's console, in the "msf auxiliary" command line

**'sessions -l'** to **list all active sessions**

**'sessions** -i **#'** to **interact with a certain machine**

in this case i do 'sessions -i 1' to interact with the first machine

![image9](https://github.com/user-attachments/assets/c29feb7c-57ef-4af9-a3af-0399fff96fb7)


## **Stealing Data - [[Working in a Meterpreter Shell]](https://github.com/rat-v/Random-Notes-for-Tools/blob/main/Metasploit%20and%20Meterpreter.md)**

**'pwd'** to find the **present working directory** to figure out where
I am

Then can use normal windows 'cd' commands to change directory

**'cd /'** to change to root directory

![image1](https://github.com/user-attachments/assets/e0348259-b391-40ee-939c-29ee9df60751)


'**ls'** to list files and folders in the directory, any name that pops
up without an extension is a folder I assume

![image6](https://github.com/user-attachments/assets/b8f77328-d687-4947-b513-6ed633c6000f)


**'cd share'** to move into the share folder

![image11](https://github.com/user-attachments/assets/3a62dac7-84ed-4fbc-872f-ceb315efb5aa)


We can see a folder called "DeathStar" which very likely has classified
imperial plans that I should investigate.

Moving into the DeathStar folder, I see 4 images of blueprints, I can
download the ENTIRE directory by using **'download \*.\*'** and then
sending it to my root folder by adding **'/root'**

So the entire command is **'download \*.\* /root'** to download the
entire directory and then outputting it into my root folder

I can also do **'/root/Blueprints'** to put these images in a dedicated
folder that was just created with the command

![image3](https://github.com/user-attachments/assets/c7b406ed-531b-4d80-9e53-e8b1f1a3f739)


![image10](https://github.com/user-attachments/assets/d4b756a6-9363-4a94-834a-209a5d3a6d45)


Each blueprint has a flag somewhere in the picture

blueprint1 = 999818

blueprint2 = 111222

blueprint3 = 777558

blueprint4 = 655913

I can also download the flag4.xml file in /share using the same download
method. Opening it reveals the flag in the first few lines of the file
(444588)

![image4](https://github.com/user-attachments/assets/3f072c03-35c3-43f5-874f-d04eb06c2d9d)


## **Closing notes**

I can find the ip address of the machine using **'ipconfig'**

**'background'** lets me put the current session in the background so I
can interact with the msf auxiliary console

Even if the target machine closes the web browser, I still have a
completely normal connected session to the machine. I can still move
through directories and download files and see changes made such as
adding or deleting files. I only lost access to the machine when they
manually stopped the "notepad.exe" process that I noticed was
responsible for the exploit in the first section.

In this lab, I noticed an additional machine in the topology called the
Windows 8.1 Attack Server. I'm not really sure how this machine played a
role in this, but I noticed it has the same 175.45.176.200 ip address as
the fake Facebook website, so perhaps it's the server hosting the fake
website? Also I never did any command involving that ip address, so
maybe it's something that was set up before.

![image5](https://github.com/user-attachments/assets/77b02be7-27cc-4350-8ed9-10e53db96ed6)
