# Sockeye-Notes

## Setup
Before you actually get started with anything related to Sockeye, you'll need to ensure that you have UBC myVPN client set up as well methods for SSC and SCP/SFTP.

To connect to sockeye, use the following:

``` shell
ssh <cwl>@sockeye.arc.ubc.ca
```

From there, you'll need to use multi-factor auth to fully login to Sockeye.

## Environment
Sockeye is based on CentOS 7.x (GNU/Linux) os and the default shell is ```/bin/bash```.

## Folders

HOME: While your home directory may seem like the logical place to store all your files and do all your work, in general this isn't the case; your home normally has a relatively small quota and doesn't have especially good performance for writing and reading large amounts of data. The most logical use of your home directory is typically source code, small parameter files and job submission scripts.

PROJECT: The project space has a significantly larger quota and is well-adapted to sharing data among members of a research group since it, unlike the home or scratch, is linked to a professor's account rather than an individual user. The data stored in the project space should be fairly static, that is to say the data are not likely to be changed many times in a month. Otherwise, frequently changing data, including just moving and renaming directories, in project can become a heavy burden on the tape-based backup system.

**Note** : project storage is read-write on login, data transfer and interactive nodes but is read-only on compute nodes.

SCRATCH: For intensive read/write operations on large files (> 100 MB per file), scratch is the best choice. Remember however that important files must be copied off scratch since they are not backed up there, and older files are subject to purging. The scratch storage should therefore be used for temporary files: checkpoint files, output from jobs and other data that can easily be recreated.

**Scratch**: read-write on all nodes

A recommend storage I/O workflow pattern on Sockeye could be summarized as:

1. Copy/transfer input data to /arc/project/```<alloc-code>```
2. Login to Sockeye and create/modify job script(s) in /scratch/```<alloc-code>```
3. Submit jobs that read input data from /arc/project/```<alloc-code>``` and writes output to /scratch/```<alloc-code>```  (or $TMDIR)
4. Job completes successfully
5. Copy/transfer job output from /scratch/```<alloc-code>``` to /arc/projects/```<alloc-code>```
6. Interactively post-process and/or analyze results in /arc/project/```<alloc-code>```

## Conda


Load conda
``` shell
module load miniconda3/4.6.14
conda config --add channels conda-forge
``` 
Note: may have to try: ```module load miniconda3/4.9.2```


Create a venv
``` shell
condacreate -p /path/to/a/folder
source activate /path/to/a/folder
```

Once activated, you can download whatever you want in the virtual environment.
``` shell
conda install <package_name>
```


## Pytorch
``` shell

```
