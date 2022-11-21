# Sockeye-Notes

## Folders

HOME: While your home directory may seem like the logical place to store all your files and do all your work, in general this isn't the case; your home normally has a relatively small quota and doesn't have especially good performance for writing and reading large amounts of data. The most logical use of your home directory is typically source code, small parameter files and job submission scripts.

PROJECT: The project space has a significantly larger quota and is well-adapted to sharing data among members of a research group since it, unlike the home or scratch, is linked to a professor's account rather than an individual user. The data stored in the project space should be fairly static, that is to say the data are not likely to be changed many times in a month. Otherwise, frequently changing data, including just moving and renaming directories, in project can become a heavy burden on the tape-based backup system.

SCRATCH: For intensive read/write operations on large files (> 100 MB per file), scratch is the best choice. Remember however that important files must be copied off scratch since they are not backed up there, and older files are subject to purging. The scratch storage should therefore be used for temporary files: checkpoint files, output from jobs and other data that can easily be recreated.


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
