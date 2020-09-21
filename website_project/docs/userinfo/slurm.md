# Slurm Job Scheduler

## Overview

In an HPC cluster, the users' tasks to be done on compute nodes are controlled by a batch queuing system. Queuing systems manage job requests (shell scripts generally referred to as jobs) submitted by all users on Talon 3. In other words, to get your computations done by the cluster, you must submit a job request to a specific batch queue. The scheduler will assign your job to a compute node in the order determined by the policy on that queue and the availability of an idle compute node. Currently, Talon 3 resources have several policies in place to help guarantee fair resource utilization from all users. 

The [SLURM Workload Manger](https://slurm.schedmd.com/documentation.html) is userd to control how jobs are dispatched on the compute nodes.


## Basic Information about Slurm

The **Slurm Workload Manager** (formally known as Simple Linux Utility for Resource Management or SLURM), or Slurm, is a free and open-source job scheduler for Linux and Unix-like kernels, used by many of the world's supercomputers and computer clusters. It provides three key functions. First, it allocates exclusive and/or non-exclusive access to resources (computer nodes) to users for some duration of time so they can perform work. Second, it provides a framework for starting, executing, and monitoring work (typically a parallel job such as MPI) on a set of allocated nodes. Finally, it arbitrates contention for resources by managing a queue of pending jobs. Slurm is the workload manager on about 60% of the TOP500 supercomputers, including Tianhe-2 that, until 2016, was the world's fastest computer. Slurm uses a best fit algorithm based on Hilbert curve scheduling or fat tree network topology in order to optimize locality of task assignments on parallel computers.

### Slurm Tutorials and Commands

A Quick-Start Guide for those unfamiliar with Slurm can be found [here](https://slurm.schedmd.com/quickstart.html)

Slurm Tutorial Videos can be found [here](https://slurm.schedmd.com/tutorials.html) for additional information

## Talon3 Job Submission

### Partitions

Currently on Talon3, there are 4 partitions for users to submit their jobs.

| Partition | Node Type | Max Nodes | Max Duration | Details |
| --------  | --------  | --------  | ----------- | -------  |
| preproduction | R420 | 22 | **See QOS** | Available to any Talon3 user |
| production | C6320 | 22 | **See QOS ** | Available to production users |
| bigmem | R720 | 2 | 1 weeks | Available to any Talon3 user |
| gpu | R730 | 3 | 1 weeks | Available to any Talon3 user |

Users have access the production partition if their allocation reaches 300,000 CPU hours within the current and previous FY OR they have an active external funding source.

If you require more resources, you may submit a support ticket to SciComp-Support@unt.edu and the Talon3 admin staff will evaaluate your request.

### QOS

The Quality of Service, QOS, sets the priority of the job to the queuing system. There are **three** QOS's under the **preproduction** and **production** partitions.

For the **bigmem** and **gpu** partition, you do NOT need to specify QOS.

| QOS | Description |
| --- | ----------  |
| debug | <ul><li>Two hour limit</li><li>two compute nodes</li><li>Highest priority</li></ul> |
| general | <ul><li>72 hour limit</li><li>22 compute nodes</li><li>Medium priority</li></ul> |
| large | <ul><li>3 week limit</li><li>22 compute nodes</li><li>lowest priority</li></ul> | 

### Common Slurm information

The following list frequently used SLURM commands

| Slurm Command | Description |
| -------------  | ----------|
| sbatch script.job | submit a job |
| squeue jobid | display job status |
| squeue -u $USER | display status of user's jobs |
| scancel jobid | canncel a job |
| scontrol update | modify a **pending** job |

The following lists command SLURM variables that you can use in your job scripts

| SLURM Variable | Description |
| -------------- | ---------- |
| $SLURM_SUBMIT_DIR | current working directory of the submitting client |
| $SLURM_JOB_ID | unique identifier assigned when the job was submitted |
| $SLURM_NTASKS | number of CPUs in use by a parallel job |
| $SLURM_NNODES | number of hosts in use by a parallel job |
| $SLURM_ARRAY_TASK_ID | index number of the current array job task |
| $SLURM_JOB_CPUS_PER_NODE | number of CPU cores per node |
| $SLURM_JOB_NAME | Name of JOB |

### SLURM Example Commands

Submitting a job

```
sbatch slurm.job
```
Where **slurm.job** is the name of the job script

List all current jobs that a user has in the queue
```
squeue -u $USER
```

Get job details
```
scontrol show job 106
```
where 106 is the JOBID number

Kill a job that is in the queue
```
scancel 106
```
where 106 is t he JOBID number of the job you wan to be killed

Hold a job in the queue
```
scontrol hold 106
```

Release a held job in the queue
```
scontrol release 106
```

### The SLURM Job Script

The job script is a file that has the SLURM information for sbatch.

The following table list command sbatch options

| Option | Argument | Description |
| -----  | -------- | ----------- |
| -p  | *parition_name* | submits to a certain *[arition_name* |
| -J  | *job_name* | defines the name of the job |
| -o | *output_name* | defines file name to direct standard output from job <br> Default *slurm-JOBID.out* |
| -e | *error_name* | defines file name to direct error output <br> Defalut *output_name* |
| --qos | *QOS_name* | defines the requested QOS |
| --exclusive | N/A | sets exclusive job, not allowing other jobs to share on compute node |
| -t | *time* | set up the wall time limit for job in hh:mm:ss |
| -N | *num_nodes* | Definies the total number of compute nodes requested |
| -n | *num_cores* | Definies the total number of cpu tasks requested |
| --ntasks-per-node | *num_cpu_pernode* | Definies the number of cpu tasks PER node |
| --mail-user | *user_email* | sets up email notification |
| --mail-type | *mail_type* | Emails users when *mail_type* is: <ul><li>**begin** A email will set when job starts</li><li>**end** A email will set when job ends</li></ul> |


###Example job Scripts

Simple serial job script example

```
#!/bin/bash
######################################
# Example of a SLURM job script for Talon3
# Job Name: Sample_Job
# Number of cores: 1
# Number of nodes: 1
# QOS: general
# Run time: 12 hrs
######################################
#SBATCH -J Sample_Job
#SBATCH -o Sample_job.o%j
#SBATCH -p preproduction
#SBATCH --qos general
#SBATCH -N 1
#SBATCH -n 1
#SBATCH -t 12:00:00

### Loading modules 
module load intel/compilers/18.0.1

./a.out > outfile.out
```

Simple parallel MPI job script example

When submitting a MPI job, make sure you load the module and use *mpirun* to launch your application
```
#!/bin/bash
######################################
# Example of a SLURM job script for Talon3
# Job Name: Sample_Job
# Number of cores: 28
# Number of nodes: 1
# QOS: general
# Run time: 12 hrs
######################################
#SBATCH -J Sample_Job
#SBATCH -o Sample_job.o%j
#SBATCH -p preproduction
#SBATCH --qos general
#SBATCH -N 1
#SBATCH -n 16
#SBATCH --ntasks-per-node 16
#SBATCH -t 12:00:00

### Loading modules
module load PackageEnv/intel17.0.4_gcc8.1.0_MKL_IMPI_AVX

### Use mpirun to run parallel jobs
mpirun ./a.out > outfile.out
```

Larger MPI job script example
```
#!/bin/bash
######################################
# Example of a SLURM job script for Talon3
# Job Name: Sample_Job
# Number of cores: 112
# Number of nodes: 4
# QOS: general
# Run time: 12 hrs
######################################
#SBATCH -J Sample_Job
#SBATCH -o Sample_job.o%j
#SBATCH -p preproduction
#SBATCH --qos general
#SBATCH -N 4
#SBATCH -n 64
#SBATCH --ntasks-per-node 16
#SBATCH -t 12:00:00

### Loading modules
module load PackageEnv/intel17.0.4_gcc8.1.0_MKL_IMPI_AVX

## Use mpirun for MPI jobs
mpirun ./a.out > outfile.out
```

Big Memory job script example
```
#!/bin/bash
######################################
# Example of a SLURM job script for Talon3
# Job Name: Sample_Job
# Number of MPI tasks: 32
# Number of nodes: 1
# Run time: 12 hrs
######################################
#SBATCH -J Sample_Job
#SBATCH -o Sample_job.o%j
#SBATCH -p bigmem
#SBATCH -N 1
#SBATCH --ntasks-per-node 32
#SBATCH -t 12:00:00

### Loading modules
module load PackageEnv/intel17.0.4_gcc8.1.0_MKL_IMPI_AVX

mpirun ./a.out > outfile.out
```

CUDA parallel GPU job script example
```
#!/bin/bash
######################################
# Example of a SLURM job script for Talon3
# Job Name: Sample_Job
# Number of devices(GPUs): 2
# Number of nodes: 1
# QOS: general
# Run time: 12 hrs
######################################
#SBATCH -J Sample_Job
#SBATCH --ntasks=1
#SBATCH --gres=gpu:2
#SBATCH -t 12:00:00
#SBATCH -p gpu

### execute code
./a.out -numdevices=2
```

## Interactive sessions

Interactive job sessions can be used on Talon if you need to compile or test software. Interactive jobs will start a command line session on a compute node. If you have to run large tasks or processes, running an interactive job will allow you to run these tasks without using the login nodes.

An example command of starting an interactive session is shown below:

```
$ srun -p preproduction --qos debug -N 1 -n 16 -t 2:00:00 --pty bash
srun: job 55692 queued and waiting for resources
srun: job 55692 has been allocated resources
[c64-6-32 ~]$ python test.py   # Run python on compute node
[c64-6-32 ~]$ exit             # Exit interactive job
```

This launches an interactive job session and launches a bash shell to a compute node. From there, you can execute software and shell commands that would otherwise not be allowed on the Talon login nodes.



