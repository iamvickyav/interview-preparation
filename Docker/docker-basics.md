# Docker 

> Docker is a platform which packages an application and all its dependencies together in the form of containers


## Step by Step Instruction to run Spring Boot War file in Tomcat running in Docker

### Pull Tomcat Docker Image

First, we need to pull the tomcat docker image from docker hub (Refer https://hub.docker.com/_/tomcat)

Use the below command

```
docker pull tomcat
```

**Remember:** Specifying the word **"tomcat"** alone will always pull the latest image from docker hub. If you want to pull particular version, you have to specify version like below

```
docker pull tomcat:8.0
```

*Docker Tomcat images comes with Java pre-installed.

### Check if Image got downloaded

Once tomcat docker image is downloaded, run images command to get list of images downloaded in your local. You should see something like below as response 

```
> docker images

REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
tomcat              latest              4e7840b49fad        4 weeks ago         529MB
```

### Run Docker Image (starting container)

While starting Docker image, its important to bind ports. Ok What I mean by bind ports here. We all know Docker runs in its own environment. if we run Tomcat docker image, it will be running in 8080 port (default tomcat port) of docker container. But when we try to hit http://localhost:8080, we are hitting only 8080 port of our sytem's 8080 not the container's 8080 port

Hence its necessary to bind the container 8080 port to our system's 8080 port

```
docker run -p 8080:8080 tomcat
```

### Add war file to tomcat running in Docker container

Now tomcat is ready & running in 8080. Its time to add our war file to Tomcat. In order to do it, we can use the copy command available with Docker

```
docker cp demo.war <CONTAINER_ID>:/usr/local/tomcat/webapps
```

For the above command to run, we need the <CONATINER_ID>. To get container id, use the following command

```
> docker ps

CONTAINER ID     IMAGE      COMMAND             CREATED             STATUS          PORTS                    NAMES
e361c2d2ebf8     tomcat     "catalina.sh run"   8 seconds ago       Up 6 seconds    0.0.0.0:8080->8080/tcp   wonderful_heisenberg
```

Copy container id from result of docker ps command & use it in docker cp command

```
docker cp demo.war e361c2d2ebf8:/usr/local/tomcat/webapps
```

Once the cp command is succesful, you can notice tomcat docker instance delploying demo.war automatically & start the application

In order to see the logs of tomcat docker instance 

```
docker logs -f <CONATAINER_ID>
```

<CONATAINER_ID> should be taken from docker ps command

Thats all folks !!
