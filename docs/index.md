# Welcome to the ***<Jenkins Containers\>*** Project

This project site serves as a gathering point for resources
to build Docker containers that run [Jenkins](https://www.jenkins.io/).

# Reading Notes

* The terms ***container*** **|** ***image*** might be used interchangeably, best effort to keep consistent with the notion that containers are instances of an image. Hence terminology should be appropriate where needed. 
    * Well a container is just a writable layer on top of an image but that’s more detail than needed here.
* Currently the only images being built are Docker images, so any notion of a ***Jenkins Image*** **|** ***image*** is to be assumed as a Docker container/image.

## Types of Jenkins Images

* Base Image
    * Will contain **Jenkins** configurations that all children will use, e.g.
        * shell that the jobs will run in
        * user account(s)
        * global credentials
            * GitHub
* Child Image
    * The differentiation of children images will be based on the job(s) that **Jenkins** runs.
        * Based currently on **jobs.toml** (see **[Image Git Repo Layout](layouts.md)**)

### Image Git Repos

1. [jenkins-docker-base](https://github.com/reap2sow1/jenkins-docker-base)
    * This is the base image **Git repo** in which other **Jenkins images** will be built on top of.
2. [jenkins-docker-torkel](https://github.com/reap2sow1/jenkins-docker-torkel)

### Other Git Repos

1. [jcasc.py](https://github.com/reap2sow1/jcasc.py)
    * Used to aid in building **Jenkins images**.
2. [jenkins-infrastructure](https://github.com/reap2sow1/jenkins-infrastructure)
    * Used in miscellaneous tasks when managing a **Jenkins** environment.

### Image Docker Repos

1. [jenkins-base](https://hub.docker.com/repository/docker/reap2sow1/jenkins-base)
    * This is the base image **Docker repo** in which other **Jenkins images** will build on top of.
2. [jenkins-torkel](https://hub.docker.com/repository/docker/reap2sow1/jenkins-torkel)
    * Child image, contains following jobs:
        * [jenkins-packerbuilds](https://github.com/reap2sow1/jenkins-packerbuilds)
