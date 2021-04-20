# Tagging Commits In Image Git Repos

* Current versioning schema roughly looks like this: ‘**vx.x.x**’, with **x** being some positive int. Should represent **major.minor.patch**, that being the intent.
* When tagging a point in the commit tree, the following process is in place (again, just at a best effort level). Should be followed in ***descending*** order, these are known as **rules**:
    1. If the **Dockerfile** changed as part of a new commit, then the image has changed and the tag should be incremented.
    2. If some part of an image file system has changed (e.g. **casc.yaml** that should be in the **$JENKINS_HOME**), then the most recent tag (e.g. if v1.0.0 and v1.0.1 exist, v1.0.1 would be the most recent tag) should be removed from its previous commit and reassigned to the new commit but not incremented. 
    3. If the **Dockerfile** has not changed, and no part of an image’s file system has changed, then no tagging needs to occur with the new commit.
        * To follow this **rule**, if a base image changes, the child image does not need to increment its tag.
        * ***EXTRA NOTE***: Jenkins Images built for a particular version can be from a commit that follows **rule (ii)** or any commit that follows **rule (iii)**. If in the commit tree there are sequential commits (e.g. 2 or more) that follow **rule (iii)** then a particular version can be built from any of these commits.
* Image file system changes > **Dockerfile** changes
    * This needs to be brought up because looking at **rule (ii)** in the above procedure list, moving a particular tag to a new commit when its file system has changed means there is now some unknown knowing when that image changed (aka, the tag incremented).
        * Rational is that currently Dockerfiles have been skimmed down and the actual image should not change as often as its contents.

# Building Jenkins Images

***NOTE: TAGGING COMMITS SHOULD OCCUR FIRST AND BE SORTED OUT! OTHERWISE THERE IS NO GUARANTEE AN IMAGE WILL BE IN LINE WITH ITS IMAGE GIT REPO.***

* To make the process of running a docker build easier, each Image Git Repo should provide a **setup** script that will prepare everything to construct a **Jenkins Image**. This script will more than likely utilize the **jcasc.py** program.
    * This serves two fold:
        * To provide a blueprint/trail for the ‘**casc.yaml**’ to be used by the **Jenkins** service in the container. This is so we know how the **casc.yaml** was created. Though again, this isn’t an image change but a **Jenkins** config change.
        * To have fewer keystrokes used...a programmer’s goal ideally.
* **docker build** works here, though it should be mentioned the **jcasc.py** program does provide a docker-build command that provides some convenience.
    * If using just **docker build**, currently I also append the follow options (this is for **official builds** anyways):
        * --no-cache
        * --build-arg
        * BRANCH=
            * You will have to assign the current branch the repo is in.
        * --build-arg
        * COMMIT=
            * You will have to assign a commit that the image was built off of.
        * --tag
        * name:tag (**Docker** format for tags)
        * “.” (the context to send to the **Docker Daemon**)

