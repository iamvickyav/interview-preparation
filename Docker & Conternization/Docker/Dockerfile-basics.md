## Basics of Dockerfile

### Deploying WAR file in Tomcat (Running in Docker)

To learn how to deploy WAR file in Tomcat running in Docker **using commands**, please follow the steps mentioned in this file
https://github.com/iamvickyav/preparation/blob/master/Docker/docker-basics.md

Now we are going to see how to do the same using Dockerfile. 

Here is the content of our Dockerfile

**Dockerfile is the file name without any extension**

```
FROM tomcat:latest
COPY target/demo.war /usr/local/tomcat/webapps/
CMD ["catalina.sh", "run"]
```

| Command       | Usage                                             |
| ------------- |---------------------------------------------------|
| FROM          | Base Image Name                                   |
| COPY          | To copy from source to destination                |
| CMD           | First command to be executed when Docker image run|


### How to build image from Dockerfile

Use the below command to build the docker image from a Dockerfile

```
> docker build -t my-img .
```

-t is for tagging a name to the image. In this case its my-img

**Note**: There is a .(dot) at end of the above docker build command. dot directs docker built command to look for Dockerfile in current directory

Use **docker images** command to check whether my-img got created successfully. 

**RUN** executes command(s) in a new layer and creates a new image. E.g., it is often used for installing software packages
**CMD** sets default command and/or parameters, which can be overwritten from command line when docker container runs
**ENTRYPOINT** configures a container that will run as an executable

**Reference**: https://goinbigdata.com/docker-run-vs-cmd-vs-entrypoint/

Thats all folks !!


