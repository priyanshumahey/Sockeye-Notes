# Sockeye-Notes

## Conda


Load conda
``` shell
module load miniconda3/4.6.14
conda config --add channels conda-forge
``` 

Create a venv
``` shell
condacreate -p /path/to/a/folder
source activate /path/to/a/folder
```

Once activated, you can download whatever you want in the virtual environment.
``` shell
conda install <package_name>
```
