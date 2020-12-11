# Dockerfile

Dockerfile represents the list of steps to create a Docker image. The file should be created with name **Dockerfile** without any extension. Dockerfile help us avoid building Docker image with Docker commands

## Building Tomcat Image 

### Dockerfile

```
FROM tomcat:8.5.21-jre8-alpine
COPY target/Sample.war /usr/local/tomcat/webapps
ENTRYPOINT ["catalina.sh", "start"]
```

### Building image from Dockerfile

Docker build command is used for creating image from Dockerfile

```
> docker build -t my-img .
```

Here `-t` is for tagging a name to the image which in this case **my-img**. There is a .(dot) at end of `docker build` command to tell build command that Dockerfile is in current directory

### Verify image creation

* Use `docker images` command to check whether my-img got created successfully

```
> docker images
```

### Understanding Dockerfile

|   FROM        |   Represents the base image to start with our image building                                                                              |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------|
|   COPY        |   COPY from source path (host system) to a path inside container                                                                          |
|   ADD         |   ADD is similar to COPY except that ADD can also download files from URL and copy it to a path inside container                          |
|   RUN         |   Command to be executed while building the Docker image. Usually used for installing Software packages                                   |
|   CMD         |   Default command to be executed while starting the Docker container. If there are multiple CMD commands, the last CMD will be considered |
|   ENTRYPOINT  |   To make our Docker image an Executable one                                                                                              |


## More Dockerfile samples

### Alpine Linux Distribution + Java

```
FROM alpine:3.11
RUN apk add openjdk11
CMD ["/usr/bin/java", "-version"]
```

### Tomcat
```
FROM tomcat:latest
COPY target/demo.war /usr/local/tomcat/webapps/
CMD ["catalina.sh", "run"]
```

### Alpine + Java

```
FROM alpine:3.11
RUN apk add openjdk11
COPY target/H2Sample.jar H2Sample.jar
CMD ["/usr/bin/java", "-jar", "H2Sample.jar"]
```

Ok. What if we need to create & run multiple Docker containers at a same time ? If we have multiple containers, how the inter container communication takes place ? The answer is the **docker-compose.yaml** file
