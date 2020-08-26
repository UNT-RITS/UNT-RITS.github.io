# File System Overview

Talon 3 has a variety of file systems. It is crucial that you understand the proper use of these file systems for best performance and stewardship of computational resources. Misuse of the file systems could mean the termination of your jobs or loss of your data.

# Summary 
| Name    | Path                    | Type     | Quota               | Other Information          |
| ------  | ----------------------- | -------- |-------------------- | -------------------------- |
| HOME    | /home/$USER             | ext4     | 20GB per user       | Backed up weekly           |
| SCRATCH | /storage/scratch2/$USER | Lustre   | 25TB per allocation | No Backup/no data purged   |
| WORK    | /work/$USER             | Lustre   | 2TB per user        | No Backup/subject to purge |

# Details


