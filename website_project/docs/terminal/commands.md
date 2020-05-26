# Commands

Here are a few commands which are useful when using Talon3 HPC:


## Modules:

See available modules:

```bash
$ module avail
```

Load modules:

```bash
$ module load name_of_module
```

Unload module:

```bash
$ module unload unload name_of_module
```

## Pre-Load modules when login to Talon

If you have modules you're using everytime you can pre-load them everytime you login to Talon.

This way you avaoid having to do module load everytime.

Terminal commands:
```bash
$ cd
$ vim .bashrc
```
Now you opened the bash file and you should see:


```bash
module load gcc slurm
```
On the same line add any module you want loaded when ever you login to Talon. 

For example, to load python 3.6.5 anytime we login:


```bash
module load gcc slurm python/3.6.5
```

## Job details:

Find out your job id:

```bash
$ squeue -u euid123
```
 
 **\$JOB_ID** can be seen under **JOBID** column:

```bash
$ scontrol show job $JOB_ID
```

Kill a job. Users can kill their own jobs, root can kill any job:

```bash
$ scancel $JOB_ID
```

Hold a job:

```bash
$ scontrol hold $JOB_ID
```


Release a job:

```bash
$ scontrol release $JOB_ID
```
 
 
## See Resources:

### Login to your node:

Find out your node name:

```
 $ squeue -u euid123
```
**\$NODE_NAME** can be seen under **NODELIST** column

To login your node:

```
 $ slogin $NODE_NAME
```

### Once logged in the node, use following commands:
See load on CPUs:

```bash
$ mpstat -P ALL 
```
See process running on CPUs:

```bash
$ pidstat
```

See GPU resources [IF IS A GPU NODE]:


```bash
$ nvidia-smi
```

## Show breakdown of jobs by user


```bash
$ squeue -h | awk '{print $4}' | sort | uniq -c | sort -rn
```


## Show queue statue by a particular user


```bash
$ squeue -u euid123
```

## Code on your computer and run it straight to an alocated node on Talon:
This can be very usefull when you have code on your personal computer that you want to run on Talon.

You will need your  **\$NODE_NAME** for this. 

**You run this command from your personal computer's terminal!**

```bash
$ ssh euid123@talon3.hpc.unt.edu slogin $NODE_NAME python < your_local_file.py 
```

*your_local_file.py* is a file located on your personal computer.

If you require certain modules to be loaded, pre-load them in your .bashrc file - See previous.

If you setup your ssh shortcut it will be as easy as:


```bash
 $ ssh t3 slogin $NODE_NAME python < your_local_file.py
```

If you need to use a dataset, you will need to change directories when ssh. To do this you have to cd first in the desired directory and then run the file:


```bash
 $ ssh t3 slogin $NODE_NAME "cd /home/euid/your_path ; python" < your_local_file.py
```

### NOTE: Remember to add any modules you want pre-loaded if you use this command!
