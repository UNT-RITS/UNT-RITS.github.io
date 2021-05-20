Slurm
============================

•    Authors
Created by                                                                                                                                                             Charles Peterson 011/2016      
Modified by                                                                                                                                                             XXXXXXXXXX      

•    Purpose
The use of Slurm on Talon3

•    Procedure

Setting up Slurm
[root@bright73 ~]# wlm-setup -w slurm -s


Multifactor Priority
Default is FIFO
Change the Multifactor in /etc/slurm/slurm.conf
# SCHEDULING
PriorityType=priority/multifactor
PriorityUsageResetPeriod=1-0
PriorityWeightFairshare=100000
PriorityWeightAge=1000
PriorityWeightPartition=10000
PriorityWeightJobSize=1000
PriorityMaxAge=14-0
PriorityDecayHalfLife=0
PriorityFavorSmall=NO
PriorityWeightQOS=0
PriorityWeightPartition=1000



Queues
scontrol show partitions

