# Docker

- Docker is a platform which packages an application and all its dependencies together in the form of containers

- Docker works like Client-Server model

- Docker Daemon or Docker Runtime acts as the server & it can be communicated using Docker CLI client (Command Line Interface)

- Docker image is a template & Docker container is the running instance of the image. Every Docker image will have its own Id & Every Container instance also will have its own Id assigned.  We can create any number of Container instance from single Docker image

## Dockerizing application with Docker commands

Lets assume we have a Spring Boot application which generates executable JAR file (say Sample.jar). Typically, we can run the application with `java -jar Sample.jar`

Now its time to Dockerize this application. In order to run JAR file, we need Java

### Pull OpenJDK Java Image

First, we need to pull the OpenJDK Java image using `pull` command

```
docker pull tomcat:8.5.21-jre8-alpine
```

**Remember:** Specifying **tomcat:8.5.21-jre8-alpine** will always pull the latest image from Docker hub


### Verify if image got downloaded

Once pull command execution is complete, run `docker images` command to get list of images. You should see something like below as response

```sh
> docker images

REPOSITORY                      TAG                 IMAGE ID            CREATED             SIZE
tomcat:8.5.21-jre8-alpine       latest              d991231dccdf        4 weeks ago         113MB
```

### Running Docker Image (aka creating container)

```sh
> docker run -p 8080:8080 tomcat:8.5.21-jre8-alpine
```

#### Port mapping

In `docker run` command, its important to do port mapping using `-p` command. Reason is, Docker container runs on its own Operating system (mostly Linux flavour). So the tomcat mentioned in above run command, Tomcat will be running in 8080 port (default tomcat port) on Linux OS of the Docker container. 

But when we try to hit http://localhost:8080, we are hitting only 8080 port of our host machine but not the container's 8080. So its necessary to do port mapping to reach a port from outside the container 

To do port mapping, we have passed `-p 8080:8080` as argument for the run command. Here the `-p` argument represents the port to be mapped from Docker container to the Host machine. In `-p 8080:8080`, 8080 before the **colon (:)** represents the port number of host system & 8080 after the **colon (:)"** represents the port in container

#### Verify Container creation

Once we execute run command, Docker creates an instance for the Docker image called as the Docker container. Every container instance will have its own id assigned called CONTAINER_ID. The CONTAINER_ID can be verified using the `docker ps` command

```sh
> docker ps

CONTAINER ID        IMAGE                       COMMAND             CREATED             STATUS              PORTS                    NAMES
b414970f84c1        tomcat:8.5.21-jre8-alpine   "catalina.sh run"   10 seconds ago      Up 9 seconds        0.0.0.0:8080->8080/tcp   nifty_aryabhata
```

### Adding war file to Tomcat container

Now Tomcat container is up & running. Its time to copy our WAR file inside Tomcat container.

```sh
docker cp demo.war <CONTAINER_ID>:/usr/local/tomcat/webapps
```

For the `docker cp` command, we need the <CONATINER_ID> which we can use from output of `docker ps` command

```
docker cp demo.war b414970f84c1:/usr/local/tomcat/webapps
```

Once the cp command is succesful, you can notice in logs that Tomcat container delploying demo.war automatically & start the application

If you want to see the logs separately 

```sh
docker logs -f <CONATAINER_ID>
```

So thats all about running WAR file with Tomcat Docker Insance using Docker commands.

But do we need to remember all these commands & execute them one by one to get the job done ? Is there any simple alternative for it? Yes, Fortunately, we have Dockerfile to automate these steps
