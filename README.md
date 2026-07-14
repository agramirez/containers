# Dev Containers
These are useful docker images setup for various types of software development.  While they can be used alone in docker containers, it is recommended that they are used with VSCode and DevContainers so that a unified local development environment can be shared accross development teams.

## Base Container
This useful container contains basic tools like wget, curl, and others.  It also contains the [Rocq Theorem Prover](https://rocq-prover.org/) and [LaTex](https://www.latex-project.org/) which both take FOREVER to build, which is why they are included in this base image.  Other images can build off this one without having to download and install these components on every build.

> A published version of the image can be found in dockerhub at [agramirez2001/devcontainer:base](https://hub.docker.com/repository/docker/agramirez2001/devcontainer/general).
