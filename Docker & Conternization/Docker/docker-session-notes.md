
# Docker session notes

## Commands Used

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

```

## Dockerfiles used

### Dockerfile 1: Docker image alpine  + Java manually installed + Checking Java version

```
FROM alpine:3.11
RUN apk add openjdk11
CMD ["/usr/bin/java", "-version"]
```

### Dockerfile 2: Docker image alpine  + Java manually installed + Copy JAR + Running JAR file

```
FROM alpine:3.11
RUN apk add openjdk11
COPY target/H2Sample.jar H2Sample.jar
CMD ["/usr/bin/java", "-jar", "H2Sample.jar"]
```

### Dockerfile 3: Docker tomcat image (alpine OS, Java, Tomcat installed by default) + Copy WAR file to Webapps folder + Running WAR file

```
FROM tomcat:8.5.21-jre8-alpine
COPY target/H2Sample.war /usr/local/tomcat/webapps
CMD ["catalina.sh","run"]
```
---

## Understanding Dockerfile

**FROM** - BASE IMAGE NAME to start with

**CMD** - Commands to be executed while running the container (docker run command)

**RUN** - Run the command while building the image (docker build command)

**COPY** - Copy from source to destination

**ADD** - Can be used in place of COPY command. Copies content from source to destination. Also can copy file from URL

---

## Things to note

**Note 1:** `catalina.sh run` command will run Tomcat is foreground & will not let container shutdown. So we can see container id in `docker ps` command

**Note 2:** In the destination side of `COPY` command, if we are not specifying file name, the same file name will be used

      E.g. `COPY target/H2Sample.war /usr/local/tomcat/webapps` will copy H2Sample.war into webapps folder without changing name

      E.g. `COPY target/H2Sample.war /usr/local/tomcat/webapps/vicky.war` will copy H2Sample.war but in the name vicky.war into webapps folder

**Note 3:** `docker build` command will try to use existing images from cache while building image

**Note 4:** Make sure you remove not only unwanted images built and also all stopped containers often. Refer to Commands Used section for the same
