Adding new nodes
============================

•    Authors
Created by                                                                                                                                                             Charles Peterson 03/2017      
Modified by                                                                                                                                                             XXXXXXXXXX      

•    Purpose
Adding new nodes to the Talon3 cluster

•    Procedure

You can do this either though cmgui or cmsh

With cmgui,
Create a new node under the ‘Nodes’ Tab.
Modify hostame
added it to a node catgory
Enter the Network values
    Name: BOOTIF (internal Talon3 network)
    Type: Physical
    Network: internalnet (10.1.0.0/16)
    IP: 10.1.xxx.xxx

    Name: ib0 (the IB network)
    Type: Physical
    Network: ibnetnet (10.11.0.0/16)
    IP: 10.11.xxx.xxx

    Name: ipmi0 (IPMI/BMC network 
    Type: BMC (IPMI)
    Network: ipminet (10.2.0.0/16)
    IP: 10.2.xxx.xxx

Boot the node and PXE boot
MAKE SURE TO CHANGE THE iDRAC NETWORK FROM THE DEDICATED PORT TO LOM1. You will need to go into the BIOS, into the system setting (F2) and go to the iDRAC network settings.


