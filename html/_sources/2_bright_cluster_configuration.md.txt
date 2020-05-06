Bright Cluster configuration
============================

•    Authors
Created by                                                                                                                                                             Charles Peterson 12/2016      
Modified by                                                                                                                                                             Yuguang Ma  08/2017    

•    Purpose
Setup configuration for Talon3 with Bright

•    Procedure

Head nodes
The Head nodes for Talon3 are R630 nodes:
location on the UNT network: t3-head.hpc.unt.edu

There are two head nodes for Talon3. High Availability (HA) is in use with have the two head nodes to act as a failover pair. 
t3-head1 – located on rack 13, rank XX
t3-head2 – located on rack 13, rank XX


Network Interfaces:
1Gb:
eth0 – internal network for management(10.1.XXX.XXX)
eth1 – UNT network, Internet (129.120.220.XXX)
10GB (with adapter): 
eth2
eth3


