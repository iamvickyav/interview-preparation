# docker-compose.yaml basics

## Introduction

When we want to run Multi-container Docker application, we have to go for docker-compose.yaml

docker-compose can able to start multiple container services at a time. The configuration is written in YAML format
 
## End to End containerization of Sample Application

### Dockerfile & docker-compose.yaml sample files
 
Lets say we have a Demo web application developed using SpringBoot which uses MySQL for database. Lets first containerize the application entirely first using Dockerfile & docker-compose.yaml..

**Dockerfile**
```
FROM openjdk:8-jdk-alpine
COPY EmpApp.jar EmpApp.jar
CMD ["java", "-jar", "EmpApp.jar"]
```

**docker-compose.yaml**
```
version : '3'
services :
  webapp :
    build : .
    image : web-app
    ports :
      - "8080:8080"
  dbapp :
    image : mysql:5.7
    restart : always
    environment :
      MYSQL_DATABASE : 'MY_DB'
      MYSQL_ROOT_PASSWORD : 'rootroot'
    expose :
      - "3306"
    ports :
      - "3306:3306"
    volumes :
      - ./sqlscript:/docker-entrypoint-initdb.d
      - ./data:/var/lib/mysql
```

### docker-compose file explained 

|   Docker-compose       |   Value                  |   Description                                                                                            |
|------------------------|--------------------------|----------------------------------------------------------------------------------------------------------|
|   version              |   3                      |   Version of Docker compose we want to use. It should be the first line in docker-compose.yaml file      |
|   services             |                          |   Configuration for each Docker container we want, is specified under services                           |
|   webapp               |                          |   User provided name for the Spring Boot web app service                                                 |
|   build                |   . (Dot)                |   Specify Dockerfile location. Use (Dot) if the Dockerfile & docker-compose.yaml are in same directory   |
|   image                |   my-img                 |   Custom Image name                                                                                      |
|   ports                |   8080:8080              |   Ports we want to expose outside of Docker container. The format is <HOST_IP>:<CONTAINER_IP>            |
|   dbapp                |                          |   User provided name for the Database container service                                                  |
|   image                |   mysql:5.7              |   Image name & its version to download from docker hub                                                   |
|   restart              |   always                 |   To restart the container every time                                                                    |
|   environment          |                          |   Environment variables we want to pass while starting the MySQL Container                               |
|   MYSQL_DATABASE       |   MY_DB                  |   Database to be created on Container startup                                                            |
|   MYSQL_ROOT_PASSWORD  |   Rootroot               |   Password for MySQL Root user account                                                                   |
|   expose               |   8080                   |   Port to be exposed for inter container communication                                                   |
|   ports                |   8080:8080              |   Ports we want to expose outside of Docker container. The format is <HOST_IP>:<CONTAINER_IP>            |
|   volumes              |   ./data:/var/lib/mysql  |   Volumes we want to mount from host to Docker container                                                 |

<hr>

## Setting DB Connection String properly

### Default DB Connecting String

Typically to connect Spring Boot with MySQL, **connection string** used to be like this

```
spring.datasource.url=jdbc:mysql://localhost:3306/MY_DB?useSSL=false&allowPublicKeyRetrieval=true
```

If you notice, the connection string refers to localhost:3306 for MySQL. Since we containerized the entire application, MySQL will run on its own container. So connecting from SpringBoot container with MySQL container is not gonna work with localhost. 

Hence we need to use the networking capabilities of the Docker to make inter cotainer communication possible

### Fixing DB Connecting String for MySQL running in Container

spring.datasource.url=jdbc:mysql://<del>localhost</del>:3306/ORDER_DB?useSSL=false&allowPublicKeyRetrieval=true

spring.datasource.url=jdbc:mysql://**dbapp**:3306/ORDER_DB?useSSL=false&allowPublicKeyRetrieval=true

**dbapp** is nothing but the name we given for the MySQL image in docker-compose.yaml file. Refer to line 31 above for **dpapp**

## Starting multiple containers with docker-compose.yaml file

In order to start the application, we can use either of the following commands

```sh
> docker-compose up

or

> docker-compose up --build
```

Thats all folks !!!
