## Build Mindset

* Future changes to **Jenkins Image** construction should use the following mindset (the term Philosophy is a bit too fancy here). The lifecycle of building a **Jenkins Image** is as followed:
    1. Preimage Build
        * The operations needed to gather all the resources for an image build should occur here.
            * What this means for ‘**Image Builds**’: We want to ensure that **Dockerfiles** are easy to follow, and can be maintained. Multistage builds are ok, but not for just running one command and gathering its results. Multistage builds should be used judiciously.
            * What this means for ‘**Container Runtime**’: There should be a narrow scope for what a container should do at runtime. Env vars evaluation for **Jenkins** is ok, but pulling a bunch of resources and performing plenty of groovy scripts with the job-dsl plugin is excessive and prone to error.
                * e.g. docker-compose injects env vars into container runtime based on what you pass in as their values. **JCasC plugin** evaluates these env vars if they exist when looking in the ‘casc.yaml’.
    2. Image Build
        * Should keep the **Dockerfiles** simple and easy to follow. Simple activities like updating packages, chmoding files, and copying files over from the **Docker context** are encouraged. However, mangling the image file system is not.
    3. Container Runtime
        * Aside from what is written above
        * The modularity of a ***Jenkins Image*** shines here, as ‘**casc.yaml**’ will ***heavily*** utilize env vars to be evaluated at runtime. This allows the same image to be run differently depending on the need(s).
