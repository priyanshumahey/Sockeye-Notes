# Sockeye-Notes

## Documentation

The link to the actual documentation is kept on: <https://confluence.it.ubc.ca/display/UARC/UBC+ARC+Technical+User+Documentation>.

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

``` bash
module load miniconda3/4.6.14
conda config --add channels conda-forge
```

Note: may have to try: ```module load miniconda3/4.9.2```

If Conda creates an issue, you may need to remove channels using: conda config --remove channels NAMEOFCHANNEL

Create a venv

``` bash
conda create -p /path/to/a/folder
source activate /path/to/a/folder
```

Once activated, you can download whatever you want in the virtual environment.

``` bash
conda install <package_name>
```

To deactivate, use

``` bash
conda deactivate
```

## Jupyter Notebooks

1. First you'll need to change to the folder where we'll create a script to run Jupyter notebooks in.

``` bash
mkdir -p /scratch/<st-alloc-1>/<cwl>/my_jupyter
```

2. From there, we'll be creating a job script named jupyter-datascience.pbs. To view what the script looks like, take a look at jupyter-datascience.pbs. There's also a file called make_jpyterpbs.ipynb which generates a pbs script for you that you can copy and paste into Sockeye to run a Jupyter notebook.

3. Run the jupyter-datascience.pbs file using qsub. This runs the job script.

``` bash
qsub jupyter-datascience.pbs
```

4. Once the job is running, you can then use qstat to request the status of jobs, queues, or a batch server.

``` bash
qstat -u $USER
```

5. Now that we've gotten the job to run, we can view the contents of connecion_<`jobid`> which will give us the SSH tunnel and connection instructions:

``` bash
cat connection_<jobid>.txt
```

6. We can create an SSH tunnel from your LOCAL workstation:

``` bash
ssh -N -L 8888:<node>:<port> <cwl>@sockeye.arc.ubc.ca
```

From there, you direct your local web browser to <http://localhost:8888/>.

7. When you're done, you can end the script using:

``` bash
qdel <jobid>
```

## Custom Environments in Jupyter

For this next step, it is assumed that we have already installed the jupyter/datascience-notebook container as /arc/project/<`st-alloc-1`>/jupyter/jupyter-datascience.sif


1. First we launch a shell with `jupyter/datscience-notebook` container on Sockeye login node:

``` bash
module load gcc singularity

singularity shell --home /scratch/<st-alloc-1>/<cwl>/my_jupyter --env XDG_CACHE_HOME=/scratch/<st-alloc-1>/<cwl>/my_jupyter /arc/project/<st-alloc-1>/jupyter/jupyter-datascience.sif
```

## Pytorch

``` bash

```
