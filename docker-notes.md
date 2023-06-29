# Docker notes

## Definitions

- **Image:** Your starting position. A blueprint. A template.
- **Container:** A running image. An instance. Each container should provide a single service; one for serving pages, one for a backend database, one for ftp, etc.
- **Host:** The computer running Docker.
- **Volumes:** Mount points between the host and the container.

## Commonly used commands

Start a new Docker container from an image.

`docker run`

Example to create a container from an image.

`docker run --env MYSQL_ROOT_PASSWORD=my-secret-pw --detach mysql`

List all the running Docker containers.

`docker ps`

Example list all the running containers in the background.

`docker ps --all`

Show the details of all the running, stopped, or exited containers.

`docker ps -a`

Stop a running container.

`docker stop`

Example stops a container using the container name or its id.

`docker stop <container_name or container_id>`

Remove a Docker container.

`docker rm`

List all the Docker images that are currently available on your system.

`docker images`

Download a Docker image from a registry.

`docker pull`

Execute a command in a running container.

`docker exec`

Example access the container that is running.

`docker exec -it test_db bash`

Manage multi-container Docker applications.

`docker-compose`

Log into a container.

`docker attach <container_name>`

Provide information about a container.

`docker inspect <container_name>`

Show the details of the list of networks in the cluster.

`docker network ls`

Free up some disk space. The image id is used to remove the image.

`docker rmi <image_id>`

Check the logs of all the docker containers with the corresponding contained id mentioned

`docker logs <container_id>`

## Docker compose

Bring up all services listed in docker-compose.yml file.

`docker-compose up -d`

Bring down all services listed in docker-compose.yml file.

`docker-compose down`

Bring up "node" service listed in docker-compose.yml file.

`docker-compose up node`

Clean up all services listed in docker-compose.yml file

`docker-compose rm -f`

Example docker-compose.yml

    version: "3"
    services:
        node:
            ports:
                - "8080:3000"
            build:
                context:-/
                dockerfile: Dockerfile
                container_name: nodeserver

Example Dockerfile

    FROM node:7.7.4-alpine
    EXPOSE 3000
    RUN mkdir /src
    COPY app.js /src
    WORKDIR /src
    CMD node app.js

The example Dockerfile above:

- Makes port 3000 available for mapping.
- Makes a directory called /src on the image.
- Copies the file app.js from current working directory within the host to the new /src directory on the image.
- Sets the current working directory of the image to /src.
- Runs the command node with the argument app.js when the container starts up.
