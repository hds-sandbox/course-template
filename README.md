# docker branch usage

This branch simply contains the docker container useful to containerize the course if needed. There is an example docker container and conda environment file, with kernels examples to add the conda environment paths for executable files, so that the shell will work when used through R or python.

## Compatibility

the docker container in the example can be built and runs with Docker on any computer or HPC cluster. Alternatively, it is also compatible with `singularity`, with the only difference that once the container is imported through singularity, you have to run the script `courseMaterial.sh`, which downloads the data, scripts, notebooks and copies the kernel settings into the home folder (this because the home folder of the container's virtualization is not present in `singularity`, where you have instead your true home folder). This renders possible to run the container on `GenomeDK` and any other HPC with singularity.

## Base Image

You can choose the standard base images, such as the ones from `rocker/rstudio` and all the variants from `jupyterlab`, such as `jupyter/minimal-notebook` in this example. You can also use the images from the ucloud repository (as in the commented line of the dockerfile), but for those you have to remember that the username is called `ucloud` (and not `jovyan` as in the `jupyterlab` base images)

The choice of username has no effect at all when using `singularity`, because there what holds is the user name in the HPC system, but is important in Docker because otherwise things will not work at all.

## UID

In the example the uid is set to 6835. This is because any user of `GenomeDK` has that as uid, and it is also compatible with the `GenomeDK` documentation, where the uid is used as port for jupyterlab.

## Examples

A specific example for the use of this Docker container execution can be seen in the `Access` menu of the NGS summer school webpage for both GenomeDK with singularity and for Docker.