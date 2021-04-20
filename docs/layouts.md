# Image Git Repo Layout

* This is expected to change overtime. ***So don’t rely on this indefinitely.***
* This also should be what must be in a **Image Git Repo**, you may or may not find other files tracked by the repos. Will denote optional files.
* Base Image:
    * .gitignore
    * **casc.yaml** (optional)
        * Can use a different filename. Must have ‘casc’ somewhere in its filename and yaml/yml as the filename extension.
    * Dockerfile
    * plugins.txt
* Child Image:
    * .gitignore
    * **child-casc.yaml** (optional)
        * Can use a different filename. No restrictions here.
        * This is used to be merged with the base image’s ‘**casc.yaml**’.
    * docker-compose.yaml (optional)
    * Dockerfile
    * jobs.toml
        * Used by the **jcasc.py** program.
    * setup
