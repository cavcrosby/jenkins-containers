# Jenkins Containers Project Site

This project site serves as a gathering point for resources
to build Docker containers that run [Jenkins](https://www.jenkins.io/).

# Reading Notes

* The terms ***container*** **|** ***image*** might be used interchangeably, it will be of best effort to keep consistent with the notion that containers are instances of an image. Hence terminology should be appropriate where needed.
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

1. [jenkins-docker-base](https://github.com/cavcrosby/jenkins-docker-base)
    * A base image **Git repo** in which other **Jenkins images** will be built on top of.
2. [jenkins-docker-torkel](https://github.com/cavcrosby/jenkins-docker-torkel)

### Other Git Repos

1. [jcascutil](https://github.com/cavcrosby/jcascutil)
    * Used to aid in constructing configuration as code (CasC) files for **Jenkins**.
2. [infrastructure](https://github.com/cavcrosby/infrastructure)
    * Used in miscellaneous tasks when managing a **Jenkins** environment.

### Image Docker Repos

1. [jenkins-base](https://hub.docker.com/repository/docker/cavcrosby/jenkins-base)
    * A base container, built from the respective **Image Git Repo**.
2. [jenkins-torkel](https://hub.docker.com/repository/docker/cavcrosby/jenkins-torkel)
    * A child container, contains following jobs:
        * [jenkins-packerbuilds](https://github.com/cavcrosby/jenkins-packerbuilds)
