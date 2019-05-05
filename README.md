### Introduction
This repository is an example of Gitlab CI/CD.   

The pipeline is as follow:
1. **test**: Run the tests on a *node:8.11-alpine* Docker container.
2. **build**: Build the image with Docker using the Dockerfile.
3. **deploy**: Stop and remove the running container and start a new one with the new built image.

The **build** and **deploy** stages are only run when a modification occurs on the master branch (which is here used as the production branch).   
However, every branch will run the **test** stage on modification.   

The **deploy** stage actually "reload" the locally running container.   
On a real production case, we would have push the new built image on a registry.   
The container "reloading" procedure have to be managed on the target server side.   

### Runners
The configuration requires two runners:
1. Executor: *shell*, tags: *docker*.
2. Executor: *docker*, image: *node:8.11-alpine*, tags: *node*.