# Talon Hight-Performance Computing


## Terminology

We refer to the same thing when we say: *Talon* , *HPC*, *Talon3* (refering to the version of Talon), *Cluster*, *High-Performance Computing*, *Server*.

## Compute Node

The Talon 3 compute nodes are where the users will run their software and other computationally intensive applications. Users **do NOT directly login to these nodes**. 
Users run their calculations on these nodes by submitting them to the Slurm queuing system. 

These specific nodes can be chosen in the SLURM queuing system by including a resource request option `#SBATCH -C` to meet your needs (i.e. for the Dell PowerEdge **C6320** use `#SBATCH -C c6320`):

| Quanity     | Memory(GB)     | Cores     | Description                                                                                                                                       |
|---------    |------------    |-------    |-----------------------------------------------------------------------------------------------------------------------------------------------    |
| 192         | 64 GB          | 28        | Dell PowerEdge **C6320** server with two 2.4GHz Intel Xeon E5-2680 v4 fourteen-core processors.                                                       |
| 75          | 32 GB          | 16        | Dell PowerEdge **R420** server with two 2.1GHz Intel Xeon E5-2450 eight-core processors.                                                              |
| 64          | 64 GB          | 16        | Dell PowerEdge **R420** server with two 2.1GHz Intel Xeon E5-2450 eight-core processors                                                               |
| 8           | 512 GB         | 32        | Dell PowerEdge **R720** server with four 2.4GHz Intel Xeon E5-4640 eight-core processors.                                                             |
| 16          | 64 GB          | 28        | Dell PowerEdge **R730** server with two 2.4GHz Intel Xeon E5-2680 v4 fourteen-core processors and **two Nvidia Tesla K80 GPUS (`4,992 GPU` cores/card)**.     |


## Login Node

The Talon 3 login nodes can be access by the domain name: 
```bash
talon3.hpc.unt.edu
```
These login nodes are for users to setup jobs and simple file editing via a Linux Command Line terminal. **Users will submit jobs via the SLURM queuing system to be dispatched on the compute nodes. There is NO X11 Forwarding capable on this server.**

## Visualization Login Nodes

There are five login nodes that have X11 capabilities and are Slurm submission hosts. This host is intended for using the graphical-based software, e.g., gnuplot, matplotlib, and other notebook features in software, such as MATLAB and Mathematica. **Users can use these nodes for any post-processing tasks, but any compute-intensive tasks MUST be submitted through the Slurm queuing system.** 

**Also, X11 graphical sessions require large bandwidth to work effectively, and you may experience lag while on a home DSL or Cable ISP.**

X11 forwarding will need to be enabled with the SSH client that you are using. Alternately, you can access a specific visualization node by entering one of the following domain names: 

* `vis.acs.unt.edu`
* `vis-01.acs.unt.edu`
* `vis-02.acs.unt.edu`
* `vis-03.acs.unt.edu`
* `vis-04.acs.unt.edu`


## GPU Node

There are 16 GPU Nodes on Talon. Each one contains 2 Nvidia Tesla K80 GPUs.

| Quanity     | Memory(GB)     | Cores     | Description                                                                                                                                       |
|---------    |------------    |-------    |-----------------------------------------------------------------------------------------------------------------------------------------------    |
|             |
| 16          | 64 GB          | 28        | Dell PowerEdge **R730** server with two 2.4GHz Intel Xeon E5-2680 v4 fourteen-core processors and **two Nvidia Tesla K80 GPUS (`4,992 GPU` cores/card)**.     |

## Job

In an HPC cluster, the users' tasks to be done on compute nodes are controlled by a batch queuing system. Queuing systems manage job requests (shell scripts generally referred to as jobs) submitted by all users on Talon 3. 

**In other words, to get your computations done by the cluster, you must submit a job request to a specific batch queue.** The scheduler will assign your job to a compute node in the order determined by the policy on that queue and the availability of an idle compute node. 

Currently, Talon 3 resources have several policies in place to help guarantee fair resource utilization from all users. 

## Batch / batch job

Refers to the process of creating a `.job` file and submit it to HPC using the slurm command `sbatch job_name.job` where `job_name.job` is your job file.

