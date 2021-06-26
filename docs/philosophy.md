## Build Philosophy

* Future **Jenkins Images** created should adhere (assuming a **Image Git/Docker** repo is created like the others) to the following philosophy. The lifecycle of building a **Jenkins Image** is as followed:
    1. Preimage Build
        * The operations needed to gather all the resources for an image build should occur here.
            * What this means for ‘**Image Builds**’: We want to ensure that **Dockerfiles** are easy to follow, and can be maintained. That said, with all the resources gathered in this step means that **Image Builds** can easily transfer over contents using the **Docker context**.
            * What this means for ‘**Container Runtime**’: Like **Image Builds**, **Container Runtime** also benefits from having all the resources needed when at runtime. This removes a moderate amount of runtime error from occurring and ensures for a more deterministic runtime. Pulling additional resources from the network or running additional groovy scripts only complicate the runtime.
    2. Image Build
        * To reiterate, **Dockerfiles** should be simple and easy to follow. Simple activities like updating packages, chmoding files, and copying files over from the **Docker context** are encouraged. However, mangling the image file system is not. Multistage builds are ok, but not for just running one command and gathering its results. Multistage builds should be used judiciously.
    3. Container Runtime
        * There should be a narrow scope for what a container should do at runtime. That said, the modularity of a ***Jenkins Image*** shines here, as ‘**casc.yaml**’ will ***heavily*** utilize environment variables to be evaluated at runtime. This allows the same image to be run differently depending on the need(s).
            * e.g. One way to ensure that environment variables are set at runtime for the **Jenkins Image** is to use docker-compose. docker-compose injects environment variables into the container runtime based on what you pass in as their values. The **JCasC plugin** evaluates these environment variables if they exist when looking in the ‘**casc.yaml**’.
