
Talon3 supports OS level virtualization (containers).

Currently, Talon3 supports [Singularity](https://sylabs.io/docs/) to run containers.


## Using Singularity

Talon3 has Singularity version 3.6 installed. 

To use singulartiy on Talon, first you **MUST** load the module

```
module load singularity/3.6
```

## Building a container

Users can set up **Singularity** on thier own workstation and create an container as a SIF image. 

The container can be used to run as a job on Talon.

## Talon3 supported containers                                                                                                                   

There are Talon3 supported containers for users located at `/storage/scratch2/share/containers`                                                                                                                                  
Talon3 supported containers:                                                                                                                     

- biogrinder

### Example container job

```
module load singularity/3.6
```

Pulling ubuntu image from dockerhub

```
singularity pull docker://ubuntu:20.04
```

Running container 

```
singularity exec --bind /storage/scratch2/$USER:/storage/scratch2/$USER,/home/$USER/:/home/$USER/ -e ubuntu_20.04.sif python test.py
```



