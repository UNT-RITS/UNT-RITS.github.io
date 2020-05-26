# SSH Terminal Easy Configuration 

(Mac and Linux Only)


If you never used SSH before [this](https://www.digitalocean.com/community/tutorials/how-to-use-ssh-to-connect-to-a-remote-server-in-ubuntu) is a helpful example.

Or if you don't know if you have SSH installed on your sistem [Mac](http://osxdaily.com/2017/04/28/howto-ssh-client-mac/)    [Linux](https://www.tecmint.com/install-openssh-server-in-linux/)

## Login

In order to login to talon you will have to use SSH command on **your personal computer's temrinal**:


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

