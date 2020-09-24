# File System Overview

Talon 3 has a variety of file systems. It is crucial that you understand the proper use of these file systems for best performance and stewardship of computational resources. Misuse of the file systems could mean the termination of your jobs or loss of your data.

# Summary 
| Name    | Path                    | Type     | Quota               | Other Information          |
| ------  | ----------------------- | -------- |-------------------- | -------------------------- |
| HOME    | /home/$USER             | ext4/NFS     | 20GB per user       |  Backed up Daily           |
| SCRATCH | /storage/scratch2/$USER | Lustre   | 25TB per allocation |  No Backup. No data purged |
| WORK    | /work/$USER             | Lustre   | 2TB per user        |  No Backup. Subject to purge at high usage |


