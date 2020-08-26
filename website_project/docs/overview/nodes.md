# Talon3 Compute Nodes 

Talon3 is a heterogeneous cluster with different compute node types.

## Login Node

The Talon 3 login nodes can be access by the domain name: 
```bash
talon3.hpc.unt.edu
```
These login nodes are for users to setup jobs and simple file editing via a Linux Command Line terminal. **Users will submit jobs via the SLURM queuing system to be dispatched on the compute nodes. There is NO X11 Forwarding capable on this server.**

## Compute Nodes

The Talon 3 compute nodes are Dell PowerEdge servers where the users will run their software and other computationally intensive applications. Users **do NOT directly login to these nodes**.
Users run their calculations on these nodes by submitting them to the Slurm queuing system.


| Type  | Quanity     | Memory(GB)     | Cores     | Description                                               |
| ----- | --------    |------------    |-------    |-------------------------------------------------------    |
| C6320 | 192         | 64 GB          | 28        | two 2.4GHz Intel Xeon E5-2680 v4 fourteen-core processors |                                                      
| R420  | 75          | 32 GB          | 16        | two 2.1GHz Intel Xeon E5-2450 eight-core processors       |                                                      
| R420  | 64          | 64 GB          | 16        | two 2.1GHz Intel Xeon E5-2450 eight-core processors       |                                                        
| R720  | 8           | 512 GB         | 32        | four 2.4GHz Intel Xeon E5-4640 eight-core processors      |  

The R420 nodes are available to ALL Talon3 allocations. This nodes can be access via the preproducation parition in SLURM.
```
#SBATCH -p preproducation
``` 

The R720 nodes are the big memory nodes that are available to ALL Talon3 allocations that can be access with the bigmem parition.
```
#SBATCH -p bigmem
```

The C6320 access is restricted to Talon3 allocations that recorded 300,000 CPU hours or more during the current or previous fiscal year or have active external funding. These nodes can be access via the producation parition in SLURM.
```
#SBATCH -p production
```


## GPU Node                                                                                                                                                                                                                                  
There are 16 GPU Nodes on Talon. Each one contains 2 Nvidia Tesla K80 GPUs.

| Type |  Quanity    | Memory(GB)     | CPU Cores | GPU         | Description                                                                                                   |
| ---- | ---------   |------------    |-------    |------------ | ----------------------------------------------------------------------------------------------------------    |
| R730 | 16          | 64 GB          | 28        | 4 GPU cards | two 2.4GHz Intel Xeon E5-2680 v4 fourteen-core processors/ two Nvidia Tesla K80 GPUS (4,992 GPU cores/card)   |

The R730 GPU nodes are availabe to ALL Talon3 allocation.
```
#SBATCH -p gpu
```

## Visualization Login Nodes

There are nodes that have X11 capabilities and are Slurm submission hosts. This host is intended for using the graphical-based software, e.g., gnuplot, matplotlib, and other notebook features in software, such as MATLAB and Mathematica. **Users can use these nodes for any post-processing tasks, but any compute-intensive tasks MUST be submitted through the Slurm queuing system.** 

These visualization nodes provide the same funcationally as the login nodes and more.

Jupyter Notebooks and Rstudio can be access to these nodes.

**Also, X11 graphical sessions require large bandwidth to work effectively, and you may experience lag while on a home DSL or Cable ISP.**

X11 forwarding will need to be enabled with the SSH client that you are using. Alternately, you can access a specific visualization node by entering one of the following domain names: 

* `vis.acs.unt.edu`



