
# Docker session

## Dockerfiles used

### Dockerfile 1: Docker image alpine  + Java installed

```
FROM alpine:3.11
# Executed while building the image
RUN apk add openjdk11
# While running the image(container)
CMD ["/usr/bin/java", "-version"]
```

### Dockerfile 2: Docker image alpine  + Java installed + Copy JAR + Running JAR file

```
FROM alpine:3.11
# Executed while building the image
RUN apk add openjdk11
# COPY from Source to Destination
COPY target/H2Sample.jar H2Sample.jar
# While running the image(container)
CMD ["/usr/bin/java", "-jar", "H2Sample.jar"]
```

### Dockerfile 3: Docker tomcat image + Copy WAR file to Webapps folder + Running WAR file

```
# Download Tomcat
FROM tomcat:8.5.21-jre8-alpine
# COPY WAR file
COPY target/H2Sample.war /usr/local/tomcat/webapps
# Start Tomcat
CMD ["catalina.sh","run"]
```

----
### Commands Used

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

```



