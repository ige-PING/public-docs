This document should help you get started with containers on supercomputers. It gives you all the steps to create a container image and use it on supercomputers, but it does not explain every tiny detail of the procedure. See the "suggested reading" section at the end of this document for more information.

# What is a container?

In computing, a container can be several different things. Here we can think of a container as "a small operating system that can be run on a supercomputer (or elsewhere), a bit like a virtual machine".

# Why use containters?

Here are some reasons:

 - you can use containers to deploy the same computing environment on multiple supercalculators.

 - you can use containers to create environments for supercomputer such as TGCC, where most outgoing connections are firewalled off (meaning that you cannot use pip or conda from TGCC).

 - you can use containers to work with multiple environments without conflict.

# Preparing a container with podman on MacOS

## Installing and seting up podman

[Podman](https://podman.io/) is a software to create container images and run containers. It is a completety free and open-source alternative to [Docker](https://www.docker.com/).

Install Podman with [Homebrew](https://brew.sh/):

```sh
brew install podman
```

The containers technology relies on Linux-specific features. Besides, many containers are based on GNU/Linux images. Podman therefore needs a virtual machine (VM) to run containers on MacOS. To download such a virtual machine, run:

```sh
podman machine init
```

You will see that podman downloads a virtual machine from [quay.io](quay.io).

You need to do this step only once: podman will find the downloaded file next time you will need it.

However, once per session (ie. every time you log out or restart your computer), you need to start the VM with:

```sh
podman machine start
```

## Create a container image

A container image is a template for containers. Several containers can be instantiated from the same image.

The definition of a container image must be in a file called `Containerfile`. Here is a minimal example:

```
FROM registry.access.redhat.com/ubi8/ubi:8.10
RUN <<EOF
dnf -y install python3.12 python3.12-pip
python3 -m venv /my-python-environment
source /my-python-environment/bin/activate
python3 -m pip install --upgrade pip
python3 -m pip install numpy
EOF
```

The `FROM` line specifies an operating system image that will be the foundation for our own custom image. Here we use an image based on Red Hat Enterprise Linux (RHEL) v8. Note that there are plenty other distributions you can use as a base system (Ubuntu, Fedora, etc.).

The `RUN` block specifies instructions that will be run inside the base image when our custom image is created. Here we install Python and Pip (`dnf` is RHEL's package manager), then we create a Python environment and install `numpy` within this environment.

To create the container image, run (choose the name you want for `$tag_of_the_image`):

```sh
podman build --platform=linux/amd64 --format=docker -t $tag_of_the_image /dir/containing/Containerfile
```

> [!NOTE]
> We build the image for the `linux/amd64` architecture because it is the architecture of the supercomputer I use (if you are on MacOS, it is probably not the same as your architecture). Here you will have to choose the correct architecture for your target system.

You can now list the exising images on your system:

```
podman image list
```

You should see at least two: the Red Hat image and your custom image.

Test your image:

```sh
podman run --rm -it $tag_of_the_image
```

Voilà! You are now within what looks like a Red Hat operating system within your MacOs system. You can test your python environment by running:

```sh
source /my-python-environment/bin/activate
```

and trying to import numpy from within python.

Use `ctrl D` to exit the container once you are done testing it.

## Use this container image on TGCC

First create a `.rar` file containing the image:

```sh
podman save -o $my_tar_file $tag_of_the_image
```

Then copy this file to TGCC (use `scp` or `rsync`).

The tool to manage containers on TGCC is called `PCOCC` (pronounced like the bird: peacock). Once logged into TGCC, import your image into your library of images (again, choose whatever name you want for `$tag_of_the_image`):

```
pcocc-rs image import docker-archive:$my_tar_file $tag_of_the_image
```

Now you can run a Python script through a container based on this image:

```sh
pcocc-rs run $tag_of_the_image /bin/bash -- --norc -c "source /my-python-environment/bin/activate ; python3 myscript.py"
```

> [!NOTE]
> We use the `--norc` flag for bash because otherwise your own `~/.bashrc` on TGCC will be loaded inside the container, which might create problems.

# Suggested reading

 - TGCC's [documentation page on containers](https://www-hpc.cea.fr/tgcc-public/en/html/toc/fulldoc/Virtualization.html#containers)
 - [Docker's documentation on Container files](https://docs.docker.com/reference/dockerfile/) (AKA Docker files)
 - A bit more detail about using containers with podman and pcocc [here](https://github.com/lucas-ige/containers)
 - Example of container files [here](https://github.com/lucas-ige/containers/tree/main/images)
