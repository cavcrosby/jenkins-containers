# Image Git Repo Layout

* This is expected to change overtime. ***So don’t rely on this indefinitely.***
* This should be what is expected in a **Image Git Repo**, you may or may not find additional files in other image repos. Will denote optional files.
* Base Image:
    * .gitignore
    * **casc.yaml** (optional)
        * Can use a different filename. Must have ‘**casc**’ somewhere in its filename and '**yaml' or '**yml**' as the filename extension.
            * Assuming you wish to use the Dockerfile as is.
            * Also assuming you are using the **jcascutil** program as is.
    * Dockerfile
    * plugins.txt
* Child Image:
    * .gitignore
    * **child-casc.yaml** (optional)
        * Can use a different filename. No restrictions here.
        * This is used to be merged with the base image’s ‘**casc.yaml**’.
    * docker-compose.yaml (optional)
    * Dockerfile
    * Makefile
    * jobs.toml
        * Used by the **jcascutil** program.
    * setup