Here is a brief example of a `.job` file that runs a python script named `test.py`:

```bash
#!/bin/bash
#SBATCH -J job_name
#SBATCH -o output_job.o%j
#SBATCH -e error_job.e%j
#SBATCH -p public
#SBATCH --qos general
#SBATCH -N 1
#SBATCH -n 1
#SBATCH -C c6320

module load python

python test.py
```

For more details on how to write a job file please check: **[Slurm Tutotials](https://hpc.unt.edu/userguide#Slurm_tutorials)**

## Interractive Session

Interactive job sessions can be used on Talon if you need to compile or test software. An example command of starting an interactive sessions is shown below:

```bash
 $ srun -p public --qos general -C c6320  --pty bash
 
```

This launches an interactive job session and lanches a bash shell to a compute node. From there, you can execute software and shell commands that would otherwise not be allowed on the Talon login nodes.

You can use same **Slurm Commands**:
Check our [UNT website](https://hpc.unt.edu/userguide#partitions)

**Example of requesting 1 node with email notificaiton for CPU:**

```bash
srun -p public --qos general --mail-user=user@unt.edu --mail-type=ALL -N 1 -C c6320 --pty bash
```

**Example of requesting 1 node with email notificaiton for GPU:**

```bash
srun -p gpu --mail-user=user@unt.edu --mail-type=ALL -N 1 --pty bash
```

This is very useful because it notifies you when your node has been allocated to you so you can start work!

For more details on how to write a job file please check: **[Slurm Tutotials](https://hpc.unt.edu/userguide#Slurm_tutorials)**



## Module/s

Talon 3 uses LMOD to manage your environment. It handles setting up access to the software packages, libraries, and other utilities.

To see the list of all available modules, run the command:

```bash
module avail
```

To see which modules are already loaded:

```bash
module list
```

To add a module for the current session:

```bash
module load <module_name>
```

where <module_name> is the name of the module you wish to load.

 

For example, if you need to use the Intel compilers, you can run

```bash
module load python/3.6.5
```
This will load the Python version 3.6.5.

Here is a table of current modules that can be found on Talon 3:

| /cm/shared/modulefiles/science       | /cm/shared/modulefiles/science                             | /cm/shared/modulefiles/utils                             |
|----------------------------------    |--------------------------------------------------------    |------------------------------------------------------    |
|    JDFTx/1.5.0                       |    R/R-devel                                               |    PackageEnv/gcc4.8.5_OBLAS0.2.19_OMPI2.1.0             |
|    OpenSees/3.0.3                    |    R/3.6.0                                       (D)       |    PackageEnv/gcc8.1.0_OBLAS0.2.19_OMPI2.1.0             |
|    amber/16-cuda-mpi                 |    anaconda/5.2                                            |    PackageEnv/intel17.0.4_MKL_IMPI_AVX                   |
|    amber/16-gen                      |    atlas/3.10.3                                            |    PackageEnv/intel17.0.4_MKL_IMPI_AVX2                  |
|    amber/18-gen              (D)     |    bison/3.5.90                                            |    PackageEnv/intel18.0.3_gcc4.8.5_MKL_IMPI_AVX          |
|    ansys/2019r1                      |    boost/1.63.0                                            |    PackageEnv/intel18.0.3_gcc4.8.5_MKL_IMPI_AVX2         |
|    armadillo/7.950.1                 |    boost/1.71.0                                  (D)       |    PackageEnv/intel18.0.3_gcc8.1.0_MKL_IMPI_AVX  (D)     |
|    bamtools/2.4.1                    |    bzip2/1.0.6                                             |                                                          |
|    bazel/0.9.0                       |    cluster-tools/7.3                                       |                                                          |
|    bazel/0.14.0              (D)     |    cmake/3.8.0                                             |                                                          |
|    bbmap/38.76                       |    cmake/3.15.2                                  (D)       |                                                          |
|    bcftools/1.4                      |    cmd                                                     |                                                          |
|    bcftools/1.4.1                    |    cmgui/7.3                                               |                                                          |
|    bcftools/1.6              (D)     |    cmsh                                                    |                                                          |
|    beast/1.8.4                       |    cuda/101/toolkit/10.1.243                               |                                                          |
|    beast/2.4.5               (D)     |    cuda/102/toolkit/10.2.89                                |                                                          |
|    bedtools/2.18                     |    cuda/75/blas/7.5.18                                     |                                                          |
|    bioperl/1.007002                  |    cuda/75/fft/7.5.18                                      |                                                          |
|    blast/2.6.0                       |    cuda/75/nsight/7.5.18                                   |                                                          |
|    bowtie2/2.3.1                     |    cuda/75/profiler/7.5.18                                 |                                                          |
|    bowtie2/2.3.2             (D)     |    cuda/75/toolkit/7.5.18                                  |                                                          |
|    bsr/bsr                           |    cuda/80/blas/8.0.61                                     |                                                          |
|    bsr/dbsrhf                (D)     |    cuda/80/fft/8.0.61                                      |                                                          |
|    bwa/0.7.17                        |    cuda/80/nsight/8.0.61                                   |                                                          |
|    caffe/cpu                         |    cuda/80/profiler/8.0.61                                 |                                                          |
|    caffe/gpu                 (D)     |    cuda/80/toolkit/8.0.61                                  |                                                          |
|    cairo/1.14.10                     |    cuda/90/blas/9.0.176                                    |                                                          |
|    cd-hit/4.6.6                      |    cuda/90/fft/9.0.176                                     |                                                          |
|    cd-hit/4.8.1              (D)     |    cuda/90/nsight/9.0.176                                  |                                                          |
|    circos/0.69                       |    cuda/90/profiler/9.0.176                                |                                                          |
|    clark/1.2.4                       |    cuda/90/toolkit/9.0.176                                 |                                                          |
|    comsol/5.5                        |    cuda/91/blas/9.1.85                                     |                                                          |
|    cp2k/6.1                          |    cuda/91/fft/9.1.85                                      |                                                          |
|    cufflinks/2.2.1                   |    cuda/91/nsight/9.1.85                                   |                                                          |
|    ddocent/2.2.16                    |    cuda/91/profiler/9.1.85                                 |                                                          |
|    dirac/2019                        |    cuda/91/toolkit/9.1.85                                  |                                                          |
|    dlpoly/class-1.10                 |    cudnn/5.1/cuda75                                        |                                                          |
|    dlpoly/4.08               (D)     |    cudnn/5.1/cuda80                              (D)       |                                                          |
|    eigen/3.3.3                       |    cudnn/6.0/cuda75                                        |                                                          |
|    emto/5.8.1                        |    cudnn/6.0/cuda80                              (D)       |                                                          |
|    espresso/6.0                      |    cudnn/7.0/cuda90                                        |                                                          |
|    espresso/6.5              (D)     |    cudnn/7.1/cuda90                                        |                                                          |
|    fastqc/0.11.8                     |    cudnn/7.6.5/cuda90                                      |                                                          |
|    fastxtoolkit/0.0.13               |    cudnn/7.6.5/cuda101                                     |                                                          |
|    fpart/1.0.0                       |    cudnn/7.6.5/cuda102                           (D)       |                                                          |
|    gamess/08182016                   |    curl/7.54.1                                             |                                                          |
|    gamess/10302017           (D)     |    ea-utils/2017                                           |                                                          |
|    gatk/3.80                         |    fftw/2.1.5                                              |                                                          |
|    gaussian/g09-revA                 |    fftw/3.3.6                                              |                                                          |
|    gaussian/g09-revD         (D)     |    fftw/3.3.8                                    (D)       |                                                          |
|    gaussian/g16-RevA.03-ax2          |    gcc/4.8.5                                               |                                                          |
|    genenetwork/2                     |    gcc/5.5.0                                               |                                                          |
|    gistic2/2.0.23                    |    gcc/6.1.0                                               |                                                          |
|    gnuplot/5.0.6             (D)     |    gcc/6.3.0                                               |                                                          |
|    grasp/grasp2018                   |    gcc/8.1.0                                     (L,D)     |                                                          |
|    gromacs/5.1.4-fftw                |    git/2.9.3                                               |                                                          |
|    gromacs/2019.1-cuda               |    glibc/2.23                                              |                                                          |
|    gromacs/2019.1            (D)     |    gnuplot/5.0.6                                           |                                                          |
|    gsl/2.4                           |    go/1.10.3                                               |                                                          |
|    gulp/4.5                          |    gperf/3.1                                               |                                                          |
|    h2o4pu/0.3.2                      |    gsl/2.6                                       (D)       |                                                          |
|    hadoop/2.8.0-rdma                 |    hdf5/1.6.10                                             |                                                          |
|    hisat/0.1.6                       |    hdf5/1.8.18-gnu                                         |                                                          |
|    hisat/2.0.5               (D)     |    hdf5/1.8.18-intel                                       |                                                          |
|    icu/4c-59                         |    hdf5/1.10.5                                   (D)       |                                                          |
|    jags/4.2.0                        |    hisat/0.1.6                                             |                                                          |
|    kallisto/0.43.1                   |    hisat/2.0.5                                             |                                                          |
|    keras/2.1.6                       |    htslib/1.4                                              |                                                          |
|    keras/2.2.0               (D)     |    htslib/1.6                                    (D)       |                                                          |
|    kraken/0.10                       |    htslib/1.10                                             |                                                          |
|    kraken/2.0.7              (D)     |    intel/IMPI/17.0.4-AVX                                   |                                                          |
|    lammps/7Aug19                     |    intel/IMPI/17.0.4-AVX2                                  |                                                          |
|    lammps/11Aug17                    |    intel/IMPI/17.0.4                                       |                                                          |
|    lammps/17Nov16            (D)     |    intel/IMPI/18.0.3-AVX                                   |                                                          |
|    maps/4.2                          |    intel/IMPI/18.0.3-AVX2                                  |                                                          |
|    mathematica/10.0                  |    intel/IMPI/18.0.3                             (D)       |                                                          |
|    mathematica/11.3          (D)     |    intel/compilers/17.0.4-AVX                              |                                                          |
|    matlab/R2014b                     |    intel/compilers/17.0.4-AVX2                             |                                                          |
|    matlab/R2016b                     |    intel/compilers/18.0.3-AVX                    (D)       |                                                          |
|    matlab/R2018b             (D)     |    intel/compilers/18.0.3-AVX2                             |                                                          |
|    minimac2/2014.9.15                |    intel/mkl/17.0.4-AVX                                    |                                                          |
|    mothur/1.43.0                     |    intel/mkl/17.0.4-AVX2                                   |                                                          |
|    mpiblast/1.6.0                    |    intel/mkl/17.0.4                                        |                                                          |
|    mplus/8                           |    intel/mkl/18.0.3-AVX                                    |                                                          |
|    mummer/4.0                        |    intel/mkl/18.0.3-AVX2                                   |                                                          |
|    namd/2.12-cuda                    |    intel/mkl/18.0.3                              (D)       |                                                          |
|    namd/2.12                 (D)     |    java/1.8                                                |                                                          |
|    ncurses/6.0                       |    java/13.0.2                                   (D)       |                                                          |
|    nonmem/7.4.3                      |    jupyter/4.4.0                                           |                                                          |
|    nwchem/6.8                        |    lapack/3.7.0                                            |                                                          |
|    nwchem/6.8.1-dev          (D)     |    libffi/3.2.1                                            |                                                          |
|    oases/0.2.8                       |    libtool/2.4.6                                           |                                                          |
|    oncosnp/1.4                       |    miniconda/2/4.7.12                                      |                                                          |
|    openfoam/5.0                      |    miniconda/3/4.7.12                                      |                                                          |
|    ovito/2.9.0                       |    netcdf/c/4.7.3                                          |                                                          |
|    paraview/5.3.0                    |    octave/5.2.0                                            |                                                          |
|    parsync/1.67                      |    openblas/0.2.19                                         |                                                          |
|    phyml/3.1                         |    opencv/3.4.7                                            |                                                          |
|    picard/2.10                       |    openmpi/gcc/1.10.6                                      |                                                          |
|    plink/1.07                        |    openmpi/gcc/2.1.0                                       |                                                          |
|    plink/1.90                        |    openmpi/gcc/3.1.4                             (D)       |                                                          |
|    plink/2.00                (D)     |    openmpi/intel/2.1.0-cuda                                |                                                          |
|    psi4/1.0.0                        |    openmpi/intel/2.1.0                           (D)       |                                                          |
|    pytorch/gpu-1.1.0                 |    openmpi/pgi/1.10.2                                      |                                                          |
|    pytorch/gpu-1.2.0                 |    openmpi/pgi/2.1.2                                       |                                                          |
|    pytorch/gpu-1.4.0                 |    openmpi/pgi/3.1.3                             (D)       |                                                          |
|    pytorch/gpu-1.5.0         (D)     |    parallel/20200122                                       |                                                          |
|    qiime2/2020.2                     |    perl/5.24.1                                             |                                                          |
|    raxml/8.2.10              (D)     |    perl/5.30.2                                   (D)       |                                                          |
|    rohan/1.0                         |    pgi/17.5                                                |                                                          |
|    sagemath/7.6                      |    pgi/18.10                                               |                                                          |
|    salmon/1.0                        |    pgi/19.7                                      (D)       |                                                          |
|    samtools/1.4                      |    pssh/2.3.1                                              |                                                          |
|    samtools/1.4.1                    |    pyMPI/2.4                                               |                                                          |
|    samtools/1.6              (D)     |    python/2.7.13                                           |                                                          |
|    seqprep/1.0                       |    python/2.7.14-pyCUDA                                    |                                                          |
|    sklearn/0.18.1                    |    python/3.5.7                                            |                                                          |
|    soapdenovo/1.03                   |    python/3.6.0                                            |                                                          |
|    spades/3.10.1                     |    python/3.6.0-2                                          |                                                          |
|    spades/3.12.0             (D)     |    python/3.6.5                                            |                                                          |
|    spark/2.3.0                       |    python/3.7.0                                            |                                                          |
|    spring/spring5                    |    python/3.7.4                                  (D)       |                                                          |
|    sra-tools/2.92                    |    qt/5.14.0                                               |                                                          |
|    stacks/1.46                       |    raxml/8.2.10                                            |                                                          |
|    star/2.5.3a                       |    readline/7.0                                            |                                                          |
|    stringtie/1.3.3b                  |    singularity/3.6                                         |                                                          |
|    subread/2.0.0                     |    slurm/16.05.8                                 (L)       |                                                          |
|    tdep/1.1                          |    sparsehash/2.0.2                                        |                                                          |
|    tecplot/2018R1                    |    szip/1.12b                                              |                                                          |
|    tensorflow/1.2.0                  |    tcl/8.6.7                                               |                                                          |
|    tensorflow/1.10.1-gpu             |    xalt/2.6                                                |                                                          |
|    tensorflow/1.10.1                 |    xalt/2.8                                      (L,D)     |                                                          |
|    tensorflow/1.12.3-gpu             |    zlib/1.2.11                                             |                                                          |
|    tensorflow/2.0                    |                                                            |                                                          |
|    tensorflow/2.1.0-gpu      (D)     |                                                            |                                                          |
|    tophat/2.1.1                      |                                                            |                                                          |
|    transformers/transformers         |                                                            |                                                          |
|    trinity/2.4.0                     |                                                            |                                                          |
|    vasp/4.6-vtst                     |                                                            |                                                          |
|    vasp/5.4.1-vtst                   |                                                            |                                                          |
|    vasp/5.4.1                        |                                                            |                                                          |
|    vasp/5.4.4-vtst           (D)     |                                                            |                                                          |
|    vcftools/0.1.17                   |                                                            |                                                          |
|    velvet/1.2.10                     |                                                            |                                                          |
|    visit/2.12.2                      |                                                            |                                                          |
|    vmd/1.9.3                         |                                                            |                                                          |
|    warp/4.5                          |                                                            |                                                          |
|    xoopic/2.70                       |                                                            |                                                          |
