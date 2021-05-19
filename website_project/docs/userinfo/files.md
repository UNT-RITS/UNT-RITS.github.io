# Talon3 file management

## Transferring files

### To/From Windows computer

To transfer files with a Windows machine, you will need an SFTP/SCP client software such as [WinSCP](https://winscp.net/eng/index.php) or [Cyberduck](https://cyberduck.io/) installed. When you download a client application, the application will require you to connect to Talon 3 (talon3.hpc.unt.edu). Once logged in, you can use the file transfer window within the program to drag and drop files between local (your personal computer) and remote (Talon 3) machines.

### To/From Mac/Linux computer

To transfer files to and from a cluster on a Linux/Mac machine, you may use the terminal application and the secure copy (scp) command or secure file transfer protocol (sftp). The following is an example of uploading a file foo.f to Talon 3 from your local machine:

```
scp foo.f talon3.hpc.unt.edu
```

You can download files from Talon3 to your local machine.

```
scp talon3.hpc.unt.edu:/home/EUID/foo.f ./
```

To recursively copy an entire directory foo from inside directory *project_foo* in your home directory on Talon 3 to the current working directory on localhost, use the following command:

```
scp -rp talon3.hpc.unt.edu:/home/EUID/project_foo ./
```

## Using rclone with OneDrive

!!! warning
        We are still working on updating our docs!
        Check back for more information!
        Please email SciComp-Support@unt.edu for your questions!


