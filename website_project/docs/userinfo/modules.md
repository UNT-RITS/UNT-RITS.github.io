# Environment Modules

Talon 3 uses LMOD to manage your environment. It handles setting up access to the software packages, libraries, and other utilities. This includes compilers, system libraries, and math libraries that are typically needed to build scientific codes. If you need to use a certain application that the HPC staff maintains, you will need to load the appropriate module. Loading the module will modify your environment variables, such as $PATH and $LD_LIBRARY_PATH, that are needed to run the certain application.

 

To see the list of all available modules, run the command:

```
module avail
```
 

To see which modules are already loaded:
```
module list
```
 

To add a module for the current session

```
module load <module_name>
```

where <module_name> is the name of the module you wish to load.

 

For example, if you need to use the Intel compilers, you can run

```
module load intel/compilers/18.0.3-AVX
```

This will load the Intel version 18.0.3 compilers.

 

To configure a module so that it will be loaded into your environment at login:

```
module initadd <module_name>
```
 

To remove a module:

```
module remove <module_name>
```

