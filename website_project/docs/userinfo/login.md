# Logging into Talon3

## Intro

Talon3 is a HPC computing cluster that users remotly access.

To login, you will need to make a remote connection to one of Talon 3’s login nodes.

User **MUST**:

* Have a **ACTIVE** Talon account that has been approved by NTSC
	* [Here](newaccount.md) is more information about requesting a Talon3 account

* Be connected to the UNT network
	* This includes computers connected to the UNT Campus LAN, Eaglenet Wi-Fi, and the UNT VPN Network

Talon3 can be access with the following methods

* [Secure Shell (SSH) terminal](../terminal/ssh.md)
	* Command-line interface
	* Most common inferface to Talon3
* [Rstudio server](..r/rstudio.md) 
	* Access to the Rsudio environment 
* Jupyter 
	* Using Jupyter [Notebooks](../jupyter/jupyter_notebook.md) and [Hub](../jupyter/jupyter_hub.md) within the Talon3 topology 
* [PyCharm](../pycharm/pycharm.md)
	* Use PyCharm IDE on Talon3

## Off Campus access

!!! warning
	Important information about Off Campus access
	
Connecting to Talon3 is only possible if your computer is in the UNT network. Examples are computers connected to the UNT Campus LAN and Eaglenet/UNT Wi-Fi. If you are off campus, you may connect to Talon3 using the UNT Campus VPN. Connecting to the UNT VPN requires an active AMS UNT EUID. This is accomplished by installing the Cisco AnyConnect VPN Client. More information about installing the VPN Client can be found [here](https://it.unt.edu/installing-vpn-client) and [here](https://itservices.cas.unt.edu/services/accounts-servers/articles/cisco-anyconnect-mobility-client-vpn). 

Once you connect to the UNT VPN (located at `vpn.unt.edu`) you can then access Talon via SSH terminal or the other ways to remotly connect. 


## Login information

In order to login to talon you will have to use SSH command on **your personal computer's temrinal**:


### Talon3 password

When you account is first created, your password is your UNTID number by default and is only active for two days. 
You **MUST** login and change it by running the command

```
passwd
```

and enter in a new password. After this, your password will be active for **180** days. An email will be send a week before expiration as a reminder.

If you forget your password or it becomes expired, please consult SciComp-Support@unt.edu. 


```bash
$ ssh euid123@talon3.hpc.unt.edu
```

Then it will ask for you password.

To make things easier you cna have it save the password and even create a shortcut so you can speed things up:

## Setup alias on you SSH connection
Make sure you are in your home directory:


```bash
$ cd ~
```

Check if you have a folder names .ssh


```bash
$ ls -a
```

If you don't you have to create one:


```bash
$ mkdir .ssh
```
Now you need to create a file named config. Use Nano or Vim or any other editor you are comfortable with:


```bash
$ vim ~/.ssh/config
```
If, for example, you want to create a shortcut to ssh on Talon3, your config file should look like:

                                                                                                                                                                                                                                             ```bash
Host t3
  HostName talon3.hpc.unt.edu
  User euid123
  Port 22
```
Where t3 (it can be any word you want) is the shortcut you will use instead of typing:
```bash
$ ssh euid123@talon3.hpc.unt.edu
```
You will type:


```bash
$ ssh t3
```
## Save SSH password
Now you have a shortcut, but you will still need to enter your password every time.

In order to save your passwords you will have to create a keygen file:


```bash
$  ssh-keygen
```
When prompted with this:


```bash
Enter file in which to save the key (/home/your_user/.ssh/id_rsa):
```
Just press Enter to save the id_ras in the path. Then you will be prompted with:


```bash
Enter passphrase (empty for no passphrase):
```
Type Enter again if you don't want to type any password when ssh


```bash
Enter same passphrase again:
```
Hit Enter again!
You should see:


```bash
Your identification has been saved in /home/your_user/.ssh/id_rsa.
Your public key has been saved in /home/you_user/.ssh/id_rsa.pub.
```
Now you can start saving passwords on you SSH:


```bash
 $ ssh-copy-id euid123@talon3.hpc.unt.edu
```
or if you have your shortcut

```bash
$ ssh-copy-id t3
```
You will be prompted to enter password. It will logout, and you should see:

```bash
Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 't3'"
and check to make sure that only the key(s) you wanted were added.
```

Congratulations! Now every time you need to login to Talon you just need to type **ssh t3** and your good to go!

## When you want to copy files using SCP
If you are not familiar with SCP you can find a nice example [here](https://www.computerhope.com/unix/scp.htm)

Now since you setup your ssh shortcut to be t3 and the password saved, when you use SCP it will be a lot easier!

Just type


```bash
scp path/to/file/my_file t3:.
```
It will automatically login and enter the password for you!

For more details on how to transfer files to Talon use [Transferring files](https://hpc.unt.edu/userguide#Transferring_files)




 
