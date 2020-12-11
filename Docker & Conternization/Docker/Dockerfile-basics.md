# Dockerfile

Dockerfile represent the list of steps to create a Docker image. The file should be created with name **Dockerfile** without any extension

## Sample Dockerfiles

### Alpine Linux Distribution + Java

```
FROM alpine:3.11
RUN apk add openjdk11
CMD ["/usr/bin/java", "-version"]
```

### Alpine Linux Distribution + Tomcat
```
FROM tomcat:8.5.21-jre8-alpine
COPY target/Sample.war /usr/local/tomcat/webapps
ENTRYPOINT ["catalina.sh", "start"]
```

### Alpine + Java

```
FROM alpine:3.11
# While building the image
RUN apk add openjdk11
# COPY from Source to Destination
COPY target/H2Sample.jar H2Sample.jar
# While running the image(container)
CMD ["/usr/bin/java", "-jar", "H2Sample.jar"]
```

### Deploying WAR with Tomcat

```
FROM tomcat:latest
COPY target/demo.war /usr/local/tomcat/webapps/
CMD ["catalina.sh", "run"]
```

## Building image from Dockerfile

To build a Docker image, 

```
> docker build -t my-img .
```

* -t is for tagging a name to the image. In this case its my-img

* There is a .(dot) at end of the above docker build command. dot meant to say docker build command should look for Dockerfile in current directory

## Verify image creation

* Use `docker images` command to check whether my-img got created successfully


## Understanding Dockerfile

**RUN** executes command(s) in a new layer and creates a new image. E.g., it is often used for installing software packages
**CMD** sets default command and/or parameters, which can be overwritten from command line when docker container runs
**ENTRYPOINT** configures a container that will run as an executable

**Refer**: https://goinbigdata.com/docker-run-vs-cmd-vs-entrypoint/

## More Dockerfile samples



