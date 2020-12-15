# Docker Commands

```sh
# Information about Docker
> docker info

# For downloading image from Docker hub
> docker pull alpine:3.11

# To see list of images downloaded
> docker image ls 
(or)
> docker images

# To run a image (or) To start a container
> docker run <img-id>

# To do port mapping from container to host system (MacOS) while starting
# Leftside - represents Host Port (MacOS port) & right side is container port number
> docker run -p 8080:8080 <img-id>
> docker run -p 9001:8080 <img-id>

# To see container information (container id)
> docker ps 
(or)
> docker container ls

# To stop a container
> ctrl + c 
(or)
> docker container stop <container-id>

# To see list of stopped containers
> docker container ls -a

# To see list of stopped containers (container Id alone)
> docker container ls -aq

# To remove stopped container from host system
> docker container rm -f <container-id>

# To remove all stopped containers from host system
> docker container rm -f $(docker container ls -aq)

# To remove a Docker image
> docker image rm -f <img-id>

# Open bash inside Container
> docker exec -it d541afb504bd bash

# To find IP address of container
> docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' <CONTAINER_ID>

# logs
> docker logs <CONTAINER_ID>
```
